# kotlin-bootcamp-notes

My personal Kotlin Learning Notes from Udacity Course | Kotlin Bootcamp for Programmers by Google

## Kotlin Basics

### Operators

```kotlin
// Returns integer
println(1 + 1) // Prints: 2
println(53 - 3) // Prints: 50
println(50 / 10) // Prints: 5
println(1 / 2) // Prints: 0
println(6 * 50) // Prints: 300

// Returns double
println(1.0 / 2.0) // Prints: 0.5
println(1.0 / 2) // Prints: 0.5
println(2 / 2.0) // Prints: 1.0

// Kotlin let's you overwrite the basic operators
// You can call methods on variables
val fish = 2
println(fish.times(6)) // Prints: 12
println(fish.div(10.0)) // Prints: 0.2
println(fish.plus(3)) // Prints: 5
println(fish.minus(3)) // Prints: -1
```

### Practice time: Operators

```kotlin
/*f you start with 2 fish, and they breed twice, producing 71 offspring the first time,
and 233 offspring the second time, and then 13 fish are swallowed by a hungry moray eel,
how many fish do you have left? How many aquariums do you need if you can put 30 fish per aquarium?*/

var fish = ((2 + 71 + 233) - 13)
 fish
>>> res10: kotlin.Int = 293

fish = fish / 30
 fish
>>> res11: kotlin.Int = 9
```

### Boxing

```kotlin
val boxed: Number = 1
     ^       ^      ^
    name    type  value

val num: Int = 2
val dob: Double = 2.0

// Same works
Integer x = 42;
Integer y = Integer.valueOf(42);

// There are two types of variables in Kotlin
// Changeable & Unchangeable
//   var           val

// With "val" you can assign value only once
val aquarium = 1
aquarium = 2 // -> ERROR! cannot be reassigned

// You can assign vals;
val str = "string"
val numInt = 1
val numDouble = 1.0
val bool = false

// With "var" you can assign a value, and then you can change it
var fish = 2
fish = 50
// Type is inferred meaning that compiler can figure out the type from the context
// Even so the type is inferred, it becomes fixed at compile time,
// So you cannot change a type of a varible in kotlin once its type has been determined.
fish = "Bubbles" // ERROR

// We can use variables in operations and there is no punctuation at the end
var str = 8
var a = 5
a + str
print(a + str)

// Number types won't implicitly convert to other types, so you can't assign
// A short value to a long variable or a byte to an int
val b: Byte = 1
val i: Int = b // ERROR Type Mismatch

// But you can always assign them by casting like this;
val i: Int = b.toInt()

// Kotlin supports underscores in numbers
val oneMillion = 1_000_000
val socialSecurityNumber = 999_99_9999L
val hexBytes = 0xFF_EC_DE_5E
val bytes = 0b11010010_01101001_10010100_100100010

// You can speficy long constants in a format that makes sense to you
// The type is inferred by Kotlin
```

### Practice time: Variables

```kotlin
/*1. Create a String variable rainbowColor, set its color value, then change it.
2. Create a variable blackColor whose value cannot be changed once assigned. Try changing it anyway.*/

1.
var rainbowColor = "Blue"
rainbowColor
>>> res16: kotlin.String = Blue

rainbowColor = "Black"
 rainbowColor
>>> res17: kotlin.String = Black

2.
val blackColor = "Black"
 blackColor
>>> res18: kotlin.String = Black

blackColor = "Red"
 blackColor
>>> error: val cannot be reassigned
```

### Nullability

```kotlin
// Kotlin helps avoid null pointer exceptions
// When you declare a variables type expicitly, by default its value cannot be null
var rocks: Int = null

// Use the question mark operator to indicate that a variable can be null
var rocks: Int? = null

// Whe you have complex data types such as a list,
var lotsOfFish: List<String?> = listOf(null, null)

// You can allow for the list to be null, but if it is not null its elements cannot be null
var evenMoreFish: List<String>? = null
var definitelyFish: List<String?>? = null

// Or you can allow both the list or the elements to be null
definitelyFish = listOf(null, null)


var rainbowColor: String? = null
var greenColor: String? = null
var blueColor = null
```

### Practice time: Nullability

```kotlin
/*Try to set rainbowColor to null. Declare two variables, greenColor and blueColor.
Use two different ways of setting them to null.*/

var rainbowColor: String? = null
var greenColor: String? = null
var blueColor = null
```

### Practice time: Nullability/Lists

```kotlin
/*1. Create a list with two elements that are null; do it in two different ways.
2. Next, create a list where the list is null.*/

1.
var lotsOfFish: List<Int?> = listOf(null, null)
lotsOfFish
>>> res6: kotlin.collections.List<kotlin.Int?> = [null, null]

var lotsOfFish = listOf(null, null)
lostOfFish
>>> res2: kotlin.collections.List<kotlin.Nothing?> = [null, null]

2.
var lotsOfFishTwo: List<Int>? = null
lotsOfFishTwo
>>> res0: kotlin.collections.List<kotlin.Int>? = null
```

### Elvis operator " ?: "

```kotlin
/*If the expression to the left of ?: is not null, the elvis operator returns it,
otherwise it returns the expression to the right.
Note that the right-hand side expression is evaluated only if the left-hand side is null.*/

val l: Int = if (b != null) b.length else -1
val l = b?.length ?: -1

/*If the expression to the left of ?: is not null, the elvis operator returns it,
otherwise it returns the expression to the right.
Note that the right-hand side expression is evaluated only if the left-hand side is null.*/

var b: String? = null
var l = b?.length ?: -1
print(l)

/*Since throw and return are expressions in Kotlin, they can also be used on the right hand side of the elvis operator.
This can be very handy, for example, for checking function arguments:
*/
fun foo(node: Node): String? {
    val parent = node.getParent() ?: return null
    val name = node.getName() ?: throw IllegalArgumentException("name expected")
    // ...
}
```

### " ! " Operator & Not-null Assertion Operator " !! "

```kotlin
/*This is unsafe nullable type (T?) conversion to a non-nullable type (T),
!// will throw NullPointerException if the value is null.*/

/*The third option is for NPE-lovers:
the not-null assertion operator (!!) converts any value to a non-null type and throws an exception if the value is null.
You can write b!!, and this will return a non-null value of b (for example,
a String in our example) or throw an NPE if b is null:*/

	val l = b!!.length

/*Thus, if you want an NPE, you can have it, but you have to ask for it explicitly,
and it does not appear out of the blue.*/
```

### Practice time: Null Checks

```kotlin
/*Create a nullable integer variable called nullTest,
and set it to null. Use a null-check that increases the value by one if it's not null,
otherwise returns 0, and prints the result.*/

var nullTest: Int? = null
nullTest?.dec() ?: 0
>>> res4: kotlin.Int = 0

var nullTest: Int? = 5
nullTest?.inc() ?: 0
>>> res13: kotlin.Int = 6
```

### Strings

```kotlin
"Hello Fish" // Hello Fish

// Concatenation
"hello" + "fish" // hello fish

val numberOfFish = 5
val numberOfPlants = 12

"I have $numberOfFish fish and $numberOfPlants plants" // I have 5 fish and 12 plants

// Here two numbers get added first then the result will be printed
"I have ${numberOfFish + numberOfPlants} fish and plants" // I have 17 fish and plants

val fish = "fish"
val plant = "plant"
println(fish == plant) // false
println(fish != plant) // true

val A = "A"
val B = "Z"
println(A < B) // true
println(A > B) // false
```

### If-Else Statements

```kotlin
val numberOfFish = 50
val numberOfPlants = 23
if (numberOfFish > numberOfPlants) {
    println("Good Ratio!")
} else {
    println("unhealthy ratio")
}
```

### Ranges

```kotlin
val fish = 50
// .. -> inclusively 1 <= fish <= 50
if (fish in 1..50) {
    println(fish.toString() + " is in the range 1 <= fish <= 50!")
}
// until -> exclusively 1 <= fish < 50
if (fish in 1 until 50) {
    println(fish)
} else {
    println(fish.toString() + " is not in the range 1 <= fish < 50!")
}
```

### When

```kotlin
// "when" is the way of switching in Kotlin
val numberOfFish = 50
when (numberOfFish) {
    0 -> println("Empty tank")
    50 -> println("Full tank")
    else -> println("Perfect!")
} // Output: Full tank

val numberOfFish = 50
when (numberOfFish) {
    in 1..50 -> println("Full tank")
} // Output: Full tank

// Create a string which would contain a * symbol n times.
val str: String = "*".repeat(100)
```

### Practice time: Strings

```kotlin
/*1. Create three String variables for `trout`, `haddock`, and `snapper`.
2. Use a String template to print whether you do or don't like to eat these kinds of fish.*/

var trout: String = "trout"
var haddock: String = "haddock"
var snapper: String = "snapper"

println("I like to eat $trout and $haddock, but not $snapper")
>>> I like to eat trout and haddock, but not snapper

/*`when` statements in Kotlin are like `case` or `switch` statements in other languages.

Create a `when` statement with three comparisons:

- If the length of the `fishName` is 0, print an error message.
- If the length is in the range of 3...12, print "Good fish name".
- If it's anything else, print "OK fish name".*/

var fishName: String = "Trout"

when (fishName.length) {
     0 -> println("Error!")
     in 3..12 -> println("Good fish name")
     else -> println("OK fish name")
 }
>>> Good fish name
```

### Array and Loops

```kotlin
// If val variable value is a reference, then you cannot assign it a different reference later

val myList = mutableListOf("tuna", "salmon", "shark");
myList = mutableListOf("Koi"); // ERROR// Cannot be re-assigned

// If you're referencing something that's not immutable(değişmez), it can still change

// val only applies to the reference and it doesn't make the object it points to immutable

// Here we cannot assign a different list in myList
but we can manipulate the elemets of the list such as removing/adding an element

val myList = mutableListOf("tuna", "salmon", "shark");
myList.remove("shark") // True
myList.add("fish") // True
```

### For/While Loop Examples

```kotlin
val myList = mutableListOf("tuna", "salmon", "shark");
// Loop through an array
for (item in myList) {
    print(item + " ") // tuna salmon shark
}
// Loop through an array With index
for (index in myList.indices) {
    print(myList[index] + " ") // tuna salmon shark
}
for ((index, value) in myList.withIndex()) {
    println("the element at $index is $value") // the element at 0 is tuna...
}
//    for (i in array.indices) {
//        println(array[i])
//    }
// To iterate over a range of numbers, use a range expression
for (i in 1..5) {
//        print(i.toString() + " ") /// Alternate
    print("$i ") // 1 2 3 4 5
}
for (c in 'a'..'z') {
    print("$c ") // a b c d e f g h i j k l m n o p q r s t u v w x y z
}
for (c in 'z' downTo 'a') {
    print("$c ") // z y x w v u t s r q p o n m l k j i h g f e d c b a
}
for (c in 10 downTo 0) {
    print("$c ") // 10 9 8 7 6 5 4 3 2 1 0
}
for (c in 10 downTo 0 step 2) {
    print("$c ") // 10 8 6 4 2 0
}
for (c in 1..10 step 2) {
    print("$c ") // 1 3 5 7 9
}
```

### While loop

```kotlin
var x = 5
while (x > 0) {
    print("$x ") // 5 4 3 2 1
    x--
}
// Arrays work pretty much as you'd expect with some cool additions
// Good practice is to prefer using "lists" over "arrays"
everywhere except for performance critical parts of your code

// It is pretty similar to Java
val l1 = listOf("a")
val l2 = listOf("a")
var x = (l1 == l2) // => true

val a1 = arrayOf("a")
val a2 = arrayOf("a")
var y = (a1 == a2) // => false
```

### listOf & MutableListOf

```kotlin
/*
List: READ-ONLY
MutableList: READ/WRITE
You can modify a MutableList: change, remove, add... its elements.
In a List you can only read them.

// Prefer MutableList over Array
// The major difference from usage side is that;
-> Arrays have a fixed size (like int [] in C++)
-> MutableList can adjust their size dynamically (like vectors in C++, a.k.a dynamic arrays)
-> Moreover Array is MUTABLE whereas List is not. (List is read-only, Array is not)

// Difference between ArrayList<String>() and mutableListOf<String>() in Kotlin
-> The only difference between the two is communicating your intent :)
-> So, there is no difference, just a convenience method.*/

// Create an array
val school = arrayOf("fish", "tuna", "salmon")

// Create Typed array (e.g. integers)
val numbers = intArrayOf(1, 2, 3)

// Error, Type Mismatch
val test = intArrayOf(2, "foo")

// But you can mix types in Untyped arrays
val mixedArray = arrayOf("fish", 2, 's', 0.0)
for (element in mixedArray) {
    println(element) // fish 2 s 0.0
    // print(element.toString() + " ")
}

// This does not prints the all elements, it prints the array address instead
val mixedArray = arrayOf("fish", 2, 's', 0.0)
print(mixedArray) // [Ljava.lang.Object;@66d3c617

// You can use joinToString or forEach, forEachIndexed, Arrays.toString( array )
val mixedArray = arrayOf("fish", 2, 's', 0.0)
print(mixedArray.joinToString()) // fish, 2, s, 0.0
mixedArray.forEach { print("$it ") } // fish, 2, s, 0.0
mixedArray.forEachIndexed { index, any -> println("$any at $index") }
// fish at 0 ...
println(Arrays.toString(mixedArray)) // [fish, 2, s, 0.0]
```

### Nesting Arrays

```kotlin
// You can nest arrays
val swarm = listOf(5, 12)
// When you put an array within an array, you have an array of arrays
// !Not a flattened array of the contents of the two
val bigSwarm = arrayOf(swarm, arrayOf("A", "B", "C"))
println(Arrays.toString(bigSwarm))
println(bigSwarm.asList()) // Shorter Printing Array Alternative
// Prints:  [[5, 12], [Ljava.lang.String;@452b3a41]

// You can nest arrays
val intList = listOf(5, 12)
val stringList = mutableListOf("A", "B", "C")
// OR this -> val stringList = listOf("A", "B", "C")
// When you put "LİST or MUTABLELIST" within an array, you have an array of arrays with merged content but "ARRAYS" are passed by ref as shown above example
val bigList = listOf(intList, stringList)
println(bigList.joinToString())
// [5, 12], [A, B, C]
```

### Create Typed Lists, Mutablelists and Arrays

```kotlin
val intList = listOf<Int>(5, 12)
val stringList = listOf<String>("1","2","3","4")

// Mutablelists
val intList = mutableListOf<Int>(5, 12)
val stringList = mutableListOf<String>("1","2","3","4")

// Array
val intList = arrayOf<Int>(5, 12)
val stringList = arrayOf<String>("1","2","3","4")

// Sized array
var table = Array<String>(words.size) {""}
val literals = arrayOf<String>("January", "February", "March")

// Create 2D Array
val grid = Array(rows) { Array(cols) { Any() } }

//String[] in Java equivalent Array<String> in Kotlin
//eg.
var array1 : Array<String?> = emptyArray()
var array2: Array<String?> = arrayOfNulls(4)
var array3: Array<String> = arrayOf("Mashroom", "Kitkat", "Oreo", "Lolipop")

val num = arrayOf(1, 2, 3, 4)   //implicit type declaration
val num = arrayOf<Int>(1, 2, 3) //explicit type declaration

// Or you can also create typed lists, arrays, mutable lists
val intList = listOf<Int>(5, 12)
val listSample: List<Int> = listOf(1,2,3)
val mutableListSample: MutableList<Int> = mutableListOf(1,2,3)
val stringList = listOf<String>("1","2","3","4")
val stringListSample: List<String> = listOf<String>("1","2","3","4")
var initList = List(4){"s"} // {"s", "s", "s", "s"}

// Arrays
val intArray = arrayOf(1,2,3)
val intArray2: Array<Int> = arrayOf(1,2,3)
val intArray3 = intArrayOf(1,2,3)
val charArray = charArrayOf('a', 'b', 'c')
val intArray = arrayOf(1,2,3)
val intArray2: Array<Int> = arrayOf(1,2,3)
val intArray3 = intArrayOf(1,2,3)
val charArray = charArrayOf('a', 'b', 'c')
val stringArray = arrayOf("genesis", "melo")
val stringArray2: Array<String> = arrayOf("genesis", "melo")
val stringOrNulls = arrayOfNulls<String>(5) // returns Array<String?>
val stringOrNulls2: Array<String?> = arrayOf("", null)// returns Array<String?>
var emptyStringArray: Array<String> = emptyArray()
var emptyStringArray2: Array<String> = arrayOf()
var sizedEmptyArray = Array(4){"s"} // {"s", "s", "s", "s"}

// In this line, we create an array from a range of numbers.
val nums3 = IntArray(5, { i -> i * 2 + 3})
// This line creates an array with IntArray. It takes the number of elements and a factory function as parameters.
// This is the output.
/*
[1, 2, 3, 4, 5]
[3, 4, 5, 6, 7, 8, 9, 10, 11, 12]
[3, 5, 7, 9, 11]
*/

// You can read this as initialize an array of 5 elements, assign each item to its index times two
val array = Array(5) {it * 2}
// OR -> val array = List(5) {it * 2}
println(array.joinToString()) // 0, 2, 4, 6, 8

val list = List(5){ it.times(2) } // Creates List: [0, 2, 4, 6, 8]

val array = Array<Int>(5) { e -> if (e % 2 == 0) 2 else 1 }
println(array.asList())

val array = List<String>(5) { e -> if (e % 2 == 0) "even" else "$e" }
println(array.joinToString()) // Prints: even, 1, even, 3, even

// Loop array with indices
val swarm = listOf(5, 12, 15, 17)

for (i in 0 until swarm.size) {
    print("$i ") // 0 1 2 3
}

for (i in 0..swarm.size - 1) {
    print("$i ") // 0 1 2 3
}

for (i in swarm.indices) {
    print("$i ") // 0 1 2 3
}

for (indexValuePair in swarm.withIndex()) {
    print("index: ${indexValuePair.index}, value: ${indexValuePair.value}\n")
} // Prints:  index: 0, value: 5
```

### Quiz: Array and Loops

```kotlin
// Read the code below, and then select the correct array initialization that will display the corresponding output.
val array = // initalize array here
val sizes = arrayOf("byte", "kilobyte", "megabyte", "gigabyte",
    "terabyte", "petabyte", "exabyte")
for ((i, value) in array.withIndex()) {
   println("1 ${sizes[i]} = ${value.toLong()} bytes")
}

// Output:
1 byte = 1 bytes
1 kilobyte = 1000 bytes
1 megabyte = 1000000 bytes
1 gigabyte = 1000000000 bytes
1 terabyte = 1000000000000 bytes
1 petabyte = 1000000000000000 bytes
1 exabyte = 1000000000000000000 bytes

// Answer / Solution Code:
val array = Array(7){ 1000.0.pow(it) }
// Notice how we had to use the double value 1000.0 and not just 1000 to be able to use the "pow" function.
```

### Practice time: Array and Loops

Looping over arrays and lists is a fundamental technique that has a lot of flexibility in Kotlin. Let's practice.

`Array<T>`is mutable (it can be changed through any reference to it),

but `List<T>`doesn't have modifying methods

Arrays have fixed size and cannot expand or shrink retaining identity (you need to copy an array to resize it). As to the lists, `MutableList<T>`
 has `add`and `remove`functions, so that it can increase and reduce its size.

```kotlin
//Basic example

/*1. Create an integer array of numbers called `numbers`, from 11 to 15.
2. Create an empty mutable list for Strings.
3. Write a `for` loop that loops over the array and adds the string representation of each number to the list.*/

val numbers = IntArray(5){it + 11}
val mutableList : MutableList<String> = arrayListOf()
for ((i, value) in numbers.withIndex()) {
     mutableList.add(i, value.toString())
 }

mutableList
>>> res7: kotlin.collections.MutableList<kotlin.String>
					= [11, 12, 13, 14, 15]


//Challenge example

/*How can you use a `for` loop to create (a list of) the numbers between 0 and 100 that are divisible by 7?*/

val nums = IntArray(101){it}
val newLst: MutableList<Int> = arrayListOf()
for ((i, value) in nums.withIndex()) {
     if (value % 7 == 0) {
         newLst.add(value)
     }
 }
newLst
>>> res21: kotlin.collections.MutableList<kotlin.Int>
				= [0, 7, 14, 21, 28, 35, 42, 49, 56, 63, 70, 77, 84, 91, 98]

// Solution Code
var list3 : MutableList<Int> = mutableListOf()
for (i in 0..100 step 7) list3.add(i)
print(list3)
[0, 7, 14, 21, 28, 35, 42, 49, 56, 63, 70, 77, 84, 91, 98]

```

## Functions

###

```kotlin


```

## Classes

###

```kotlin


```

## Kotlin Essentials: Beyond the Basics

###

```kotlin


```

## Functional Manipulation

###

```kotlin


```
