---
layout: default
title: Usage
parent: Command Line Interface
nav_order: 1
---

# Usage
{: .no_toc }

## Table of contents
{: .no_toc .text-delta }

1. TOC
{:toc}
----

The cinch CLI follows the [docopt](http://docopt.org/){:target="_default"} standard. Arguments and options
are used to pass configuration and data to cinch.

## Arguments

Arguments are the strings - separated by spaces - that come after the command name itself. They are
ordered, and can be optional or required. They cannot begin with a `-`.

### Required Arguments

The cinch CLI requires two arguments for every command, except `help` and `list`. The first argument must always
be `command` and the second `project`.

```bash
# cinch <command> <project>
cinch migrate sales
```

## Options

Options are not ordered and are always optional. Every option comes in two flavors: short and long. Short options
begin with a `-` followed by a single character. Long options begin with `--`. Options can have an optional
or required value, separated by a space or `=`.

### Global Options

Cinch contains a set of options that can be used with any command. 

| option                | description                                                                                                                                                                             |
|-----------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| -e, –environment=NAME | The environment to use when executing the command. The default is `environments.default` from the project file.                                                                         |
| -w, –working-dir=DIR  | The working directory to use when executing the command. Cinch searches for the [project](#required-arguments) directory within this DIR. The default is the current working directory. |
| -z, –time-zone=TZ     | Sets the time zone for logging and display. The default is the current **system** time zone (not PHP). This option has no effect on the target database.                                |
{: .col1-nowrap }