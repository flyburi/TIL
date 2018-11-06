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