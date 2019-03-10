# Summary.

## Redis. Основные понятия. Типы.

Key
- Strings
- Hashes
- List
- Sets
- Sorted Sets
https://redis.io/topics/data-types-intro

- Binary-safe strings.
- Lists: collections of string elements sorted according to the order of insertion. They are basically linked lists.
- Sets: collections of unique, unsorted string elements.
- Sorted sets, similar to Sets but where every string element is associated to a floating number value, called score. The elements are always taken sorted by their score, so unlike Sets it is possible to retrieve a range of elements (for example you may ask: give me the top 10, or the bottom 10).
- Hashes, which are maps composed of fields associated with values. Both the field and the value are strings. This is very similar to Ruby or Python hashes. (как объекты только не может быть вложенных объектов)
Bit arrays (or simply bitmaps): it is possible, using special commands, to handle String values like an array of bits: you can set and clear individual bits, count all the bits set to 1, find the first set or unset bit, and so forth.
- HyperLogLogs: this is a probabilistic data structure which is used in order to estimate the cardinality of a set. Don't be scared, it is simpler than it seems... See later in the HyperLogLog section of this tutorial.
- Streams: append-only collections of map-like entries that provide an abstract log data type. They are covered in depth in the Introduction to Redis Streams.


## Keys

Binary safe – any binary sequence can be used as a key. Key sensetive.
All keys in same space. Only conventions. But separate by namespaces only for single app. For several apps use different databases.
Commands. 
KEYS - get keys; block all. 
SCAN - get keys; returns a slot reference for continue.
DEL - delete, blocking;
UNLINK - async, not blocking
EXISTS


## Strings

Text data, Integers, Float, binary data. Max 512Mb
Encoding verified before command execution.
Commands
DECRBY (DECR) - decrement
INCRBY (INCR) - increment
TYPE - check type (return "string")
OBJECT ENCODING key - check encoding of a value (ex. return "int")


## Hashes

mini key value store within a key (only string to string)
inner structure dynamic schema free
extremely memory efficient and compact structures