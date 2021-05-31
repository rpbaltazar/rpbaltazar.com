---
author: rpbaltazar
categories:
- Curiosities
- Databases
- Software development
date: "2014-11-18T10:23:39Z"
guid: http://balazar.net/random/?p=97
id: 97
tags:
- Database
- migration
- populate
- rails
- rails 4
- ror
title: Rails populate after migrate
url: /2014/11/18/rails-populate-after-migrate/
videourl:
- ""
---
Even though it is not a good policy to use the migrations to populate your database, sometimes, when there are very static things it is almost safe to assume that you can do it.
Nevertheless, if you are planning to run the migrations in batch (e.g develop, develop, develop, publish into production) you might run into problems that you haven&#8217;t in your dev environment.

The issue this time was regarding a migration that tried to populate a column previously created in another migration. It was failing when accessing it.

The issue became a bit weirder when we tried to print the attr_accessible of the Model itself, as well as the actual db columns and both outputs were showing that the column was there and supposedely accessible through the model.

Re-running the migration, after failing solved the issue which led me to think that the problem was somehow related with the environment loaded. I decided to throw in a debugger into the migration file and take a look to what was actually loaded. Happens that the migration, even though running successfully, it doesn&#8217;t force a reload of the changed Models. Therefore, our newly added column was not yet available.

Happily, there is a solution for this very specific problem:
`Model.reset_column_information`

This will force the reload of the model, making the newly column available on the next call. The use of this is in this scenario is also referenced in the documentation as the most common use for this method:

&#8220;The most common usage pattern for this method is probably in a migration, when
just after creating a table you want to populate it with some default values&#8221;

Please refer to:
[http://apidock.com/rails/ActiveRecord/Base/reset\_column\_information/class](Please refer to: http://apidock.com/rails/ActiveRecord/Base/reset_column_information/class "Reset Colum Information")

See you
