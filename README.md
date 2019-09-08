# FQL

Functional Query Language

A common set of functions for writing composable and reusable queries of data within any language

- c
- python
- ruby
- java
- clojure
- etc...

and targeting any backend

- mysql
- sqlite
- in memory hashes and lists
- hive

## Data Interfaces

There are exactly three data interfaces

1. Collections
   - Collections can nest arbitrarily many collections
   - Collections can be empty
2. Records
   - Records are always the last element in a tree of collections
3. Atoms
   - Atoms are the fundamental data types available in a language { string, float, int, etc... }
   - FQL specifies exactly what types it expects in an environment

## Functions

There are limited possible function signatures

```
f(Collection, *args) -> Collection
f(Collection, *args) -> Record
f(*Collections, *args) -> Collection
f(Record, *args) -> Collection
f(Record, *args) -> Atom
```

These signatures allow for a system capable of expressing any possible transformation of data we'd care to imagine.

FQL is intended to be infinitely extensible making it easy to create any new 


group, ungroup, map, paste, union,

min, max, avg,
