---
author: Arnab
title: Pluggable Storage Engines of MySQL
excerpt:
layout: post
category: tech
tags:
  - databases
  - mysql
post_format: [ ]
---
Came across a very nice feature of MySQL – thought to share it with you.
Well actually, it is one of the main reasons why MySQL is succeeding – so not really an obscure nice feature at all!!! In fact, very well known and appreciated by the community…

(MySQL is a GNU Public licensed Database – and FREEly available. You can go for enterprise option and get support too. Recently Sun bought MySQL!!!)

Anyway, coming back to the point – it has a concept of a Pluggable Storages Engine. So when you write the DDL for creating the table, you specify which engine should be used to store the table – like so:

CREATE TABLE IF NOT EXISTS MY\_FUNKLY\_TABLE (
MY\_FUNKY\_ID CHAR(4) NOT NULL,
FUNKY_DESCRIPTION VARCHAR(10) NOT NULL,
IS\_IT\_REALLY_FUNKY ENUM(‘Y’, ‘N’) DEFAULT ‘Y’,

PRIMARY KEY (MY\_FUNKY\_ID)
) ENGINE=InnoDB CHARACTER SET utf8 COLLATE utf8_bin
;

So what’s the deal? Well you can specify whether you want the table to be stored in memory or actually in storage; you can kinda tell what it’s used for – Archiving? Have BDB (BerkleyDB) type features!!! Different types of engines are MyISAM, InnoDB, BDB, Memory, Merge, Archive, Federated, Cluster/NDB, Other – read more about each type in the links given below…

Moreover, you can implement any engine (MyOwnEngine) and plug that into MySQL – cool ha?

The best part is a story I heard from someone recently – a table was taking up around 1.5 GB – after converting it to Archive engine, it became 47MB!!!
A 32 times reduction in space!!!

Yeah yeah yeah – I agree it depends on what sorta data was there in the first place – but still 32 times (3200% to put it differently ![:-)][1] ) is a lot man!!!

Read more at:
[Wikipedia][2]
[An article about this from MySQL][3]

 [1]: http://www.arnab-deka.com/posts/wp-includes/images/smilies/icon_smile.gif
 [2]: http://en.wikipedia.org/wiki/MySQL
 [3]: http://dev.mysql.com/tech-resources/articles/mysql_5.0_psea1.html