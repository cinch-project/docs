---
layout: default
title: Migrate
parent: Workflows
nav_order: 1
---

# Migrate
{: .no_toc }

1. TOC
{:toc}
----

## Eligibility
Eligibility simply means a migration script can/should be migrated. It must meet one of the following conditions:
1. `once` migration script that has never been migrated
2. `always-before` or `always-after` migration script: which "always" deploys
3. `onchange-before` or `onchange-after` migration script that has never been migrated or has changed since it was last migrated

## Sorting