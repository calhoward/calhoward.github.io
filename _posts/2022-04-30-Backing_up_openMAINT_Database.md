---
title: Backing up an openMAINT Database with pg_dump
date: 2022-04-30 10:48:00 +/-TTTT
---
![]({{ site.baseurl }}/assets/img/2022/pexels-panumas-nikhomkhai-1148820_Cropped-min.jpg)
*Photo credit - [panumas nikhomkhai](https://www.pexels.com/@cookiecutter/)*
## Introduction

The information in your openMAINT instance is stored in a PostgreSQL database. It can be simply backed up in the form of a `.dump`  file with a single command. 

Follow this guide for an explanation of how `pg_dump`  works in the context of openMAINT's database.

>*Note: At the time of writing, the most recent version of openMAINT is [openMAINT 3.4](https://sourceforge.net/projects/openmaint/files/2.2/Core%20updates/openmaint-2.2-3.4/) and it is still recommended to use PostgreSQL version 10, so this guide will assume your database is also configured for use with PostgreSQL 10.*
{: .prompt-tip }
## Backing up the database

We will use `pg_dump`  to create a `.dump`  file of our PostgreSQL database. Modify the following command to fit your database and name the output file, and use it to create your database backup:

```bash
 pg_dump -Fc -h 127.0.0.1 --cluster 10/main -U postgres <your_database_name> -f openMAINT_backup_MM_DD_YYYY.dump
 ```

* The `-Fc`  flag specifies that the database has a custom format.
* The `-h`  flag specifies the host `127.0.0.1` in the case of a standard openMAINT installation
* The `--cluster`  flag specifies version `10/main`. This is necessary to avoid version mismatching when restoring to an instance of openMAINT running on top of PostgreSQL 10.
* The `-U`  flag is our user, `postgres`, in the case of a standard openMAINT installation
* The `-f`  flag specifies our `filename.dump`

That's it! You will find your output `.dump` file in whatever directory you ran the command in.

## Disclaimer

*I am not affiliated with Tecnoteca Srl., nor am I maintainer of either openMAINT, or CMDBuild. This guide is written in good faith, and in the spirit of contribution towards the Free Software Movement, for consumption as-is.*

*Some of the steps listed in this guide may break or cease to function as software packages are updated, deprecated, or become obseleted.*
## Refrences

[openMAINT on SourceForge](https://sourceforge.net/projects/openmaint/)

[openmaint.org](https://www.openmaint.org/)

[pg_dump on postgresql.org](https://www.postgresql.org/docs/current/app-pgdump.html)