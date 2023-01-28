---
layout: default
title: Project
parent: Concepts
nav_order: 3
---

# Project
{: .no_toc }

## Table of contents
{: .no_toc .text-delta }

1. TOC
{:toc}
----

A project represents a database instance, or set of schemas within an instance, to version control. It contains 
a [migration store](/concepts/migration-store.html), [environments](/concepts/environment.html) and some configuration values.

## Name
The project name is the unique identifier for a cinch installation. It can contain any valid UTF8 character, expect 
forward slash, and has a range of 1 - 128 characters.

## Description
The project's description provides an overview of a project. It can contain any valid UTF8 character and has a 
range of 1 - 255 characters.

## Time Zone
The project time zone is used for display purposes only -- not for databases. The time zone must be a valid 
IANA canonical time zone identifier: such as `America/New_York`, `Europe/Belfast`, `Asia/Tokyo`.

## Migration Store
A project must have a single [migration store](/concepts/migration-store.html). All configuration and migration scripts (deployed or not) must be
contained within this store. The project references this store using a [Store DSN](/concepts/dsn.html#migration-store-parameters).

### Multiple Stores
Cinch can be configured to support multiple stores, but not for the same project. For example: if a development machine 
uses a local filesystem store, but requires a GitHub store for production, then a different project or cinch 
installation must be used.


