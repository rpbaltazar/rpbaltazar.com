---
author: rpbaltazar
categories:
- Rails
date: "2019-04-07T00:00:00Z"
tags:
- DateRange
- Data Manipulation
title: The Strange Date Range Case
---
> There are only two hard things in Computer Science: cache invalidation and naming things
>  - *Phil Karlton*
>
> There are only two hard problems in CS: Cache invalidation and How to quit Vim
> - *Aaron Patterson*


Luckily for me, after 10 years of having vim open, I managed to learn how to quit. When it comes to naming things, I always blame the "non native speaker" in me, so that is also out of the way.

Given this, I see time, Timezones and dates as a pain and hard thing to solve correctly as well.
Today, I'd like to write a bit more about dates in particular.

Recently, we were developing a simple small DateRange class for our Rails application, which I'm sure many of us have written before. The main goal of this DateRange is to provide us with an array of dates between start and end dates, as well as this same date range in different steps.

So initially we wrote something along these lines:

```ruby
class DateRange
  def initialize(start_date = nil, end_date = nil)
    @start_date = start_date || Date.today
    @end_date = end_date || Date.today
  end

  def days_grouped_by_month
    # NOTE: Consider providing the to_a method for the date range
    # instances if we start to use more often.
    date_range.to_a.group_by { |date| "#{date.month}-#{date.year}" }
  end

  def in_monthly_step
    dates = []
    current_date = @start_date
    while current_date <= @end_date
      dates << current_date
      current_date = current_date >> 1
    end
    dates
  end

  private

  def date_range
    (@start_date..@end_date)
  end
end
```

Let's look at our initial use case scenario:

```ruby
start_date = Date.parse('01-01-2019')
end_date = Date.parse('03-04-2019')
dr = DateRange.new(start_date, end_date)
monthly_dates = dr.in_monthly_step
# => [Tue, 01 Jan 2019, Fri, 01 Feb 2019, Fri, 01 Mar 2019, Mon, 01 Apr 2019]
```

This seemed to work perfectly fine until we had to rely on end of months date ranges.

When we use `current_date >> 1` this shifts the date one month forward. The problem is
that it doesn't behave consistently. It is quite understandable why. Putting a bit of
thought into this, leads to the usual question: when you have months with different
number of days (e.g. Jan-31, Feb-28/29, Apr-30, ...) how do you decide what a monthly step
is? I think this leads to a lot of discussion because it is not clear and there is no
consensus on how this should behave.

What is the expected behavior when you have, for example:

```ruby
start_date = Date.parse('01-01-2019')
next_date = start_date + 1.month
# next_date = ?
```

In this case `next_date` will be `Fri, 01 Feb 2019` so it means we've travelled 31 days. But then, when we have:

```ruby
start_date = Date.parse('31-01-2019')
next_date = start_date + 1.month
# next_date = ?
```

`next_date` will be `Thu, 28 Feb 2019` so it means we've travelled 28 days.

In my opinion, the behavior would be consistent here if

```ruby
start_date = Date.parse('28-02-2019')
next_date = start_date + 1.month
# next_date = ?
```

were to return `Sun, 31 Mar 2019` but instead, it returns `Thu, 28 Mar 2019`.
To add to the confusion, if we were to add 2 months instead of 1 in January 31,
we do get `Sun, 31 Mar 2019`.

```ruby
start_date = Date.parse('31-01-2019')
next_date = start_date + 2.month
```

Given this, the outcome of our discussion was that based on our use cases we
should have two separate methods:
- `in_monthly_step` - that will give us the dates moving on a monthly basis,
taking in account the monthly shifts that might happen.
(e.g 30/01/2019, 28/02/2019, 30/03/2019 or 15/01/2019, 15/02/2019, 15/03/2019)

- `end_of_months_in_date_range` - this will give us all date ranges that
fall within the start and end dates.

```
sd=30/01/2019
ed=30/04/2019
end_of_months_in_date_range => [31/01/2019, 28/02/2019, 31/03/2019, 30/04/2019]
```

While

```
sd=01/01/2019, ed=25/04/2019
end_of_months_in_date_range => [31/01/2019, 28/02/2019, 31/03/2019]
```

Here is the simplified final version:

```ruby
class DateRange
  def initialize(start_date = nil, end_date = nil)
    @start_date = start_date || Date.today
    @end_date = end_date || Date.today
  end

  def days_grouped_by_month
    # NOTE: Consider providing the to_a method for the date range
    # instances if we start to use more often.
    date_range.to_a.group_by { |date| "#{date.month}-#{date.year}" }
  end

  def end_of_month_in_range
    dates = days_grouped_by_month.values.map(&:last)
    dates.pop unless @end_date == @end_date.end_of_month
    dates
  end

  def in_monthly_step
    dates = []
    current_date = @start_date
    while current_date <= @end_date
      dates << current_date
      current_date = current_date >> 1
    end
    dates
  end

  private

  def date_range
    (@start_date..@end_date)
  end
end
```

Because I felt that we could benefit in the future from it, I decided to extract
the code to a [gem itself](https://github.com/rpbaltazar/jiff-date_range) that
does not rely on Rails' Date methods nor DateTime.
At the time of writing I haven't yet tested it with rails for any unforseen
conflicts, but in theory because its written on top of Ruby's Date, it should
support Rails with no issues. You might want to take a look at it and feel free
to comment, use it or open any issues you might find.

The gem implementation has a couple more useful methods that I don't mention here
such as `include?`, `overlap?` and `overlap`. These make sense to exist as part
of the DateRange.
