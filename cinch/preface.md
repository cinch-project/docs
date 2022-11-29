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

* Support for SQL and PHP change scripts
* Easy to configure or integrate into PHP applications: a cinch
* 100% framework-agnostic
* Store history in a database other than the target
* Ability to source changes directly from version control
* Lifecycle hooks during a deployment: commit or revert
* CI/CD pipeline friendly
* Team-oriented change management

## Why Cinch?
Cinch was created to fill a gap in the PHP community around database change management (migration) tools. Most 
existing tools are bundled with frameworks and not designed for use outside their ecosystems. In addition, some of 
them do not support pure SQL change scripts. 

### Microservices
With the continued growth of microservices, heterogeneous software stacks are becoming more common: 
one service uses NodeJS while another Python, Java, or PHP. Most of these stacks have "their" way of 
doing things, including some kind of database change management system. 

Cinch is framework and language-agnostic. SQL change scripts allow it to be used across stacks: Python, Ruby, 
Java, etc. This means a team managing a set of microservices, utilizing different stacks, can now use
a single tool to manage their database changes.

### Multiple Data Sources
Most of these tools have a limited number of ways to source change scripts: typically just the filesystem.
This makes it difficult (or unnatural) to integrate into web applications or to deploy database
changes within a CI/CD pipeline. Cinch solves this by integrating with the most popular source control systems, 
allowing change scripts to be sourced from where they live.