I am using Java for all the exercises.

# Java
## Array
```Java
char ca[] = {'a', 'b', 'c'};
char[] ca = {'a', 'b', 'c'};
```

## String
### StringBuilder
### [String Formatting](https://dzone.com/articles/java-string-format-examples)
```java
String output = String.format("%s = %d", "joe", 35);
System.out.printf("My name is: %s%n", "joe");
```
## Compare
```Java
List<Integer> list = Arrays.asList(1, 3);
list.sort(null); // element implemented Comparable interface don't need additional Comparator
Collections.sort(list);

/**
 * Definition of Interval:
 * public class Interval {
 *     int start, end;
 *     Interval(int start, int end) {
 *         this.start = start;
 *         this.end = end;
 *     }
 */
intervals.sort(Comparator.comparing(i -> i.start));
intervals.sort(Comparator.comparingInt(i -> i.start));
intervals.sort((a,b) -> Integer.compare(a.start, b.start));
intervals.sort((a,b) -> Integer.valueOf(a.start).compareTo(Integer.valueOf(b.start)));
intervals.sort((a,b) -> new Integer(a.start).compareTo(new Integer(b.start)));
intervals.sort((a,b) -> a.start - b.start);

```
### [Comparator.thenComparing](https://stackoverflow.com/questions/24436871/very-confused-by-java-8-comparator-type-inference)
- Use an exact method reference (one with no overloads), like Song::getTitle. This then gives enough type information to infer the type variables for the comparing() call, and therefore give it a type, and therefore continue down the chain.
- Use an explicit lambda (as you did in your example).
- Provide a type witness for the comparing() call: Comparator.<Song, String>comparing(...).
- Provide an explicit target type with a cast, by casting the receiver expression to Comparator<Song>.
```java
intervals.sort(Comparator.comparing(a -> a.start).thenComparing(a -> a.end)); // compile error!!!!
intervals.sort(Comparator.comparing((Interval a) -> a.start).thenComparing(a -> a.end));
intervals.sort(Comparator.<Interval, Integer> comparing(a -> a.start).thenComparing(a -> a.end));
Collections.sort(intervals, Comparator.comparing((Interval a) -> a.start).thenComparing(a -> a.end));
```

### List
Print list: `intervals.forEach((intervals a) -> System.out.printf("[%d, %d], ", a.start, a.end));`

## 144. Interleaving Positive and Negative Numbers


## 390. [Find Peak Element II](http://www.lintcode.com/en/problem/find-peak-element-ii/)
[MIT lecture](http://courses.csail.mit.edu/6.006/spring11/lectures/lec02.pdf)
[
[0,0,0,0,0,0],
[0,1,12,3,4,0],
[0,5,11,7,12,0],
[0,9,10,9,13,0],
[0,13,9,15,16,0],
[0,0,0,0,0,0]
]


# 7


## 404. Subarray Sum II
