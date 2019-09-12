# Functional Query Language

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
- etc...

## Queries

FQL evaluates lazily. You build up your queries and then `collect` when you're ready to pull back results.

Intermediate queries can be saved to variables and composed. Depending on the target backend the compiler can make lots of optimizations to reuse intermediate results and boost performance over hand tuned SQL or other logic.

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

These signatures allow for a system capable of expressing any possible transformation of data we'd care to imagine

FQL is intended to be infinitely extensible making it easy to create any new function matching one of the above signatures

```
f(*Collections, *args) -> Collection

join, zip, union
```

```
f(Collection, *args) -> Collection

group, ungroup, filter, sort

group(collection, 'col1')
map(collection, )
```

```
f(Collection, *args) -> Record

min, max, avg
```

```
f(Record, *args) -> Collection
```

```
f(Record, *args) -> Atom

get
```

```
[
  [
    [1, 1],
    [1, 2],
  ],
  [
    [2, 3],
    [2, 4],
  ]
]

sum(0)
[
  [2, 3],
  [5, 6],
]

sum(1)
[
  [2, 3],
  [4, 7],
]

sum(2)
[
  [3, 4],
  [3, 6],
]

sum(get(0,1)) ...?

```

- Should we just use broadcasting type functions? And we just ignore NULLs
- No **map** function would be needed then...
- Should we allow slicing? What about regex match of columns and indices

```
col, row, group?

zip(
  get('x', 'y', 'z'),
  name('a', sum('x', 'y', 'z')),
  name('b', div('x', 'y')),
  name('c', avg('x', 'y', 'z')),
)
``` 

