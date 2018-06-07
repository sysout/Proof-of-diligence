# Cracking the coding interview
## Chapter 14 Database
### Denormalized v.s. Normalized Database
Normalized database are designed to minimize redundancy, while denormalized database are designed to optimize read time. Denormalization is commonly used to create highly scalable systems.
- Write a SQL query to get a list of tenants who are renting more than one apartment

### Chapter 15 Threads and Locks
In Java, two ways of implement threads
- java.lang.Runnable
- java.lang.Thread


# Other tech interview questions
- [Write-back vs Write-Through](https://stackoverflow.com/questions/27087912/write-back-vs-write-through)
  * write back has better performance. It's complex, but more sophisticated. most memory in modern cpu use this policy
  * The benefit of write-through to main memory is that it simplifies the design of the computer system. With write-through
  * Write through is also more popular for smaller caches that use no-write-allocate
