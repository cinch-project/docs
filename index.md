---
title: Welcome
layout: home
nav_order: 1
---
Cinch is a database migration system written in PHP, designed to be extendable, configurable and
powerful, while maintaining simplicity. It's a cinch!
{: .fs-6 .fw-300 }

## Table of contents
{: .no_toc .text-delta }

1. TOC
{:toc}
----

## Why Cinch?
Cinch began as a simple C program to perform database migrations, which was ported to PHP to support 
PHP migration scripts. Although other PHP tools exist, most are either bundled with a (unwanted) framework, 
far too simplistic or lack specific features.

Many existing tools have a limited number of ways to source migrations: typically just the filesystem.
This makes it difficult, and unnatural, to integrate into web applications or deploy within a pipeline.
Cinch solves this by integrating with the most popular version control systems, allowing migrations to be sourced
from where they (most commonly) live.

## Primary Goals

* Support for SQL and PHP migrations
* Easy to configure or integrate into PHP applications
* 100% framework-agnostic
* Store history in a database other than the target
* Ability to source migrations directly from version control
* Lifecycle hooks during a deployment: `migrate` or `rollback`
* CI/CD pipeline friendly
* Team-oriented management

## Database Support
Cinch can be used to manage a number of databases. These databases can be used for the migration target or history.
Below is a full list including minimum versions. All versions newer than the minimum are supported.

| name                 | minimum version | release date     |
|----------------------|-----------------|------------------|
| MySQL                | 5.7             | October 21, 2015 |
| MariaDB              | 10.2            | April 18, 2016   |
| PostgreSQL           | 12.0            | October 3, 2019  |
| Microsoft SQL Server | 12.0            | March 18, 2014   |
| Azure SQL Database   | 12.0            | N/A              |
| SQLite               | 3.9             | October 10, 2016 |

{: .highlight}
MySQL, MariaDB, PostgreSQL, SQL Server tested with GCP, AWS RDS, Amazon Aurora and Azure. It is very likely Cinch will
work with other solutions based on these databases.

## Migration Store Support
A migration store (change source) houses migration scripts that have been or should be migrated to the target database. 
Cinch currently supports several popular version control systems.

| database              | description                                                                                     |
|-----------------------|-------------------------------------------------------------------------------------------------|
| Filesystem            | use the local filesystem, which is the default for the cinch CLI                                |
| GitHub                | use a branch within a GitHub repository                                                         |
| GitLab                | use a branch within a GitLab repository: v4 API, can be on-premise installation                 |
| Azure DevOps Services | use a branch within an Azure (cloud) repository: Azure DevOps Server (on-premise) not supported |

## Influences
Either through research or previous usage, many other tools influenced cinch: including, but not limited to, 
[Flyway](https://flywaydb.org/){:target="_default"}, 
[Liquibase](https://www.liquibase.org/){:target="_default"}, 
[Phinx](https://phinx.org/){:target="_default"}, 
[Doctrine](https://www.doctrine-project.org/projects/migrations.html){:target="_default"} and 
[Laravel](https://laravel.com/docs/9.x/migrations){:target="_default"}. 
Concepts and features from all these tools, can be found within cinch. However, cinch's approach to schema management 
differs from these tools.

{% comment %}
getting started/
* what is cinch
* brief history
* prerequisites
* installation
Concepts/
* Design diagram
* Terminology
* Data Source Name
  * 
* Project
  * Project name
  * Life Cycle Hooks 
    * Events
    * Handlers (exec or http)
    * Options
* History
  * Deployments
  * Changes
  * schema, table_prefix
  * schema version
  * schema owner (auto_create_schema)
* MigrationStore
  * Directory
  * Migration
    * MigrationId - default vs custom 
    * Script
      * sql scripts
      * php scripts (diff between executing local and remote)
    * Metadata: author, authored_at, description
    * Location
    * Commit Policies
  * Sorting
    * Sort Policy
Commands/
* create
  
{% endcomment %}
