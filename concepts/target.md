---
layout: default
title: Target
parent: Concepts
nav_order: 2
---

# Target
{: .no_toc }

## Table of contents
{: .no_toc .text-delta }

1. TOC
{:toc}
----

A cinch target represents the database where migrations (changes) are deployed. The target is the whole point behind
cinch: keeping your database schemas up to date and version controlled.

A target's configuration is part of an [environment]({% link concepts/environment.md %}), which is part of 
a [project]({% link concepts/project.md %}). Since a project can contain multiple environments, there can be multiple 
targets. There should only be one production target per project. **This is a very strong recommendation**, but cinch
itself will not, and cannot, stop you from doing otherwise.

All [supported databases](/index.html#database-support) can be a target, and all are referenced via
[Database DSNs](/concepts/dsn.html#database-parameters).

{: .important}
Cinch only makes changes to a target when instructed to do so: migration scripts or deployments updating 
[history](/concepts/history.html) tables. The latter only occurs when history is housed in the same database as the target.