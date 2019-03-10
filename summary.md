# Summary.

## Redis. Основные понятия. Типы.

- Keys

- Strings
- Hashes
- List
- Sets
- Sorted Sets
- Bit arrays
- HyperLogLogs
- Streams
https://redis.io/topics/data-types-intro

- Binary-safe strings.
- Lists: collections of string elements sorted according to the order of insertion. They are basically linked lists.
- Sets: collections of unique, unsorted string elements.
- Sorted sets, similar to Sets but where every string element is associated to a floating number value, called score. The elements are always taken sorted by their score, so unlike Sets it is possible to retrieve a range of elements (for example you may ask: give me the top 10, or the bottom 10).
- Hashes, which are maps composed of fields associated with values. Both the field and the value are strings. This is very similar to Ruby or Python hashes. (как объекты только не может быть вложенных объектов)
- Bit arrays (or simply bitmaps): it is possible, using special commands, to handle String values like an array of bits: you can set and clear individual bits, count all the bits set to 1, find the first set or unset bit, and so forth.
- HyperLogLogs: this is a probabilistic data structure which is used in order to estimate the cardinality of a set. Don't be scared, it is simpler than it seems... See later in the HyperLogLog section of this tutorial.
- Streams: append-only collections of map-like entries that provide an abstract log data type. They are covered in depth in the Introduction to Redis Streams.


## Keys

Binary safe – any binary sequence can be used as a key. Key sensetive.
All keys in same space. Only conventions. But separate by namespaces only for single app. For several apps use different databases.
Commands:
KEYS - get keys; block all. 
SCAN - get keys; returns a slot reference for continue.
DEL - delete, blocking;
UNLINK - async, not blocking
EXISTS


## Strings

Text data, Integers, Float, binary data. Max 512Mb
Encoding verified before command execution.
Commands:
DECRBY (DECR) - decrement
INCRBY (INCR) - increment
TYPE - check type (return "string")
OBJECT ENCODING key - check encoding of a value (ex. return "int")


## Hashes

mini key value store within a key (only string to string). key with named fields.
single level
provides commands on those fields
inner structure dynamic schema free
extremely memory efficient and compact structures
this can be critical when you need to deal with hundreds of millions of keys and need low storage overhead and predictable performance 
Commands:
HSET
HEXISTS
HDEL
HSETNX - set if not exist
HINCRBY -
HINCRBYFLOAT - 

Field access:
HGET key field
HGETALL 
...

UseCases:
- Rate limit
- Session cache

 
## List

Ordered collection of Strings
Dublicates are allowed
Elements can be added and removed at Left or Right
Elements can be inserted relative to another
Used to implement Stacks and Queue
Commands:
PUSH, LPUSH, RPUSH
POP, LPOP, RPOP
LLEN - length of the list
LRANGE - subset of the list
LINDEX - returns the element by index
LINSERT - insert before or after element
LSET - set value at the specified index
LREM - remove

Use cases:
- Activity Stream
- Queue


## Sets

Unordered collection of unique strings
allows for set operations (difference, intersect, union)
Commands:
SADD
SMEMBERS (use in dev)
SSCAN
SISMEMBER - check if element exists
SREM - 
SPOP - remove and return a random element from the set


## Sorted sets

Ordered collection of unique strings
Floating point Score
Manipulation by value, position, score or lexigraphically
operations(Union, Intersection)
Commands:
ZADD
ZRANGE - 
ZREVRANGE - reverted
ZRANK key member - Returns the rank of member in the sorted set stored at key, with the scores ordered from low to high. The rank (or index) is 0-based, which means that the member with the lowest score has rank 0.
ZSCORE - provides the score of element
ZCOUNT - number of members between arranges scores
ZRANGE [WITHSCORES]
ZRANGEBYSCORE
ZRANGEBYLEX
ZREM