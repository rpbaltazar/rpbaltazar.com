---
author: rpbaltazar
categories:
- Software development
- Terminal
date: "2016-11-18T17:27:45Z"
guid: http://balazar.net/random/?p=187
id: 187
tags:
- backup
- Database
- heroku
- postgresql
title: Restoring partial backups
url: /2016/11/18/restoring-partial-backups/
---
Recently a client called quite desperate stating they had deleted some data and couldn&#8217;t find a way to get it back.
In our system we use this gem called [paranoia](https://github.com/rubysherpas/paranoia) for most of our models. This gem, overrides the default behaviour of destroy and instead of actually destroying the record, it sets a timestamp in the deleted_at attribute. It also adds a scope to the queries to exclude the deleted records by default. If you really want to delete the record, or search over deleted records, you can obviously do that as well.

Anyway, the problem would&#8217;ve been solved just by using this if we had the model in question configured to use paranoia. Unfortunately we didn&#8217;t as the initial requirements stated quite clearly that there was close to zero problems if some of the records were deleted. (\*Lesson number one\*: close to zero problem is not zero problem and space is not a current limitation, so when in doubt, save the data).

With the impossibility of using this gem&#8217;s skills, we had to turn to our backups. Our backups run on a daily basis during the night when the workload is lower. But when this problem was reported, much more data had been created which made it impossible to fully restore the backup and go on to our lives.

This way, we came up with a neat solution that got us back on track without much effort:
1. Download the most recent backup and load it into one of our machines.
We have a script that fetches a list of the existing backups and allows us to choose whether to create a new one at the execution time or use the last one generated. Since the data in production had been lost already we used the most recent backup before the report.
2. Create an auxiliary table that would include a subset of the data we wanted to restore and export it to a sql script.
[This stackoverflow question](http://stackoverflow.com/questions/12815496/export-specific-rows-from-a-postgresql-table-as-insert-sql-script) turned out to be quite helpful for us to give us the idea of how to solve the problem.
3. Once the data was exported, we needed to edit the file to replace the auxiliary table name with the actual table name. Since the export does not write any drop statements but only inserts, it is safe to do so. So, we opened the file and replaced all the occurrences of the auxiliary table name by the actual table name. If the file is small enough you can easily open it in any text editor. If it turns out to be too big, try a scripting language to apply a sed in place.
4. Because our application is currently running on heroku machines, we still had to run this script in production to insert the missing data back. In order to do so, we used a simple bash command inspired from [here](http://stackoverflow.com/questions/15237366/how-to-execute-a-sql-script-on-heroku)
\`cat file.sql | heroku pg:psql &#8211;app app_name\`

cat outputs the contents of the file, and with | we redirect it to the command after it. In this case the command line interface with heroku.

This allowed us to insert the missing data successfully without messing with any other users data.
