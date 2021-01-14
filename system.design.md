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


- [系统设计System Design]
  * https://soulmachine.gitbooks.io/system-design/content/cn/bigdata/heavy-hitters.html
  * red black tree https://www.jianshu.com/p/e136ec79235c
  * b+ tree etc https://www.jianshu.com/p/b597aa97c9de
  * https://www.educative.io/courses/grokking-the-system-design-interview
  * https://www.evernote.com/shard/s576/client/snv?noteGuid=7e58b450-1abe-43a8-bf82-fbf07f1db13c&noteKey=049802174415b418a2e65f75b744ab72&sn=https%3A%2F%2Fwww.evernote.com%2Fshard%2Fs576%2Fsh%2F7e58b450-1abe-43a8-bf82-fbf07f1db13c%2F049802174415b418a2e65f75b744ab72&title=Interview%2BPreparation
  * https://jobs.1point3acres.com/companies


- [面经](https://www.1point3acres.com/bbs/thread-541834-1-1.html)
  * Design an online reader system. (Amazon) Design an online chat room.
  * Design an online poker room. (Amazon) Design an online messenger.
  * Design an online reservation system (air ticket, restaurant/hotel reservation etc) (Amazon) Design a Hotel reservation system which will support the following functions.
  * Design a voice conferencing system (Amazon)
    + a) User will get a list of all different types of rooms.
    + b) User selects a room type & check the room availabilty between the specified dates.
    + c) User Makes Reservation.
  * [Discussed about "locking" the room availbilty or not in case if user wants to proceed with reservation] (Amazon)
  * Design a software for a restaurant (Amazon)

- `***`[Sharding Pinterest: How we scaled our MySQL fleet](https://medium.com/pinterest-engineering/sharding-pinterest-how-we-scaled-our-mysql-fleet-3f341e96ca6f)
  * We created a 64 bit ID that contains the shard ID, the type of the containing data, and where this data is in the table (local ID). The shard ID is 16 bits, type ID is 10 bits and local ID is 36 bits. The savvy additionology experts out there will notice that only adds to 62 bits. My past in compiler and chip design has taught me that reserve bits are worth their weight in gold. So we have two (set to zero).
  * ID = (shard ID << 46) | (type ID << 36) | (local ID<<0)
  ```SQL
  CREATE TABLE board_has_pins (
    board_id INT,
    pin_id INT,
    sequence INT,
    INDEX(board_id, pin_id, sequence)
  ) ENGINE=InnoDB;
  ```
  * ZooKeeper
  * Mod Shard
  ```
  shard = md5(“1.2.3.4") % 4096
  ```
