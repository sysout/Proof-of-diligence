# Chapter 1
- 4S
  * scenario: ask feature / QPS / DAU / Interfaces
  * service: split / Application / Module
  * storage: Schema / Data / SQL / NoSQL / File System
  * Sharding / Optimization / Special Case
- News Feed
  * 关注和被关注
  * 每个人看到的内容是不同的
  * pull v.s. push model
    + pull
      - K 路归并
      - 适合于
        * 资源充足
        * 实时性要求高
        * 用户发帖很多
        * 单向好友关系，有明星问题
    + push
      - fanout
        * 明星用户一次fanout可能要好几个小时，不适合push model
      - Async task
        * message queue
        * producer consumer不匹配
      - rank follower by weight，让活跃用户优先获得推送
      - 适合于：
        * 资源少
        * 想偷懒，少写代码
        * 实时性要求不高
        * 用户发帖比较少
        * 双向好友关系，没有明星问题
  * Facebook, Twitter use pull
  * Instagram push + pull
- [Redis v.s. Memcached](https://www.infoworld.com/article/3063161/nosql/why-redis-beats-memcached-for-caching.html)
  * Memcached
    + Memcached is multithreaded, you can easily scale up by giving it more computational resources, but you will lose part or all of the cached data (depending on whether you use consistent hashing).
    + Least Recently Used algorithm
    + Memcached limits key names to 250 bytes and works with plain strings
  * Redis
    + Redis, which is mostly single-threaded, can scale horizontally via clustering without loss of data.
    + six different eviction policies
    + Redis supports both lazy and active eviction
    + Redis allows key names and values to be as large as 512MB each, and they are binary safe
    + Real-time statistics about every aspect of the database, the display of all commands being executed, the listing and managing of client connections
    + 6 Data types
      - Strings
      - Lists
      - Sets
      - Hashes
      - Sorted sets
      - Bitmaps and HyperLogLogs
