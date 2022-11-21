---
layout: default
title: Data Source Names
parent: Concepts
grand_parent: Cinch
nav_order: 1
git_write_benefits: >- 
    Write access allows creating the changelog.yml, during create project, and adding a 
    change script stub. However, both can be created manually
---

# Data Source Names (DSN)
{: .no_toc }

## Table of contents
{: .no_toc .text-delta }

1. TOC
{:toc}
----

Cinch uses DSNs to represent connection strings for the filesystem, database and remote GIT repositories. The format
used by cinch is always a valid URI.

The URI format was chosen to represent a DSN for several reasons:
1. well-known and understood format
2. simplicity - all values can be represented in a single string
3. large library support - internally cinch uses `GuzzleHttp\Psr7\Uri`

## DSN Parameters
All DSNs support parameters, which are encoded within the URI query. The below table lists parameters available
to all data sources. These are all optional.

| name            | default | description                                |
|-----------------|---------|--------------------------------------------|
| connect_timeout | 10      | connect timeout in seconds                 |
| timeout         | 10000   | request/query timeout in milliseconds      |
| sslca           | empty   | path to certificate authority              |
| sslcert         | empty   | path to client certificate                 |
| sslkey          | empty   | path to private key for client certificate |


## Filesystem DSN
A filesystem DSN uses a `file` scheme. Where ever a filesystem URI is expected, an absolute or relative pathname
can be used in its place.

### Format
```bash
# relative
file://.              # same as .
file://reports/pdf    # same as reports/pdf
file:.                # omit authority - same as .

# absolute
file:///home/andrew   # same as /home/andrew
file:/home/andrew     # omit authority - same as /home/andrew
```

## MySQL DSN
The MySQL DSN uses a `mysql` scheme. The format is identical to [pgsql](#postgresql-dsn).

### Format
```bash
mysql://user:password@host:port/dbname?charset=name
```

### Defaults

| value    | default                                                     |
|----------|-------------------------------------------------------------|
| user     | root - supply password without user `mysql://:password@...` |
| password | empty, there is no default                                  |
| host     | 127.0.0.1 - must omit authority `mysql:dbname`              |
| port     | 3306                                                        |
| dbname   | this is a required value, no default                        |
| charset  | utf8mb4                                                     |

## PostgreSQL DSN
The PostgreSQL DSN uses a `pgsql` scheme. The format is identical to [mysql](#mysql-dsn).

### Format
```bash
pgsql://user:password@host:port/dbname?charset=name&sslmode=mode&search_path=a,b,c
```

### Defaults

| value       | default                                                                                                                                                                     |
|-------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| user        | postgres - supply password without user `pgsql://:password@...`                                                                                                             |
| password    | empty, there is no default                                                                                                                                                  |
| host        | 127.0.0.1 - must omit authority `pgsql:dbname`                                                                                                                              |
| port        | 5432                                                                                                                                                                        |
| dbname      | this is a required value, no default                                                                                                                                        |
| charset     | UTF8                                                                                                                                                                        |
| sslmode     | `verify-full` if other ssl parameters were provided, otherwise `prefer`: see [PostgreSQL Parameter Key Words][sslmode]{:target="_blank"} for a list of all possible values. |
| search_path | set by postgres                                                                                                                                                             |

## GitHub DSN
The GitHub DSN uses a `github` scheme. This is for use with the cinch Changelog. You must use a 
[personal access token][github-pac]{:target="_blank"} with at least repository read access. 

{: .highlight }
It is recommended to use GitHub's new fine-grained personal access tokens. However, "classic" tokens will also work.

Optionally, you can enable repository write access. {{ page.git_write_benefits }}.

### Format
```bash
github:owner/repo/changelog_dir?branch=branch&token=token
```

* authority `://` is not supported, GitHub always uses `api.github.com:443`
* `owner` is either GitHub username or organization <small>[required]</small>
* `repo` is the name of the GitHub repository <small>[required]</small>
* `changelog_dir` is the path from the root of `repo` to the changelog directory. If omitted, cinch uses 
the root of `repo` as the changelog directory.
* `branch` parameter is the branch to use within `repo` <small>[required]</small> 
* `token` parameter is the personal access token. If omitted, the `CINCH_GITHUB_TOKEN` environment variable must be set.

## GitLab DSN
The GitLab DSN uses a `gitlab` scheme. This is for use with the cinch Changelog. You must use a
[personal access token][gitlab-pac]{:target="_blank"}, [group access token][gitlab-gat]{:target="_blank"}, or 
[project access token][gitlab-prat]{:target="_blank"} with at least `read_api, read_repository` scopes.

Optionally, you can enable `api` scope. {{ page.git_write_benefits }}. If `api` scope is 
enabled, no other scopes are required.

### Format
```bash
# for gitlab.com (GitLab SaaS)
gitlab:project_id/changelog_dir?branch=branch&token=token

# on premise (self-managed) - same as above if host is gitlab.com
gitlab://host:port/project_id/changelog_dir?branch=branch&token=token
```

* `host` is required for self-managed GitLab. If omitted, `gitlab.com` is used
* `port` default is 443
* `project_id` is the GitLab project identifier, which can be found at the top of the project's main page <small>[required]</small>
* `changelog_dir` is the path from the root of project to the changelog directory. If omitted, cinch uses
  the root of project as the changelog directory.
* `branch` parameter is the branch to use within project <small>[required]</small>
* `token` parameter is the personal, group, or project access token. If omitted, the `CINCH_GITLAB_TOKEN` environment variable must be set.


## Azure DevOps DSN

{: .warning }
Supports Azure DevOps Services (cloud), not Azure DevOps Server (on-premise).

The Azure DevOps DSN uses a `azure` scheme. This is for use with the cinch Changelog. You must use a
[personal access token][azure-pac]{:target="_blank"} with at least `code read` access.

Optionally, you can enable `code write` access. {{ page.git_write_benefits }}.

### Format
```bash
azure:organization/project/repo/changelog_dir?branch=branch&token=token
```

* authority `://` is not supported, Azure always uses `dev.azure.com:443`
* `organization` is the Azure organization name <small>[required]</small>
* `project` is the name of the Azure project <small>[required]</small>
* `repo` is the name of the Azure repository <small>[required]</small>
* `changelog_dir` is the path from the root of `repo` to the changelog directory. If omitted, cinch uses
  the root of `repo` as the changelog directory.
* `branch` parameter is the branch to use within `repo` <small>[required]</small>
* `token` parameter is the personal access token. If omitted, the `CINCH_AZURE_TOKEN` environment variable must be set.

[github-pac]: https://docs.github.com/en/authentication/keeping-your-account-and-data-secure/creating-a-personal-access-token
[gitlab-pac]: https://docs.gitlab.com/ee/user/profile/personal_access_tokens.html
[gitlab-gat]: https://docs.gitlab.com/ee/user/group/settings/group_access_tokens.html
[gitlab-prat]: https://docs.gitlab.com/ee/user/project/settings/project_access_tokens.html
[azure-pac]: https://learn.microsoft.com/en-us/azure/devops/organizations/accounts/use-personal-access-tokens-to-authenticate?view=azure-devops&tabs=Windows
[sslmode]: https://www.postgresql.org/docs/current/libpq-connect.html#LIBPQ-PARAMKEYWORDS