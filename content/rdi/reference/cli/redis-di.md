---
Title: redis-di
linkTitle: redis-di
description: A command line tool to manage and configure Redis Data Integration
weight: 10
alwaysopen: false
categories: ["redis-di"]
aliases: 
---

A command line tool to manage and configure Redis Data Integration

## Usage

```
Usage: redis-di [OPTIONS] COMMAND [ARGS]...
```

## Options
* `version`: 
  * Type: BOOL 
  * Default: `false`
  * Usage: `--version`

  Show the version and exit.


* `help`: 
  * Type: BOOL 
  * Default: `false`
  * Usage: `--help`

  Show this message and exit.



## CLI Help

```
Usage: redis-di [OPTIONS] COMMAND [ARGS]...

  A command line tool to manage & configure Redis Data Integration

Options:
  --version  Show the version and exit.
  --help     Show this message and exit.

Commands:
  add-context           Adds a new context
  configure             Configures the RDI Database so it is ready to...
  create                Creates the RDI Database instance
  delete                Deletes RDI database permanently
  delete-all-contexts   Deletes all contexts
  delete-context        Deletes a context
  deploy                Deploys the RDI configurations including target
  describe-job          Describes a transformation engine's job
  dump-support-package  Dumps RDI support package
  get-rejected          Returns all the stored rejected entries
  list-contexts         Lists all saved contexts
  list-jobs             Lists transformation engine's jobs
  reset                 Resets the pipeline into initial full sync mode
  scaffold              Generates configuration files for RDI and...
  set-context           Sets a context to be the active one
  set-secret            Writes a secret to Redis secret store
  start                 Starts the pipeline
  status                Displays the status of the pipeline end to end
  stop                  Stops the pipeline
  trace                 Starts a trace session for troubleshooting data...
  upgrade               Upgrades RDI Engine without losing data or downtime
```

