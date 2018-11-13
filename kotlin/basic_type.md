Link https://kotlinlang.org/docs/reference/basic-types.html

# Basic Types

## Numbers
```
<Type>	<Bit width>
Double	64
Float	32
Long	64
Int	32
Short	16
Byte	8
``` 

## Literal Constants
Decimals: 123
- Longs 은 대문자 L 을 붙인다.: 123L

Hexadecimals: 0x0F

Binaries: 0b00001011

Doubles : 123.5

Floats 은 f나 F을 붙인다.: 123.5f


## Underscores in numeric literals (since 1.1)
숫자를 더 읽기 쉽게 underscore를 붙여 표현할 수 있다.
``` 
fun main(){
    val oneMillion = 1_000_000
    val creditCardNumber = 1234_5678_9012_3456L
    val socialSecurityNumber = 999_99_9999L
    val hexBytes = 0xFF_EC_DE_5E
	val bytes = 0b11010010_01101001_10010100_10010010

    println(oneMillion) //1000000
    println(creditCardNumber) //1234567890123456
	println(socialSecurityNumber) //999999999
    println(hexBytes) //4293713502
    println(bytes) //3530134674
    
}
``` 

## Representation
Java 플랫폼에서 number는 nullable number 참조(e.g. Int?)가 필요하거나 제네릭으로 호출하지 않는 한 JVM primitive 타입으로 저장된다.
nullable number 참조하거나 제네릭이 호출한다면 number는 boxing된다.

number boxing은 identity를 유지하지 않는다.
```
//boxedA 와 anotherBoxedA 는 nullable number로 참조되었기 때문에 객체는 같지 않다고 출력. 
fun main() {
    val a: Int = 10000
    println(a === a) // Prints 'true'
    val boxedA: Int? = a
    val anotherBoxedA: Int? = a
    println(boxedA === anotherBoxedA) // !!!Prints 'false'!!!
}
```

하지만, 두 변수의 값은 같다.
```
fun main() {
    val a: Int = 10000
    println(a == a) // Prints 'true'
    val boxedA: Int? = a
    val anotherBoxedA: Int? = a
    println(boxedA == anotherBoxedA) // Prints 'true'
} 
```

## Explicit Conversions(명시적 형변환) 

smaller type은 bigger type으로 묵시적 형변환이 되지 않는다.
명시적 형변환 없이는 Byte 타입을 Int 타입으로 할당할 수 없다는 것을 의미한다.

```
fun main() {
    val b: Byte = 1 // OK, literals are checked statically
    val i: Int = b // ERROR
    // 결과
    // Type mismatch: inferred type is Byte but Int was expected
}
```

명시적으로 형변환을 해보자.
```
fun main() {
    val b: Byte = 1
    val i: Int = b.toInt() // OK: explicitly widened
    print(i) // 에러 없이 "1"로 잘 찍힌다.
}

```
각 number type에는 다음과 같은 형변환 메소드가 있다.
```
toByte(): Byte
toShort(): Short
toInt(): Int
toLong(): Long
toFloat(): Float
toDouble(): Double
toChar(): Char
```
## Operations

비트 연산자 : Int와 Long 에서만 사용 가능하다.
```
shl(bits) – signed shift left (Java's <<)
shr(bits) – signed shift right (Java's >>)
ushr(bits) – unsigned shift right (Java's >>>)
and(bits) – bitwise and
or(bits) – bitwise or
xor(bits) – bitwise xor
inv() – bitwise inversion
```

## Floating Point Numbers Comparison

Equality checks: a == b and a != b

Comparison operators: a < b, a > b, a <= b, a >= b

Range instantiation and range checks: a..b, x in a..b, x !in a..b

```
NaN is considered equal to itself
NaN is considered greater than any other element including POSITIVE_INFINITY
-0.0 is considered less than 0.0
```

## Characters

Characters는 Char 타입으로 표현되고 number를 직접 쓸 수 없다.
```
fun check(c: Char) {
    if (c == 1) { // ERROR: incompatible types
        // ...
    }
}
```
Character literals은 홀 따옴표로 감싸줘야한다.
 
특수 문자는 역슬래쉬를 사용해서 escape 할 수 있다.
지원하는 escape 문자 : \t, \b, \n, \r, \', \", \\, \$
다른 문자열 encode 하기 위해서는 unicode를 사용 :'\uFF00'

Character를 Int 타입으로 명시적 형변환하기.
```
fun decimalDigitValue(c: Char): Int {
    if (c !in '0'..'9')
        throw IllegalArgumentException("Out of range")
    return c.toInt() - '0'.toInt() // Explicit conversions to numbers
}
```

## Booleans
Boolean은 true, false 두 개의 값을 가진다.

boolean에는 아래와 같은 built-in 연산자도 포함한다.
|| – lazy disjunction
&& – lazy conjunction
! - negation


## Arrays
get, set function을 가지는 Array class.
```
class Array<T> private constructor() {
    val size: Int
    operator fun get(index: Int): T
    operator fun set(index: Int, value: T): Unit

    operator fun iterator(): Iterator<T>
    // ...
}
```

array를 생성하기 위해, arrayOf() function을 사용하고 arrayOf(1,2,3) 처럼 값을 전달하면,
array [1,2,3] 이 생성이 된다. 
아니면 arrayOfNulls()를 이용하여 null element로 채워진 array를 생성할 수도 있다.

또, Array 생성자를 이용해서 array size와 function을 받는 생성자를 사용해서 
각 index 별로 array element의 값을 초기화한 후 return 할수도 있다.

```
fun main() {
    // Creates an Array<String> with values ["0", "1", "4", "9", "16"]
    val asc = Array(5, { i -> (i * i).toString() })
    asc.forEach { println(it) }
}
/* return */
/* 
0
1
4
9
16
*/
```
[] 연산자는 function의 member인 get(), set()을 호출한다.

Note:
자바와 다르게 Kotlin에서 array는 불변이다.
이 말은 Kotlin은 Array<String>을 Array<Any>로 할당할 수 없다는 뜻이다.

Kotlin에는 또한 boxing 없이 primitive 타입의 array를 표현할 수 있는 특수한 클래스가 있다.
ByteArray, ShortArray, IntArray 등등 
이 클래스트들은 Array 클래스를 상속하지 않았으나 같은 method나 properties 들이 있다. 

```
val x: IntArray = intArrayOf(1,2,3)
x[0] = x[1] + x[2]

```

## Unsigned integers
Kotlin은 unsigned integer 타입을 따른다.

```
kotlin.UByte: an unsigned 8-bit integer, ranges from 0 to 255
kotlin.UShort: an unsigned 16-bit integer, ranges from 0 to 65535
kotlin.UInt: an unsigned 32-bit integer, ranges from 0 to 2^32 - 1
kotlin.ULong: an unsigned 64-bit integer, ranges from 0 to 2^64 - 1
```

## Specialized classes

```
kotlin.UByteArray: an array of unsigned bytes
kotlin.UShortArray: an array of unsigned shorts
kotlin.UIntArray: an array of unsigned ints
kotlin.ULongArray: an array of unsigned longs
```

UInt와 ULong을 지원하는 range와 progression
```
kotlin.ranges.UIntRange, 
kotlin.ranges.UIntProgression, 
kotlin.ranges.ULongRange, 
kotlin.ranges.ULongProgression
```

## Literals
unsigned integer를 쉽게 이용하기 위해 kotlin에서는 숫자 리터럴(literal)뒤에 specific unsigned type (Float/Long와 비슷)를 나타낼 수 있도록 제공한다.

u와 U를 뒤에 분이면 unsinged를 나타낸다.  
타입을 안붙이면 literal의 사이즈에 따라 UInt나 ULong이 제공된다. 

```
val b: UByte = 1u  // UByte, expected type provided
val s: UShort = 1u // UShort, expected type provided
val l: ULong = 1u  // ULong, expected type provided

val a1 = 42u // UInt: no expected type provided, constant fits in UInt
val a2 = 0xFFFF_FFFF_FFFFu // ULong: no expected type provided, constant doesn't fit in UInt
```

unsigned long으로 명시적으로 uL, UL 붙여주기
```
val a = 1UL // ULong, even though no expected type provided and constant fits into UInt
```

## Experimental status of unsigned integers
..(생략. 나중에 필요할 때 보기로.. )..

## Strings
String은 불변.
String의 각 element에 접근하기 위해서는 s[i] 처럼 index 연산자로 접근 가능하다.
```
fun main() {
val str = "abcd"
    for (c in str) {
        println(c)
    }
}
```

+ 연산자를 이용해서 String 값 연결하기(붙이기)
```
fun main() {
    val s = "abc" + 1
    println(s + "def")
}
```

## String Literals
Kotlin은 string literal 두개의 타입을 가진다.

