# loqusdb [![Build Status][travis-image]][travis-url] 

Small tool to setup a local variant database.

Right now **locusdb** uses [mongodb][mongodb] as backend for 
storing variants but there should not be a huge difference to use another
database manager.

## Installation ##

`pip install loqusdb`

or

```
$git clone https://github.com/moonso/loqusdb
$cd loqusdb
$pip install --editable .
```

## Idea ##

We want to keep track of the variants that have been seen in affected individuals.
This is not a tool for solving the problem with frequencies.
It will basically count the number if times we have seen a variant in affected individuals.
Since we have a fairly large number of affected individuals we will be able to use this tool to ignore variants that have been seen many times.
We will also keep track of the variants that have been seen in a homozygous state in affected individuals. 

Variants are stored by providing a vcf file and a family file or a family id.

The tool will select one affected individual per family and insert counts for the variants of this individual.

When the variants are added:

- Either the variant exists, in this case we increase the number of observations with one
- Or this variant has not ben seen before, then the variant is added to database


## Command Line Interface ##

```
$ loqusdb
Usage: loqusdb [OPTIONS] COMMAND [ARGS]...

  loqusdb: manage a local variant count database.

Options:
  -db, --database TEXT   [default: loqusdb]
  -u, --username TEXT
  -p, --password TEXT
  -port, --port INTEGER  Specify the port where to look for the mongo
                         database.  [default: 27017]
  -h, --host TEXT        Specify the host where to look for the mongo
                         database.  [default: localhost]
  -b, --backend [mongo]  Specify what backend to use.  [default: mongo]
  -c, --conn_host TEXT   Used for testing.  [default: mongodb://]
  -l, --logfile PATH     Path to log file. If none logging is printed to
                         stderr.
  -v, --verbose
  --version              Show the version and exit.
  --help                 Show this message and exit.

Commands:
  delete  Delete the variants of a case
  load    Load the variants of a case The loading is...
  wipe    Wipe the entire db
```




[travis-url]: https://travis-ci.org/moonso/loqusdb?branch=master
[travis-image]: https://img.shields.io/travis/moonso/loqusdb/master.svg?style=flat-square
[mongodb]: https://www.mongodb.org
