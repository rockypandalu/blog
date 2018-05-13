---
layout:     post
title:      "Oracle Database Architecture - PFILE, SPFILE"
subtitle:   "Yan Lu"
active: journal
image:
  feature: "pc001.jpg"
date:       2017-10-31
header-img: "img/postcover/pc001.jpg"
tags: []
categories: []
comments: false
---

Recently, I am working on an Oracle Database Conversion Project, which aims to convert a non-tenant database to a Pluggable Database (PDB) in a multitenant database.
One of its initial step is creating a Container Database (CDB) to hold the PDBs. And to achieve that, I need to understand the initial files required which including PFILE, SPFILE and Control File.

## PFILE
PFILE is a text-based file which stores the database setting related parameters. These parameters help the Oracle programs know how to start, including memory size, storage size, thread number etc. As a text-based file, PFILE can be directly edited by text editor when people want to change the database settings.
The data of PFILE can be find at <ORACLE_HOME>\database\init<SID>.ora (for windows machine) or <ORACLE_HOME>/dbs/init<SID>.ora for most of the other OS.

## SPFILE
SPFILE is a more recent and advanced way of storing database settings. It stores data as binary. People cannot modify SPFILE directly, it need to be modified via system command.
SPFILE uses similar file directory comparing to PFILE, but the file name is changed to spfile<SID>.ora.
SPFILE enables database to provide additional advantages over PFILE:
    * SPFILE can be backed-up by RMAN (Recover Manager), which make it easier for back-up and recovery
    * SPFILE is maintained by server, which will reduce the human mistakes
    * System command alter can persist setting change only if database is based on SPFILE

## SPFILE and PFILE conversion
When connect to database software as SYSDBA, SPFILE and PFILE can easily create each other by
CREATE SPFILE FROM PFILE;
CREATE PFILE FROM SPFILE;
