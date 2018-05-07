# <img src="https://upload.wikimedia.org/wikipedia/commons/b/b5/Kotlin-logo.png" style="width: 70px; margin: 0; background: none; border: none;"/>otlin



# Introduction
- Multi-Paradigm Programming Language
- Statically Typed
- JVM Targeted
- Developed By JetBrains



# Design Philosophy
#### A Better Language Than Java
- Concise and Expressive
- Null Safety, Immutability
- Composition Over Inheritance
- Fully Compatible and Interoperable with Java
- Smooth Learning Curve
- Gradual Migration
- Tooling Support



# Adoption
<p style="margin-top: 60px">
<img src="https://upload.wikimedia.org/wikipedia/commons/thumb/1/1a/JetBrains_Logo_2016.svg/220px-JetBrains_Logo_2016.svg.png" style="width: 96px; margin: 0 10px 0 0; background: none; border: none; box-shadow: none;"/>

<img src="https://www.shareicon.net/data/256x256/2016/07/08/117140_system_512x512.png" style="width: 96px; margin: 0 10px 0 0; background: none; border: none; box-shadow: none;"/>

<img src="https://sdtimes.com/wp-content/uploads/2016/05/0517.sdt-gradle.png" style="width: 96px; margin: 0 10px 0 0; background: #fff; border: none; box-shadow: none;"/>

<img src="http://www.iconsplace.com/download/red-pinterest-256.ico" style="width: 96px; margin: 0 10px 0 0; background: none; border: none; box-shadow: none;"/>

<img src="http://icons.iconarchive.com/icons/martz90/circle/256/evernote-icon.png" style="width: 96px; margin: 0 10px 0 0; background: none; border: none; box-shadow: none;"/>
</p>

<p>
<img src="https://www.shareicon.net/data/128x128/2016/11/03/849474_social_512x512.png" style="width: 96px; margin: 0 10px 0 0; background: #fff; border: none; box-shadow: none;"/>

<img src="https://www.corda.net/wp-content/uploads/2017/01/16-10-31_R3_Corda_Master-Logo-04-1-e1516308027926-1024x455.png" style="height: 96px; margin: 0 6px 0 0; background: none; border: none; box-shadow: none;"/>

<img src="https://i.pinimg.com/originals/b9/33/ab/b933abf000b8b16ddb6f2772f401630c.png" style="width: 96px; margin: 0 10px 0 0; background: none; border: none; box-shadow: none;"/>

<img src="http://softwaresforyou.live/wp-content/uploads/2018/04/Atlassian-icon-blue-onecolor@2x-1.png" style="width: 96px; margin: 0 10px 0 0; background: none; border: none; box-shadow: none;"/>
</p>



# Syntax



### Variables
##### Basic Syntax

```
fun foo(a: Int, b: Int): Int {
    val x: Int = 1

    val y = 2         // `Int` type is inferred

    val z: Int        // Type required when no initializer
    z = 3             // Immutable can only be initialized once

    var n: Int? = 100 // Nullable and mutable variable
    n = null          // Mutable can be re-assigned

    return a + b + x + y + z + (n ?: 0)
}
```


### Variables
##### Null Safety

```
// Kotlin distinguishes between nullable references
// and non-null references:

var a: String = "abc"
a = null // compilation error

var b: String? = "abc"
b = null // ok

val aLen = a.length // ok

val bLen = b.length // compilation error because b may be null
                    // you have to tell kotlin what to do if b = null
                    // instead of ignore it and throw NPE at runtime
```


### Variables
##### Null Safety

```
// Verbose way:
val bLen: Int
if (b != null) {
    bLen = b.length // smart cast happens here
} else {
    bLen = -1
}

// With safe calls
val bLen: Int? = b?.length // bLen is null if b is null

// Chained safe calls
alex?.department?.manager?.lastName

```


### Variables
##### Null Safety

```
// Don't like nullable bLen? Safe call + elvis operator
// Same as the verbose way above but more concise
val bLen: Int = b?.length ?: -1

// Just want to ignore the fact that b could be null
// non_null assertion => may throw NPE at runtime
val bLen = b!!.length
```


### Variables
##### Null Safety

With null safety:
- Still have to write logic that handles null values, especially for inputs that are passed in from outside, e.g. HTTP requests
- But it eliminates a lot of verbose null check logic within the module
- And it makes interfaces between components clearer: it explicitly states which arguments accept null values and which not



### Functions
##### Basic Syntax

```
fun foo(a: Int, b: Int): Int {
    val x: Int = 1

    val y = 2         // `Int` type is inferred

    val z: Int        // Type required when no initializer
    z = 3             // Immutable can only be initialized once

    var n: Int? = 100 // Nullable and mutable variable
    n = null          // Mutable can be re-assigned

    return a + b + x + y + z + (n ?: 0)
}
```


### Functions
##### Expression Body

```
// Function with an expression body and inferred return type
fun sum(a: Int, b: Int) = a + b

// Same as
fun sum(a: Int, b: Int): Int {
    return a + b
}
```


### Functions
##### Expression Body With If-Else

```
fun sumWithBoundary(left: Int, right: Int, min: Int, max: Int) =
    if (left + right < min) min
    else if (left + right > max) max
    else left + right

assertTrue(sumWithBoundary(33, 66, 0, 100) == 99)
assertTrue(sumWithBoundary(44, 66, 0, 100) == 100)
assertTrue(sumWithBoundary(33, -66, 0, 100) == 0)
```


### Functions
##### Expression Body With When

```
fun sumWithBoundary(left: Int, right: Int, min: Int, max: Int) =
    when {
        left + right < min -> min
        left + right > max -> max
        else -> left + right
    }

assertTrue(sumWithBoundary(33, 66, 0, 100) == 99)
assertTrue(sumWithBoundary(44, 66, 0, 100) == 100)
assertTrue(sumWithBoundary(33, -66, 0, 100) == 0)
```


### Functions
##### Default Argument

```
fun sumWithBoundary(
        left: Int, right: Int,
        min: Int = 0,   // Default argument
        max: Int = 100  // Default argument
) = when {
        left + right < min -> min
        left + right > max -> max
        else -> left + right
}

assertTrue(sumWithBoundary(33, 66) == 99)
assertTrue(sumWithBoundary(44, 66, 0, 50) == 50)
assertTrue(sumWithBoundary(33, -66, -100) == -33)
```


### Functions
##### Named Arguments

```
fun sumWithBoundary(
        left: Int, right: Int,
        min: Int = 0,   // Default argument
        max: Int = 100  // Default argument
) = when {
        left + right < min -> min
        left + right > max -> max
        else -> left + right
}

assertTrue(sumWithBoundary(left = 44, right = 66, max = 50) == 50)
// Also better readability
```


### Functions
##### No Meaningless Method Overloading

```
// This what you have to do in Java
long copyLarge(InputStream input, OutputStream output);

long copyLarge(InputStream input, OutputStream output, byte[] buffer);

long copyLarge(InputStream input, OutputStream output, long inputOffset, long length);

long copyLarge(InputStream input, OutputStream output, long inputOffset, long length, byte[] buffer);
```


### Functions
##### Vararg & Spread Operator 

```
fun max(vararg numbers: Int): Int {
    // ...
    return maxInteger
}

val integers = intArrayOf(4, 5, 6)
max(1, 2, *integers, 7, 8)
```


### Functions
##### Infix Notation

```
//Functions marked with the infix keyword can also be called using the infix notation
infix fun Int.shl(x: Int): Int {
    // ...
}

// calling the function using the infix notation
1 shl 2

// is the same as
1.shl(2)
```


### Functions
##### Infix Notation

```
// A more interesting example
enum class Suit { HEARTS, SPADES, CLUBS, DIAMONDS }
enum class Rank {
    TWO, THREE, ..., QUEEN, KING, ACE;
    infix fun of(suit: Suit) = Card(this, suit)
}
data class Card(val rank: Rank, val suit: Suit)

// Traditional approach to create a card
val card = Card(QUEEN, HEARTS)

// With infix notation => expressive and concise
val card = QUEEN of HEARTS
```