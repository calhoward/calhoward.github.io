---
title: Backing up an openMAINT Database with pg_dump
date: 2022-04-30 10:48:00 +/-TTTT
---

## Introduction

*Note: At the time of writing, the most recent version of openMAINT is 3.4 and it is recommended to install PostgreSQL 10, so this guide will assume your database is also versioned for PostgreSQL 10.*

The information in your openMAINT instance is stored in a PostgreSQL database. It can be simply backed up in the form of a .DUMP file with a single command. 

Follow this guide for an explanation of how pg_dump works in the context of openMAINT's database.

## Backing up the database

We will use pg_dump to create a .DUMP file of our PostgreSQL database. Modify the following command and use it to create your database backup:

```bash
 pg_dump -Fc -h 127.0.0.1 --cluster 10/main -U postgres <your_database_name> -f openMAINT_backup_MM_DD_YYYY.dump
 ```

The -Fc flag specifies that the database has a custom format.
The -h flag specifies the host, 127.0.0.1 in the case of a standard openMAINT install
The --cluster flag specifies version "10/main". This is necessary to avoid version mismatching when restoring to an instance of openMAINT running on top of PostgreSQL 10.
The -U flag is our user, "postgres", in the case of a standard openMAINT install
The -f flag specifies our filename
