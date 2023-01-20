---
layout: default
title: Migration Store
parent: Concepts
nav_order: 6
---

# Migration Store
{: .no_toc }

## Table of contents
{: .no_toc .text-delta }

1. TOC
{:toc}
----

## Store Path

## Migrate Policy

### once

### always

#### always-before

#### always-after

### onchange

#### onchange-before

#### onchange-after

### Eligibility
Eligibility simply means a migration script is ready to be deployed. It must meet one of the following conditions:
1. `once` migration script that has never been deployed
2. `always-before` or `always-after` migration script: which "always" deploys
3. `onchange-before` or `onchange-after` migration script that has never been deployed or has changed since it was last deployed

