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

In traditional SQL an agg function (like sum, min, max, avg) could operate over rows, columns, or columns of groups... I think that's it.

Numpy can go arbitarily deep with its grouping/dimensions, but do we want or need this? Even if our model allowed for that level of flexibility it'd likely never be used but for numerical applications, and dealing with axis is kinda confusing for most people

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

- Should we just use broadcasting type functions? And we just ignore NULLs
- No **map** function would be needed then...
- Should we allow slicing? What about regex match of columns and indices

```
col, row, group?

x, y, z = get(col, 'x', 'y', 'z')

zip(
  x, y, z,
  name('a', sum(x, y, z)),
  name('b', div(x, y)),
  name('c', avg(x, y, z)),
)


??? (x + y) / z
sum(row, x, y)
is div implied since it's always binary?

functions for rows and functions for columns?  I don't like that

g = group(col, 'x')


``` 

