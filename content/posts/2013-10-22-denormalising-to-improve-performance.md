---
author: rpbaltazar
categories:
- Computer Science
date: "2013-10-22T07:00:28Z"
guid: http://balazar.net/random/?p=11
id: 11
tags:
- Database
- normalization
- performance
title: Denormalising to improve performance?
url: /2013/10/22/denormalising-to-improve-performance/
---
Chris Date, which advanced the relational data model along with Dr Ted Codd, its creator, got tired of misinformed arguments against normalisation and systematically demolished them using scientific method &#8211; he got large databases and _tested_ these assertions. I think he wrote it up in _Relational Database Writings 1988-1991_ but this book was later rolled into edition six of _Introduction to Database Systems_. This is _the_ definitive text on database theory and design, currently in its eighth edition. Chris Date was an expert in this field when most of us were still running around barefoot.

He found that:

  * Some of them hold for special cases
  * All of them fail to pay off for general use
  * All of them are significantly worse for other special cases

It all comes back to mitigating the size of the working set. Joins involving properly selected keys with correctly set up indexes are cheap, not expensive, because they allow significant pruning of the result _before_ the rows are materialised.

Materialising the result involves bulk disk reads which are the most expensive aspect of the exercise by an order of magnitude. Performing a join, by contrast, logically requires retrieval of only the _keys_. In practice, not even the key values are fetched: the key hash values are used for join comparisons, mitigating the cost of multi-column joins and radically reducing the cost of joins involving string comparisons. Not only will vastly more fit in cache, there&#8217;s a lot less disk reading to do.

Moreover, a good optimiser will choose the most restrictive condition and apply it before it performs a join, very effectively leveraging the high selectivity of joins on indexes with high cardinality.

Admittedly this type of optimisation can also be applied to denormalised databases, but the sort of people who _want_ to denormalise a schema typically don&#8217;t think about cardinality when (if) they set up indexes.

It is important to understand that table scans (examination of every row in a table in the course of producing a join) are rare in practice. A query optimiser will choose a table scan only when one or more of the following holds.

  * There are fewer than 200 rows in the relation (in this case a scan will be cheaper)
  * There are no suitable indexes on the join columns (if it&#8217;s meaningful to join on these columns then why aren&#8217;t they indexed? fix it)
  * A type coercion is required before the columns can be compared (WTF?! fix it or go home)
  * One of the arguments of the comparison is an expression (no index)

Performing an operation is more expensive than not performing it. However, performing the _wrong _operation, being forced into pointless disk I/O and then discarding the dross prior to performing the join you really need, is _much_ more expensive. Even when the &#8220;wrong&#8221; operation is precomputed and indexes have been sensibly applied, there remains significant penalty. Denormalising to precompute a join &#8211; notwithstanding the update anomalies entailed &#8211; is a commitment to a particular join. If you need a _different_ join, that commitment is going to cost you _big_.

If anyone wants to remind me that it&#8217;s a changing world, I think you&#8217;ll find that bigger datasets on gruntier hardware just exaggerates the spread of Date&#8217;s findings.

For all of you who work on billing systems or junk mail generators (shame on you) and are indignantly setting hand to keyboard to tell me that you know for a fact that denormalisation is faster, sorry but you&#8217;re living in one of the special cases &#8211; specifically, the case where you process _all_ of the data, in-order. It&#8217;s not a general case, and you _are_ justified in your strategy.

You are _not_ justified in falsely generalising it. See the end of the notes section for more information on appropriate use of denormalisation in data warehousing scenarios.

I&#8217;d also like to respond to &#8220;Joins are just cartesian products with some lipgloss&#8221;.

What a load of bollocks. Restrictions are applied as early as possible, most restrictive first. You&#8217;ve read the theory, but you haven&#8217;t understood it. Joins are _treated_ as cartesian products to which predicates apply _only_ by the query optimiser. This is a symbolic representation (a normalisation, in fact) to facilitate symbolic decomposition so the optimiser can produce all the equivalent transformations and rank them by cost and selectivity so that it can select the best query plan.

The only way you will ever get the optimiser to produce a cartesian product is to fail to supply a predicate: `SELECT * FROM A,B`

## Notes

  * David Aldridge provides some important additional information.
  * There is indeed a variety of other strategies besides indexes and table scans, and a modern optimiser will cost them all before producing an execution plan.
  * A practical piece of advice: if it can be used as a foreign key then index it, so that an index strategy is_available_ to the optimiser.
  * I used to be smarter than the MSSQL optimiser. That changed two versions ago. Now it generally teaches _me_. It is, in a very real sense, an expert system, codifying all the wisdom of many very clever people in a domain sufficiently closed that a rule-based system is effective.

&#8220;Bollocks&#8221; may have been tactless. I am asked to be less haughty and reminded that math doesn&#8217;t lie. This is true, but not all of the implications of mathematical models should necessarily be taken literally. Square roots of negative numbers are very handy if you carefully avoid examining their absurdity (pun there) and make damn sure you cancel them all out before you try to interpret your equation.

A cartesian product is a relation. A join is a function. More specifically, a join is a relation-valued function. With an empty predicate it will produce a cartesian product, and checking that it does so is one correctness check for a database query engine, but nobody writes unconstrained joins in practice because they have no practical value outside a classroom.

I called this out because I don&#8217;t want readers falling into the ancient trap of confusing the model with the thing modelled. A model is an approximation, deliberately simplified for convenient manipulation.

The cut-off for selection of a table-scan join strategy may vary between database engines. It is affected by a number of implementation decisions such as tree-node fill-factor, key-value size and subtleties of algorithm, but broadly speaking high-performance indexing has an execution time of _k_ log _n_ + _c_. The C term is a fixed overhead mostly made of setup time, and the shape of the curve means you don&#8217;t get a payoff (compared to a linear search) until _n_ is in the hundreds.

## Sometimes denormalisation is a good idea

Denormalisation is a commitment to a particular join strategy. As mentioned earlier, this interferes with _other_ join strategies. But if you have buckets of disk space, predictable patterns of access, and a tendency to process much or all of it, then precomputing a join can be very worthwhile.

You can also figure out the access paths your operation typically uses and precompute all the joins for those access paths. This is the premise behind data warehouses, or at least it is when they&#8217;re built by people who know why they&#8217;re doing what they&#8217;re doing, and not just for the sake of buzzword compliance.

A properly designed data warehouse is produced periodically by a bulk transformation out of a normalised transaction processing system. This separation of the operations and reporting databases has the very desirable effect of eliminating the clash between OLTP and OLAP (online transaction processing ie data entry, and online analytical processing ie reporting).

An important point here is that apart from the periodic updates, the data warehouse is _read only_. This renders moot the question of update anomalies.

Don&#8217;t make the mistake of denormalising your OLTP database (the database on which data entry happens). It might be faster for billing runs but if you do that you will get update anomalies. Ever tried to get Reader&#8217;s Digest to stop sending you stuff?

Disk space is cheap these days, so knock yourself out. But denormalising is only part of the story for data warehouses. Much bigger performance gains are derived from precomputed rolled-up values: monthly totals, that sort of thing. It&#8217;s _always_ about reducing the working set.

&nbsp;

> Source: http://stackoverflow.com/questions/173726/when-and-why-are-database-joins-expensive
