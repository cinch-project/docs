---
layout: default
title: Preface
parent: Cinch
nav_order: 1
---

# Preface
{: .no_toc }

## Table of contents
{: .no_toc .text-delta }

1. TOC
{:toc}
----

## Primary Goals

* Support for SQL and PHP migrations
* Easy to configure or integrate into PHP applications
* 100% framework-agnostic
* Store history in a database other than the target
* Ability to source migrations directly from version control
* Lifecycle hooks during a deployment: `migrate` or `rollback`
* CI/CD pipeline friendly
* Team-oriented management

## Why Cinch?
CInch began as a low-tech C program to perform database migrations, which was ported to PHP. There was a need for PHP 
migrations scripts, ruling out Python or Java tools, in addition to SQL migration support. Although other PHP tools 
exist, most are either bundled with a (unwanted) framework, far too simplistic or lack specific features. 

### Multiple Data Sources
Many existing tools have a limited number of ways to source migrations: typically just the filesystem.
This makes it difficult, and unnatural, to integrate into web applications or deploy within a pipeline. 
Cinch solves this by integrating with the most popular version control systems, allowing migrations to be sourced 
from where they (most commonly) live.

## Influences
Either through research or previous usage, many other tools influenced cinch: including but not limited to Flyway, 
Liquibase, Phinx, Doctrine and Laravel. Concepts and features from all these tools, can be found within cinch. 
However, cinch's approach differs from these tools.