---
layout: default
title: Data Source Name
parent: Concepts
nav_order: 1

required: <span style="color:#FF595E">*</span>
git_write_benefits: >-
    Write access allows creating the store.yml during create project, and adding a
    migration script stub. However, both can be created manually
required_token: "The `token` is a required value: either the parameter or environment variable must be set."
---

# Data Source Names (DSN)
{: .no_toc }

## Table of contents
{: .no_toc .text-delta }

1. TOC
{:toc}
----

Cinch uses data source names to represent connection strings for the [target]({% link concepts/target.md %}) database,
[history]({% link concepts/history.md %}) database and the [migration store]({% link concepts/migration-store.md %}).

## Format
The cinch DSN format is a space-separated list of parameters: `name=value` pairs ignoring spaces around the `=` sign.
Every DSN must contain a `driver` parameter.

```text
driver=pgsql host=localhost port = 333
```

If a value contains a space, it must be single quoted. Within single quotes, backslash `\` and single quote `'` must be
escaped: `'ex\\amp\'le'`. 

Values that are not quoted, are not escaped. A value is only considered quoted if it begins and ends with a single quote.

```text
name = 'value'      # value
name = 'value       # 'value
name = value'       # value'
name = '\'value\''  # 'value'
```

## Database Parameters
Database DSNs are used by the [target]({% link concepts/target.md %}) and [history]({% link concepts/history.md %}) databases.

### MySQL/MariaDB
Both MySQL and MariaDB use the same parameters and driver name. Internally, cinch detects which platform it is 
connected to and makes any necessary adjustments.

| name     | default    | description                  |
|----------|------------|------------------------------|
| driver   | mysql      | driver name, must be `mysql` |
| user     | root       | user name                    |
| password | (empty)    | user password                |
| host     | 127.0.0.1  | hostname, IPv4, IPv6         |
| port     | 3306       | TCP port number              |
| dbname   | (required) | database name                |
| charset  | utf8mb4    | client encoding              |

All [optional parameters](#optional-parameters) are supported.

### PostgreSQL
PostgreSQL includes two unique parameters: `sslmode` and `search_path`. You can learn mode about 
[sslmode here](https://www.postgresql.org/docs/current/libpq-connect.html#LIBPQ-PARAMKEYWORDS){:target="_blank"}.

| name        | default    | description                                                     |
|-------------|------------|-----------------------------------------------------------------|
| driver      | pgsql      | driver name, must be `pgsql`                                    |
| user        | postgres   | user name                                                       |
| password    | (empty)    | user password                                                   |
| host        | 127.0.0.1  | hostname, IPv4, IPv6                                            |
| port        | 5432       | TCP port number                                                 |
| dbname      | (required) | database name                                                   |
| charset     | UTF8       | client encoding                                                 |
| search_path | (empty)    | comma-separated list of schemas                                 |
| sslmode     | prefer     | can be: disable, allow, prefer, require, verify-ca, verify-full |

All [optional parameters](#optional-parameters) are supported.

### Azure DB/SQL Server
SQL Server based databases are treated the same. Client encoding is always UTF8, there is no `charset` parameter.

| name        | default    | description                                                     |
|-------------|------------|-----------------------------------------------------------------|
| driver      | mssql      | driver name, must be `mssql`                                    |
| user        | sa         | user name                                                       |
| password    | (empty)    | user password                                                   |
| host        | 127.0.0.1  | hostname, IPv4, IPv6                                            |
| port        | 1443       | TCP port number                                                 |
| dbname      | (required) | database name                                                   |

All [optional parameters](#optional-parameters) are supported.

### SQLite
SQLite does not require credentials or connection information, just the location of the database file.

| name   | default    | description                   |
|--------|------------|-------------------------------|
| driver | sqlite     | driver name, must be `sqlite` |
| dbname | (required) | path to database file         |

## Migration Store Parameters
There are four different types (drivers) of migration stores. All require `driver` and `store_dir` parameters.

The three Git stores, GitHub, GitLab, Azure DevOps, also require `branch` and `token`. It is highly recommended
that a dedicated repo, branch or `store_dir` be used for Git stores. 

### Filesystem
The filesystem store provides simplicity and is great for development. 

| name      | required | description                                                |
|-----------|----------|------------------------------------------------------------|
| driver    | yes      | driver name, must be `fs`                                  |
| store_dir | yes      | store root path: absolute or relative to project directory |

Relative paths: if the project directory is `/home/foo/projects/sales`, and store_dir is `my-store`, then the store_dir would
be `/home/foo/projects/sales/my-store`. The `store_dir` can be set to `.`.

### GitHub
The default for the `token` parameter is the `CINCH_GITHUB_TOKEN` environment variable. {{ page.required_token }}

| name      | required | description                                                                               |
|-----------|----------|-------------------------------------------------------------------------------------------|
| driver    | yes      | driver name, must be `github`                                                             |
| store_dir | yes      | relative path to the root of the repository                                               |
| owner     | yes      | user or organization name                                                                 |
| repo      | yes      | repository name                                                                           |
| branch    | yes      | branch name within repository                                                             |
| token     | yes      | [personal access token][github-pac]{:target="_blank"} with `repository` read/write access |

All [optional parameters](#optional-parameters) are supported.

[github-pac]: https://docs.github.com/en/authentication/keeping-your-account-and-data-secure/creating-a-personal-access-token

### GitLab
The default for the `token` parameter is the `CINCH_GITLAB_TOKEN` environment variable. {{ page.required_token }}

| name       | required | description                                                                   |
|------------|----------|-------------------------------------------------------------------------------|
| driver     | yes      | driver name, must be `gitlab`                                                 |
| store_dir  | yes      | relative path to the root of the repository                                   |
| project_id | yes      | located at the top of gitlab project page                                     |
| branch     | yes      | branch name within repository                                                 |
| token      | yes      | [personal access token][gitlab-pac]{:target="_blank"} with `api` scope access |
| host       | no       | on-premise installations, default is gitlab.com                               |
| port       | no       | on-premise installations, default is 443                                      |

The `token` can also be a [group][gitlab-gat]{:target="_blank"} or [project][gitlab-prat]{:target="_blank"} access token.

All [optional parameters](#optional-parameters) are supported.

[gitlab-pac]: https://docs.gitlab.com/ee/user/profile/personal_access_tokens.html
[gitlab-gat]: https://docs.gitlab.com/ee/user/group/settings/group_access_tokens.html
[gitlab-prat]: https://docs.gitlab.com/ee/user/project/settings/project_access_tokens.html

### Azure DevOps
The default for the `token` parameter is the `CINCH_AZURE_TOKEN` environment variable. {{ page.required_token }}

| name      | required | description                                                                        |
|-----------|----------|------------------------------------------------------------------------------------|
| driver    | yes      | driver name, must be `azure`                                                       |
| store_dir | yes      | relative path to the root of the repository                                        |
| org       | yes      | organization name                                                                  |
| project   | yes      | project name                                                                       |
| repo      | yes      | repository name                                                                    |
| branch    | yes      | branch name within repository                                                      |
| token     | yes      | [personal access token][azure-pac]{:target="_blank"} with `code` read/write access |

All [optional parameters](#optional-parameters) are supported.

[azure-pac]: https://learn.microsoft.com/en-us/azure/devops/organizations/accounts/use-personal-access-tokens-to-authenticate?view=azure-devops&tabs=Windows

## Optional Parameters

The below table lists the optional parameters for all data sources.

| name            | default | description                                |
|-----------------|---------|--------------------------------------------|
| connect_timeout | 10      | connect timeout in seconds                 |
| timeout         | 10000   | request/query timeout in milliseconds      |
| sslca           | (empty) | path to certificate authority              |
| sslcert         | (empty) | path to client certificate                 |
| sslkey          | (empty) | path to private key for client certificate |

{: .note }
These parameters are ignored when used with a Filesystem or SQLite driver: `driver=fs` or `driver=sqlite`.