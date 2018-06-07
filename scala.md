## List of what I think I don't know, yet
- scala symbol 'abc
  * Lisp (which uses 'abcd like Scala), Ruby (:abcd), Erlang and Prolog (abcd; they are called atoms instead of symbols)
- type safe
  * https://www.tikalk.com/posts/2010/11/08/type-safe-builder-in-scala-using-type-constraints/


## Install
```
brew install scala
```
https://www.jetbrains.com/help/idea/run-debug-and-test-scala.html
- [Add jar file to Scala REPL](https://alvinalexander.com/scala/scala-how-add-jar-file-scala-repl-classpath-command-line)
  * `scala> :require myjar.jar`
  *

## Practices
- https://www.scala-exercises.org/
- [1. Two Sum](https://leetcode.com/problems/two-sum/description/)
  * [sample solution](https://discuss.leetcode.com/topic/107183/scala-solutions)

    ```scala
    import scala.collection.mutable

    object Solution {
        def twoSum(nums: Array[Int], target: Int): Array[Int] = {
            val map = mutable.Map[Int, Int]()
            for (assoc @ (v, i) <- nums.zipWithIndex)
                map get (target - v) match{
                    case Some(j) => return Array(i, j)
                    case None => map += assoc
                }
            throw new NoSuchElementException()
        }
    }
    ```
- [219. Contains Duplicate II](https://leetcode.com/problems/contains-duplicate-ii/description/)
  * [for comprehensions with Options](http://markhneedham.com/blog/2011/09/15/scala-for-comprehensions-with-options/)

    ```scala
    import scala.collection.mutable._;

    object Solution {
        def containsNearbyDuplicate(nums: Array[Int], k: Int): Boolean = {
            var map = Map[Int, Int]();
            for (a @ (v, i) <- nums.zipWithIndex){
                for (j <- map.get(v)) if (i - j <= k) return true
                map += a
            }
            return false
        }
    }
    ```

## Syntax
- [What do all of Scala's symbolic operators mean?](https://stackoverflow.com/questions/7888944/what-do-all-of-scalas-symbolic-operators-mean)
- [Scala methods: dots, spaces, and parentheses](https://alvinalexander.com/scala/scala-methods-dots-spaces-single-one-parameter)
  * if a Scala method **takes a single parameter**, like this `object.method(param)`, can be written as `object method param`
- [Using the Scala Option, Some, and None idiom](https://alvinalexander.com/scala/using-scala-option-some-none-idiom-function-java-null)

  ```scala
  def toInt(in: String): Option[Int] = {
      try {
          Some(Integer.parseInt(in.trim))
      } catch {
          case e: NumberFormatException => None
      }
  }
  toInt(someString) match {
      case Some(i) => println(i)
      case None => println("That didn't work.")
  }
  ```
- [@ operator](https://stackoverflow.com/questions/2359014/scala-operator)
- [zipWithIndex](https://alvinalexander.com/scala/how-to-use-zipwithindex-create-for-loop-counters-scala-cookbook)
- [CASE CLASSES](https://docs.scala-lang.org/tour/case-classes.html)
  * Case classes are compared by structure and not by reference
- Seq
  * Seq is a good generalization for sequences, so if you program to interfaces, you should use that. Note that there are actually three of them: **collection.Seq**, **collection.mutable.Seq** and **collection.immutable.Seq**, and it is the latter one that is the "default" imported into scope.
- [cast a Scala object from one type to another](https://alvinalexander.com/scala/how-to-cast-objects-class-instance-in-scala-asinstanceof)

  ```scala
  import javax.script._
  val engine = new ScriptEngineManager().getEngineByName("js")
  val ans = engine.eval("4*5").asInstanceOf[Int]
  ```
- [new & companion object's apply method](https://stackoverflow.com/questions/9727637/new-keyword-in-scala)
  * Use the new keyword when you want to refer to a class's own constructor
  * Omit new if you are referring to the companion object's apply method
  * Java classes rarely have companion objects with an apply method, so you must use new and the actual class's constructor
- [initialization](http://www.scala-lang.org/old/node/8566)
  * Array are zero initialized by JVM

  ```scala
  var b : Byte // error
  var b: Byte = 0
  var b: Byte = _
  ```
- [underscore](https://stackoverflow.com/questions/8000903/what-are-all-the-uses-of-an-underscore-in-scala)
- [Existential types in Scala](https://www.cakesolutions.net/teamblogs/existential-types-in-scala)
- Why this doesn't work?

  ```scala
  val customers = collection.mutable.Map(100 -> "Paul Smith",
    101 -> "Sally Smith")
  customers += (102, "Xiong") // error
  customers += (102 -> "Xiong") // OK!!!
  var a = (102, "Xiong")
  customers += a // OK!!!
  ```
### String
- [string comparison](https://alvinalexander.com/scala/how-to-test-string-equality-in-scala-cookbook)
  * In Scala, the == method defined in the AnyRef class first checks for null values, and then calls the equals method on the first object (i.e., this) to see if the two objects are equal. As a result, you also don’t have to check for null values when comparing strings

### Function, Function0 to Function22
- https://www.scala-lang.org/api/current/scala/Function0.html

### [reference equality](https://stackoverflow.com/questions/6835578/scala-reference-equality)

```scala
val x = new Obj
val y = x
x eq y // evaluates to true
x ne y // evaluates to false
```

### [Either, Left, and Right](https://alvinalexander.com/scala/scala-either-left-right-example-option-some-none-null)

### Implicit
[Keynote - What to Leave Implicit by Martin Odersky](https://www.youtube.com/watch?v=Oij5V7LQJsA)
[Scala - How to add new methods to existing classes](https://alvinalexander.com/scala/scala-how-to-add-new-methods-to-existing-classes)

## [Scala Advanced, Part 1 - The Scala Type System](https://www.udemy.com/scala-advanced-part-1-the-scala-type-system/learn/v4/overview)
```scala
import scala.annotation.implicitNotFound

@implicitNotFound("You need to define a CompareT for ${T}")
abstract class CompareT[T] {
  def isSmaller(i1: T, i2: T): Boolean
  def isLarger(i1: T, i2: T): Boolean
}

def genInsert[T: Ordering](item: T, rest: List[T]): List[T] = {
  val cmp = implicitly[Ordering[T]]
  rest match {
    case Nil => List(item)
    case head :: _ if cmp.lt(item, head) => item :: rest
    case head :: tail => head :: genInsert(item, tail)
  }
}

def genSort[T: Ordering](xs: List[T]): List[T] = xs match {
  case Nil => Nil
  case head :: tail => genInsert(head, genSort(tail))
}

val nums = List(1,4,3,2,6,5)

genSort(nums)

case class Person(first: String, age: Int)

object Person {
  implicit object PersonOrdering extends Ordering[Person] {
    override def compare(x: Person, y: Person): Int = x.age - y.age
  }
}

implicit object POrdering2 extends Ordering[Person] {
  override def compare(x: Person, y: Person) = 0
}

val people = List(
  Person("Fred", 25),
  Person("Sally", 22),
  Person("George", 53)
)

genSort(people)
```

## TODO
- Predef
  * classOf[T]
- trait xxxx extends scala.AnyRef
- scala.Unit
  * Unit is a subtype of scala.AnyVal. There is only one value of type Unit , () , and it is not represented by any object in the underlying runtime system. A method with return type Unit is analogous to a Java method which is declared void
- sealed abstract class
  * eg. sbt.SettingKey


## [Effective Scala](https://www.youtube.com/watch?v=TNSe0QzLx4E)
- use expressions, not statements
  * for expression: start with a set, return with a set

    ```scala
    def findPeopleIn(city: String, people: Seq(People)): Set[People] = {
      val found = new mutable.HashSet[People]
      for (person <- people){
        for (address <- person.addresses){
          if (address.city = city)
            found.put(person);
        }
      }
      return found
    }

    def findPeopleIn(city: String, people: Seq[People]) : Set[People] = {
      for {
        person <- people.toSet[People]
        address <- person.addresses
        if address.city == city
      } yield person
    }
    ```

- use REPL
- Array is mutable, Vector is immutable
  * `var addresses: Array[Address] = Array.empty`
  * `var addresses: Vector[Address] = Vector.empty`
- use **case class** and `copy` method
  * Automatic equality
  * Automatic hashcode
  * `case class Person(addresses: Vector[Address] = Vector.empty)`
  * `person = person.copy(addresses = newAddresses)`
- local mutability still ok

  ```scala
    def defaultData: Seq[Int] = {
      val a = new ArrayBuffer[Int]
      fillArray(a)
      a.toSeq
    }
  ```


## [LEARN SCALA IN ONE VIDEO](http://www.newthinktank.com/2015/08/learn-scala-one-video/)
- notes
  * var v.s. val
    + var can be changed
    + val is like const
    + interesting read: [Use of def, val, and var in scala](https://stackoverflow.com/questions/4437373/use-of-def-val-and-var-in-scala)
    + When Defining classes
      - both val and var create accessor

        ```scala
        class A(a: Int) {}
        // Doesn't compile (value a is not a member of)
        // (new A(1)).a

        class B(val b: Int) {}

        (new B(1)).b
        //> res0: Int = 1
        ```


  * Byte : -128 to 127
  * Char : unsigned max value 65535
  * Short : -32768 to 32767
  * val lgprime = BigInt("11111111111111111111111111111111111111111111111111111111") // scala.math.BigInt
  * val pi50 = BigInt("11111111111111111111111111111111111111111111111111111111") // scala.math.BigInt

```scala
// Install Scala on Mac : Install Java VM, Install Homebrew,
// In terminal type: brew install scala

// Scala is the perfect choice if you want to explore functional
// programming without disregarding OOP
// Scala runs on the JVM which provides a ton of libraries

// File ends with the scala extension

// How to import library functions
import scala.io.StdIn.{readLine,readInt}
import scala.math._
import scala.collection.mutable.ArrayBuffer
import java.io.PrintWriter
import scala.io.Source

/*
You can execute commands directly in the terminal
REPL : Read Evaluate Print Loop
Type scala in terminal to start and :q to quit

// Creates a variable of the correct type
10 + 3 * 5 / 2

// You only use semicolons in Scala if you have multiple statements per line

// You can use that variable in the code that follows
"Your answer " + res0

// Define your own variable
var myName = "Derek"

// Define your own constant variable
val myAge = 40

// You can define the type
val lastName: String = "Banas"
```
###  DATA TYPES
```scala
// All datatypes in Scala are objects and they include
// (Get the max value with MaxValue)
// Byte : -128 to 127
// Boolean : true or false
// Char : unsigned max value 65535
// Short : -32768 to 32767
// Int : -2147483648 to 2147483647
// Long : -9223372036854775808 to 9223372036854775807
// Float : -3.4028235E38 to 3.4028235E38
// Double : -1.7976931348623157E308 to 1.7976931348623157E308

// A Double will only hold precision up to 15 digits
val num13 = 1.999999999999999

// Create a BigInt
val lgPrime = BigInt("622288097498926496141095869268883999563096063592498055290461")
lgPrime + 1

 Create a BigDecimal
val pi50 = BigDecimal("3.14159265358979323846264338327950288419716939937510")
0.00000000000000000000000000000000000000000000000001 + pi50

var randInt = 100000

// See functions available by typing randInt. (Click Tab)
// randInt.asInstanceOf[Double] casts number to a double
// randInt.isInstanceOf[Int] checks if is of type Int
```
###  MATH
```scala
"5 + 4 = " + (5 + 4)
"5 - 4 = " + (5 - 4)
"5 * 4 = " + (5 * 4)
"5 / 4 = " + (5 / 4)
"5 % 4 = " + (5 % 4)

// Shorthand notation (No randInt++, or randInt--)
randInt += 1
"randInt += 1" + randInt

randInt -= 1
"randInt -= 1" + randInt

randInt *= 1
"randInt *= 1" + randInt

randInt /= 1
"randInt /= 1" + randInt

// Import the math library in the terminal import scala.math._

abs(-8)
cbrt(64) // Cube root a^3 = n (Find a)
ceil(5.45)
round(5.45)
floor(5.45)
exp(1) // Euler's number raised to the power
pow(2, 2) // 2^2
sqrt(pow(2,2) + pow(2,2))
hypot(2, 2) // sqrt(X^2 + y^2)
log10(1000) // = 3 (10 × 10 × 10 = 10^3)
log(2.7182818284590455) // Natural logarithm to the base e
min(5, 10)
max(5, 10)
(random * (11 - 1) + 1).toInt // Random number between 1 and 10
toRadians(90)
toDegrees(1.5707963267948966)

// acos, asin, atan, atan2, cos, cosh, sin, sinh, tan, tanh
```
###  CONDITIONALS
```scala
// if statements are like Java except they return a value like the
// ternary operator

// Conditional Operators : ==, !=, >, <, >=, <=
// Logical Operators : &&, ||, !

var age = 18

val canVote = if (age >= 18) "yes" else "no"

// You have to use { } in the REPL, but not otherwise
if ((age >= 5) && (age <= 6)) {
  println("Go to Kindergarten")
} else if ((age > 6) && (age <= 7)) {
  println("Go to Grade 1")
} else {
  println("Go to Grade " + (age - 5))
}

true || false
!(true)

*/

object ScalaTut {
  def main(args: Array[String]) {
```
###  LOOPING
- [There is no break or continue in Scala](https://stackoverflow.com/questions/2742719/how-do-i-break-out-of-a-loop-in-scala)

```scala
// To compile and run in the terminal
// 1. scalac ScalaTut.scala
// 2. scala ScalaTut

    var i = 0

    while (i <= 10) {
      println(i)
      i += 1
    }

    do {
      println(i)
      i += 1
    } while(i <= 20)

    for (i <- 1 to 10){
      println(i)
    }

    // until is often used to loop through strings or arrays
    val randLetters = "ABCDEFGHIJKLMNOPQRSTUVWXYZ"
    for (i <- 0 until randLetters.length){

      // Get the letter in the index of the String
      println(randLetters(i))
    }

    // Used to iterate through a list
    val aList = List(1,2,3,4,5)
    for(i <- aList){
      println("List Item " + i)
    }

    // Store even numbers in a list
    var evenList = for { i <- 1 to 20
      // You can put as many conditons here separated with semicolons
      // as you need
      if (i % 2) == 0
    } yield i

    println("Even List")
    for(i <- evenList)
      println(i)

    // This loop assigns a value to the 1st variable and it retains
    // that value until the 2nd finishes its cycle and then it iterates
    for (i <- 1 to 5; j <- 6 to 10){
      println("i: " + i)
      println("j: " + j)
    }

    // There is no break or continue in Scala
    def printPrimes() {

      val primeList = List(1,2,3,5,7,11)
      for (i <- primeList){

        // Works like break if you return from a function
        if(i == 11){
          return
        }

        // Works like continue
        if (i != 1){
          println(i)
        }

      }

    }

    printPrimes

```
###  INPUT / OUTPUT
```scala
var numberGuess = 0

do{
  print("Guess a number : ")

  // You can also use readInt, readDouble, readByte, readShort, readLong,
  //
  numberGuess = readLine.toInt

  } while(numberGuess != 15)

  printf("You guessed the secret number %d\n", 15)

  // You can use string interpolation
  val name = "Derek"
  val age = 39
  val weight = 175.5
  println(s"Hello $name")

  println(f"I am ${age + 1} and weigh $weight%.2f")

  // printf Style Format Specifiers
  // %c : Characters
  // %d : Integers
  // %f : Floating Point Numbers
  // %s : Strings
  printf("'%5d'\n",5) // Right justify

  printf("'%-5d Hi'\n",5) // Left justify

  printf("'%05d'\n",5) // Zero Fill

  printf("'%.5f'\n",3.14) // 5 decimal minimum & maximum

  printf("'%-5s'\n", "Hi") // Left Justify String

  // Special Characters : \n, \b, \\, \a
```
###  STRINGS
- [String Interpolator](https://docs.scala-lang.org/overviews/core/string-interpolation.html)
  * Prepending s to any string literal allows the usage of variables directly in the string.
  * Prepending f to any string literal allows the creation of simple formatted strings, similar to printf in other languages. When using the f interpolator, all variable references should be followed by a printf-style format string, like %d

```scala
var randSent = "I saw a dragon fly by"

// Get the 3rd index value
println("3rd Index : " + randSent(3))

// Get String length
println("String length " + randSent.length())

// Concatenate strings
println(randSent.concat(" and explode"))

// Compare strings for equality
println("Are strings equal " + "I saw a dragon".equals(randSent))

// Get index of a match
println("dragon starts at index ", randSent.indexOf("dragon"))

// Convert a string into an array
val randSentArray = randSent.toArray

for (v <- randSentArray)
  println(v)
```
###  FUNCTIONS
```scala
// def funcName (param1:dataType, param2:dataType) : returnType = {
//    function body
//    return valueToReturn
// }

// You can give parameters default values
def getSum( num1:Int = 1, num2:Int = 1) : Int = {
  return num1 + num2
}

println("5 + 4 = " + getSum(5,4))

// you can use named arguments
println("5 + 4 = " + getSum(num2=5, num1=4))

// A function that returns nothing (Procedure)
def sayHi() : Unit = {
  println("Hi how are you doing")
}

sayHi

// Receive variable number of arguments
def getSum2(args: Int*) : Int = {
  var sum : Int = 0
  for(num <- args){
    sum += num
  }
  sum
}

println("getSum2: " + getSum2(1,2,3,4,5))

// Recursion example calculating factorials
def factorial(num : BigInt) : BigInt = {
  if (num <= 1)
    1
  else
    num * factorial(num - 1)
}

// 1st: num = 4 * factorial(3) = 4 * 6 = 24
// 2nd: num = 3 * factorial(2) = 3 * 2 = 6
// 3rd: num = 2 * factorial(1) = 2 * 1 = 2

println("Factorial of 4 = " + factorial(4))
```
###  ARRAYS
- [array of specified length](https://stackoverflow.com/questions/9413507/scala-creating-a-type-parametrized-array-of-specified-length/9413750)
  * `val chars = Array[Char](256)`
    + creates one-element array (with code 256)
  * `val chars = Array.fill(256){0}`
    + where {0} is a function to produce elements
  * `val chars = new Array[Char](256)`
  * `Array.ofDim[Char](256)`

    ```
    import scala.reflect._
    classTag[Char].newArray(256)
    ```


```scala
// You'll use arrays when the size is fixed, or an ArrayBuffer for a
// variable size

// Create an array of Ints with a max size of 20
val favNums = new Array[Int](20)

// Create and initialize array in 1 line
val friends = Array("Bob", "Tom")

// Change the value in an array
friends(0) = "Sue"

println("Best Friend " + friends(0))

// Create an ArrayBuffer
val friends2 = ArrayBuffer[String]()

// Add an item to the 1st index
friends2.insert(0, "Phil")

// Add item to the next available slot
friends2 += "Mark"

// Add multiple values to the next available slot
friends2 ++= Array("Susy", "Paul")

// Add items starting at 2nd slot
friends2.insert(1, "Mike", "Sally", "Sam", "Mary", "Sue")

// Remove the 2nd element
friends2.remove(1)

// Remove 2 elements starting at the 2nd index
friends2.remove(1, 2)

// Cycle through and print ArrayList or Array
var friend : String = " "
for(friend <- friends2)
      println(friend)

// Add values to an array with a loop
for (j <- 0 to (favNums.length - 1)){
  favNums(j) = j
  println(favNums(j))
}

// Use yield to multiply all values times 2 and store in a new array
val favNumsTimes2 = for(num <- favNums) yield 2 * num

// Another way to print out values in array
favNumsTimes2.foreach(println)

// You can also store values that match a condition
var favNumsDiv4 = for(num <- favNums if num % 4 == 0) yield num

favNumsDiv4.foreach(println)

// Create a multidimensional array with Array.ofDim
var multTable = Array.ofDim[Int](10,10)

for(i <- 0 to 9){
  for(j <- 0 to 9){
    multTable(i)(j) = i * j
  }
}

for(i <- 0 to 9){
  for(j <- 0 to 9){
    printf("%d : %d = %d\n", i, j, multTable(i)(j))
  }
}

println("Sum : " + favNums.sum)

println("Min : " + favNums.min)

println("Max : " + favNums.max)

// Sort in desending order (Use < for assending)
val sortedNums = favNums.sortWith(_>_)

// Return an indexed sequence and convert it into a string with commas
println(sortedNums.deep.mkString(", "))
```
###  MAPS
```scala
// Maps are collections of key value pairs

// Create a Map that can't be changed (Immutable)
val employees = Map("Manager" -> "Bob Smith", "Secretary" -> "Sue Brown")

// Get value using the key after checking that it exists
if(employees.contains("Manager"))
  printf("Manager : %s\n", employees("Manager"))

// Create a Mutable map
val customers = collection.mutable.Map(100 -> "Paul Smith",
  101 -> "Sally Smith")

printf("Cust 1 : %s\n", customers(100))

// Change a value using the key
customers(100) = "Tom Marks"

// Add an item
customers(102) = "Megan Swift"

// Output a Map
for((k,v) <- customers)
  printf("%d : %s\n", k, v)
```
### [TUPLES](https://alvinalexander.com/scala/scala-tuple-examples-syntax)
- A tuple isn't actually a collection; it's a series of classes named Tuple2, Tuple3, etc., through Tuple22. You don't have to worry about that detail, other than knowing that you can have anywhere from two to twenty-two items in a tuple. (And in my opinion, if you have twenty-two miscellaneous items in a bag, you should probably re-think your design.)

```scala
scala> val stuff = (42, "fish")
stuff: (Int, java.lang.String) = (42,fish)

scala> stuff.getClass
res0: java.lang.Class[_ <: (Int, java.lang.String)] = class scala.Tuple2

// Tuples can hold values of many types, but they are immutable

var tupleMarge = (103, "Marge Simpson", 10.25)

printf("%s owes us $%.2f\n", tupleMarge._2, tupleMarge._3)

// Iterate through a tuple
tupleMarge.productIterator.foreach{ i => println(i)}

// Convert Tuple to String
println(tupleMarge.toString())
```
###  CLASSES
```scala
val rover = new Animal
rover.setName("Rover")
rover.setSound("Woof")
printf("%s says %s\n", rover.getName, rover.getSound)

val whiskers = new Animal("Whiskers", "Meow")
println(s"${whiskers.getName} with id ${whiskers.id} says ${whiskers.getSound}")

println(whiskers.toString)

val spike = new Dog("Spike", "Woof", "Grrrr")

spike.setName("Spike")
println(spike.toString)

val fang = new Wolf("Fang")
fang.moveSpeed = 36.0
println(fang.move)
```
###  TRAITS
```scala
val superman = new Superhero("Superman")
println(superman.fly)
println(superman.hitByBullet)
println(superman.ricochet(2500))
```
###  HIGHER ORDER FUNCTIONS
```scala
// Functions can be passed like any other variable
// You need the _ after the function to state you meant the function
val log10Func = log10 _

println(log10Func(1000))

// You can apply a function to all items of a list with map
List(1000.0,10000.0).map(log10Func).foreach(println)

// You can use an anonymous function with map as well
// Receives an Int x and multiplies every x by 50
List(1,2,3,4,5).map((x : Int) => x * 50).foreach(println)

// Filter will pass only those values that meet a condition
List(1,2,3,4,5,6).filter(_ % 2 == 0).foreach(println)

// Pass different functions to a function
def times3(num : Int) = num * 3
def times4(num : Int) = num * 4

// Define the function parameter type and return type
def multIt(func : (Int) => Double, num : Int ) = {
  func(num)
}

printf("3 * 100 = %.1f)\n", multIt(times3, 100))

// A closure is a function that depends on a variable declared outside
// of the function
val divisorVal = 5
val divisor5 = (num : Double) => num / divisorVal
println("5 / 5 = " + divisor5(5.0))
```
###  FILE I/O
```scala
// Use import java.io.PrintWriter to write to a file
val writer = new PrintWriter("test.txt")
writer.write("Just some random text\nSome more random text")
writer.close()

// Use import scala.io.Source to read from files
val textFromFile = Source.fromFile("test.txt", "UTF-8")

// Iterate through each line in the file and print
val lineIterator = textFromFile.getLines
for(line <- lineIterator){
  println(line)
}
textFromFile.close()

```
###  EXCEPTION HANDLING
```scala

def divideNums(num1 : Int, num2 : Int) = try
{
  (num1 / num2)
} catch {
    case ex: java.lang.ArithmeticException => "Can't divide by zero"
} finally {
  // Clean up after exception here
}

println("3 / 0 = " + divideNums(3,0))

} //  END OF MAIN
```
###  CLASSES
```scala
// Classes are used as blueprints to create objects
// Objects define the attributes (fields) and capabilities (methods) of an
// object

class Animal(var name : String, var sound : String) {
  this.setName(name)

  // Any code that follows the class name is executed each time an
  // object is created as part of the Primary Constructor

  // This function is defined in the Animal companion object below
  val id = Animal.newIdNum

  // You must initialize all fields
  // protected means the field can only be accessed directly by methods
  // defined in the class or by subclasses
  // private fields can't be accessed by subclasses of Animal
  // public fields can be accessed directly by anything

  // protected var name = "No Name"
  // protected var sound = "No Sound"

  // Getters and setters are used to protect data
  def getName() : String = name
  def getSound() : String = sound
  def setName(name : String){
    // Check if the String contains numbers and if so don't allow
    if(!(name.matches(".*\\d+.*")))

      // this allows us to refer to any object without knowing its name
      this.name = name
    else
      this.name = "No Name"
  }
  def setSound(sound : String) {
    this.sound = sound
  }

  // Subclasses can't call this constructor unlike with Java
  def this (name : String){

    // This calls the primary constructor defined on the class line
    this("No Name", "No Sound")
    this.setName(name)
  }

  def this (){
    // This calls the primary constructor defined on the class line
    this("No Name", "No Sound")
  }

  // You can override any other method
  override def toString() : String = {

    // How to format Strings
    return "%s with the id %d says %s".format(this.name, this.id, this.sound)
  }

}

// The companion object for a class is where you'd define static class
// variables and functions in Java
object Animal {
  private var idNumber = 0
  private def newIdNum = { idNumber += 1; idNumber }
}
```
###  INHERITANCE
```scala
// A class that inherits from another gains all its fields and methods
// A class declared final can't be extended
class Dog (name : String, sound : String, growl : String) extends
Animal(name, sound){

  def this (name : String, sound : String){
    this("No Name", sound, "No Growl")
    this.setName(name)
  }

  def this (name : String){
    this("No Name", "No Sound", "No Growl")
    this.setName(name)
  }

  def this (){
    this("No Name", "No Sound", "No Growl")
  }

  // You can override any other method
  override def toString() : String = {
    return "%s with the id %d says %s or %s".format(
      this.name, this.id, this.sound, this.growl)
  }
}
```
###  ABSTRACT CLASS
```scala
// An abstract class can't be instantiated. It is made up of both abstract
// and non-abstract methods and fields

abstract class Mammal(val name : String){
  // An abstract field has no initial value
  var moveSpeed : Double

  // An abstract method has no body
  def move : String

}

class Wolf(name : String) extends Mammal(name){
  // You don't use override when defining abstract fields
  var moveSpeed = 35.0;

  def move = "The wolf %s runs %.2f mph".format(this.name, this.moveSpeed)

}
```
###  TRAITS
```scala
// A trait is a like a Java interface in that a class can extend more then 1
// Unlike Java interfaces traits can provide concrete methods and fields
trait Flyable {
  def fly : String

}

trait Bulletproof {
  def hitByBullet : String

  // You can define concrete methods in traits
  def ricochet(startSpeed : Double) : String = {
    "The bullet ricochets at a speed of %.1f ft/sec".format(startSpeed * .75)
  }
}

// The first trait starts with extends and then with for each other
class Superhero(val name : String) extends Flyable with Bulletproof{
  def fly = "%s flys through the air".format(this.name)

  def hitByBullet = "The bullet bounces off of %s".format(this.name)
}

} //  End of object ScalaTut
```
