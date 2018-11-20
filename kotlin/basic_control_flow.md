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






















