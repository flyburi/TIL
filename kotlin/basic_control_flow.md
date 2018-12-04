Control Flow: if, when, for, while

Link https://kotlinlang.org/docs/reference/control-flow.html

# If Expression
Kotlin에서 if는 값을 반환하는 표현식(expression)이다.
그래서 (condition ? then : else)와 같은 3항 연산자가 없다.     

```
// Traditional usage 
var max = a 
if (a < b) max = b

// With else 
var max: Int
if (a > b) {
    max = a
} else {
    max = b
}
 
// As expression 
val max = if (a > b) a else b
```

if는 { } 로 감쌀수 있고, {}의 마지막에 값은 last expression 

```
val a = 1
val b = 2

val max = if (a > b) {
    print("Choose a:")
    a
} else {
    print("Choose b:")
    b
}
print(max)
    
```

if는 꼭 else 가 있어야 한다. 만약 없다면 컴파일 에러가 난다.
```
fun main(){
    val a = 1
    val b = 2
    
    val max = if (a > b) {
    	print("Choose a:")
	    a
	} 
    print(max)
   
}
// 'if' must have both main and 'else' branches if used as an expression
 
```

# When Expression
```
when (x) {
    1 -> print("x == 1")
    2 -> print("x == 2")
    else -> { // Note the block
        print("x is neither 1 nor 2")
    }
}
```

만약 여러 case 를 동시에 쓸 경우는 아래처럼. 
```
when (x) {
    0, 1 -> print("x == 0 or x == 1")
    else -> print("otherwise")
}
```
when의 else는 필수. 없으면 컴파일 에러남.

값을 지정하지 않고도 when 안에 들어온 값을 변경가능한지를 case로 쓸수있다.
```
when (x) {
    parseInt(s) -> print("s encodes x")
    else -> print("s does not encode x")
}
```

in과 !in을 통해서 collection의 범위에 있는지 체크도 가능하다.
```
when (x) {
    in 1..10 -> print("x is in the range")
    in validNumbers -> print("x is valid")
    !in 10..20 -> print("x is outside the range")
    else -> print("none of the above")
} 
```

특정 타입인지 체크도 가능.
```
fun hasPrefix(x: Any) = when(x) {
    is String -> x.startsWith("prefix")
    else -> false
}
```

if - else if 를 대체하여 사용
```
when {
    x.isOdd() -> print("x is odd")
    x.isEven() -> print("x is even")
    else -> print("x is funny")
}
```

Kotlin 1.3 이후 버전에선 when 안의 변수값을 이용하여 사용 가능.
```
fun Request.getBody() =
        when (val response = executeRequest()) {
            is Success -> response.body
            is HttpError -> throw HttpException(response.status)
        }
```

# For Loops

```
for (item in collection) print(item)

for (item: Int in ints) {
    // ...
}
```

range expression를 이용하여 number의 범위를 순차적으로 loop 도는 것이 가능.
```
for (i in 1..3) {
    println(i)
}
for (i in 6 downTo 0 step 2) {
    println(i)
}
```

array나 list의 index 이용
```
for (i in array.indices) {
    println(array[i])
}
```

array의 withIndex도 사용 가능
```
for ((index, value) in array.withIndex()) {
    println("the element at $index is $value")
}
```


# While Loops
while과 do..while 모두 이용가능.
```
while (x > 0) {
    x--
}

do {
    val y = retrieveData()
} while (y != null) // y is visible here!
``` 

# loops 안에서 break와 continue 사용
break, continue 지원한다.
자세한건 다음장에서 계속..
https://kotlinlang.org/docs/reference/returns.html
























