## installation
```
brew cask install caskroom/versions/java8
```

## Enum

## Operators
- [:: (double colon) Method References in Java 8](https://docs.oracle.com/javase/tutorial/java/javaOO/methodreferences.html)
  * There are four kinds of method references
    + ContainingClass::staticMethodName
    + containingObject::instanceMethodName
    + ContainingType::methodName
      ```
      String[] stringArray = { "Barbara", "James", "Mary", "John",
          "Patricia", "Robert", "Michael", "Linda" };
      Arrays.sort(stringArray, String::compareToIgnoreCase);
      // The method reference would invoke the method a.compareToIgnoreCase(b)
      ```
    + ClassName::new



## [precedence](https://introcs.cs.princeton.edu/java/11precedence/)
![precedence](images/2018/01/precedence.png)

## Bitwise
- operators
  * `|` Bitwise OR
  * `&` Bitwise AND
  * `~` Bitwise Complement
  * `^` Bitwise XOR
  * `<<` Left Shift
  * `>>` Right Shift
  * `>>>` Unsigned Right Shift
- exercise
  * https://www.hackerrank.com/contests/hackerrank-hiring-contest/challenges/winning-lottery-ticket/

## Object
- .equals() v.s. .hashCode()
  * objects which are .equals() MUST have the same .hashCode()
  * objects produce same .hashCode() don't have to be equal

## ArrayDeque
- ArrayDeque will throw NullPointerException if you offer(null)

## Java 8 LocalTime
```java
import java.time.*;

private static void dateTimes() {
  // dates, e.g. 2014-02-18

  // the current date
  LocalDate currentDate = LocalDate.now();

  // 2014-02-10
  LocalDate tenthFeb2014 = LocalDate.of(2014, Month.FEBRUARY, 10);

  // months values start at 1 (2014-08-01)
  LocalDate firstAug2014 = LocalDate.of(2014, 8, 1);

  // the 65th day of 2010 (2010-03-06)
  LocalDate sixtyFifthDayOf2010 = LocalDate.ofYearDay(2010, 65);


  // times, e.g. 19:12:30.733

  LocalTime currentTime = LocalTime.now(); // current time
  LocalTime midday = LocalTime.of(12, 0); // 12:00
  LocalTime afterMidday = LocalTime.of(13, 30, 15); // 13:30:15

  // 12345th second of day (03:25:45)
  LocalTime fromSecondsOfDay = LocalTime.ofSecondOfDay(12345);

  // dates with times, e.g. 2014-02-18T19:08:37.950
  LocalDateTime currentDateTime = LocalDateTime.now();

  // 2014-10-02 12:30
  LocalDateTime secondAug2014 = LocalDateTime.of(2014, 10, 2, 12, 30);

  // 2014-12-24 12:00
  LocalDateTime christmas2014 = LocalDateTime.of(2014, Month.DECEMBER, 24, 12, 0);


  // By default LocalDate and LocalTime will use the system clock in the default time zone
  // We can change this by providing a timezone or an alternative clock implementation

  // current (local) time in Los Angeles
  LocalTime currentTimeInLosAngeles = LocalTime.now(ZoneId.of("America/Los_Angeles"));

  // current time in UTC time zone
  LocalTime nowInUtc = LocalTime.now(Clock.systemUTC());


  System.out.println("date/time creation: currentDate: " + currentDate);
  System.out.println("date/time creation: tenthFeb2014: " + tenthFeb2014);
  System.out.println("date/time creation: firstAug2014: " + firstAug2014);
  System.out.println("date/time creation: sixtyFifthDayOf2010: " + sixtyFifthDayOf2010);
  System.out.println("date/time creation: currentTime: " + currentTime);
  System.out.println("date/time creation: midday: " + midday);
  System.out.println("date/time creation: afterMidday: " + afterMidday);
  System.out.println("date/time creation: fromSecondsOfDay: " + fromSecondsOfDay);
  System.out.println("date/time creation: currentTimeInLosAngeles: " + currentTimeInLosAngeles);
  System.out.println("date/time creation: currentDateTime: " + currentDateTime);
  System.out.println("date/time creation: secondAug2014: " + secondAug2014);
  System.out.println("date/time creation: christmas2014: " + christmas2014);
}
```

## Array
- `Arrays.copyOf(T[] original, int newLength)`
- `Arrays.copyOfRange(T[] original, int from, int to)`
- `Arrays.fill(int[] a, int val)`
```Java
char ca[] = {'a', 'b', 'c'};
char[] ca = {'a', 'b', 'c'};
```
- convert list integer array int
  * `list.stream().mapToInt(Integer::intValue).toArray();`
    + intValue is not static

## String
```
str.split("\\s+"); // split by space
str.split("\\."); // split by dot, for example 255.255.255.255
```
### StringBuilder
### [String Formatting](https://dzone.com/articles/java-string-format-examples)
```java
String output = String.format("%s = %d", "joe", 35);
System.out.printf("My name is: %s%n", "joe");
// reverse a String
new StringBuilder(s).reverse().toString();
// join a list of String
List<String> list = Arrays.asList("foo", "bar", "baz");
String.join("->", list);
```
## Sort & Compare
```Java
List<Integer> list = Arrays.asList(1, 3);
list.sort(null); // element implemented Comparable interface don't need additional Comparator
Collections.sort(list);
Arrays.sort(data, Collections.reverseOrder()); // only works for boxed types


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

## Collections
- Collections.singleton(obj)
- Collections.singletonList(obj)
- Collections.singletonMap(key, value)
- Collections.removeIf(Predicate<? super E> filter)
  ```java
  public static void main(String[] args) {
    Map<String, String> map = new HashMap<String, String>();
    map.put("1", "One");
    map.put("2", "Two");
    map.put("3", null);
    map.put("4", "Four");
    map.put("5", null);
    System.out.println(map);
    map.values().removeIf(Objects::isNull);
    System.out.println(map);
  }
  ```


### List
- Print list: `intervals.forEach((intervals a) -> System.out.printf("[%d, %d], ", a.start, a.end));`
- `List<Integer> arr=new ArrayList<Integer>(Collections.nCopies(10, 0));`

### Map
```java
Function<Integer, Set<Integer>> setGen = k -> new HashSet<>();
Map<Integer, Set<Integer>> relationship = new HashMap<>();
relationship.computeIfAbsent(from_user_id, setGen).add(to_user_id);
```

### TreeMap

## java.util.concurrent

### ThreadLocalRandom

```java
import java.util.concurrent.ThreadLocalRandom;

/**
 * @author ashraf
 *
 */
public class ThreadLocalRandomTest {

	public static void main(String[] args) {

		System.out.println("Random int:");
		// Returns a pseudorandom, uniformly distributed integer value between 0
		// (inclusive) and 10000 (exclusive)
		System.out.println(ThreadLocalRandom.current().nextInt(10000));

		// Returns a pseudorandom, uniformly distributed int value between 5000
		// (inclusive) and 10000 (exclusive)
		System.out.println(ThreadLocalRandom.current().nextInt(5000, 10000));

		System.out.println("Random long:");
		// Returns a pseudorandom, uniformly distributed long value between 0
		// (inclusive) and 10000 (exclusive)
		System.out.println(ThreadLocalRandom.current().nextLong(10000));

		// Returns a pseudorandom, uniformly distributed long value between 5000
		// (inclusive) and 10000 (exclusive)
		System.out.println(ThreadLocalRandom.current().nextLong(5000, 10000));

		System.out.println("Random double:");
		// Returns a pseudorandom, uniformly distributed long value between 0
		// (inclusive) and 10000 (exclusive)
		System.out.println(ThreadLocalRandom.current().nextDouble(10000));

		// Returns a pseudorandom, uniformly distributed long value between 5000
		// (inclusive) and 10000 (exclusive)
		System.out.println(ThreadLocalRandom.current().nextDouble(5000, 10000));

	}

}
```
