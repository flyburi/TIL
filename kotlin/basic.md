
Link : https://kotlinlang.org/docs/reference/basic-syntax.html

# functions 선언

### Int 파라미터 & 리턴 타입 선언
```
fun sum(a: Int, b: Int): Int {
    return a + b
}
```

### expression body 과 리턴 타입 추론 
```
fun sum(a: Int, b: Int) = a + b
```

### return 값 없을 때는 Unit
```
fun printSum(a: Int, b: Int): Unit {
    println("sum of $a and $b is ${a + b}")
}
```

### Unit return 타입 생략 
```
fun printSum(a: Int, b: Int) {
    println("sum of $a and $b is ${a + b}")
}
```

# variables 선언
```
val a: Int = 1  // 선언과 동시에 할당.
val b = 2   // Int 타입 생략 추론. 
val c: Int  // Type만 정의하고, 초기값 없음
c = 3       // deferred assignment
```

### Mutable 값
```
var x = 5 // Int 타입 추론.
x += 1
```

### Top-level 변수
```
val PI = 3.14
var x = 0

fun incrementX() { 
    x += 1 
}
```

# Comments
```
// This is an end-of-line comment

/* This is a block comment
   on multiple lines. */
```

# string templates 
```
fun main() {
    var a = 1
    // simple name in template:
    val s1 = "a is $a" 

    a = 2
    // arbitrary expression in template:
    val s2 = "${s1.replace("is", "was")}, but now is $a"
    println(s2)
}
```


# conditional expressions
```
fun maxOf(a: Int, b: Int): Int {
    if (a > b) {
        return a
    } else {
        return b
    }
}

fun main() {
    println("max of 0 and 42 is ${maxOf(0, 42)}")
} 
```

### if 조건을 이용해서 maxOf fun 구현하면
```
fun maxOf(a: Int, b: Int) = if (a > b) a else b
```


### nullable 값 체크
```
fun parseInt(str: String): Int? {
    // ...
}
```

```
fun parseInt(str: String): Int? {
    return str.toIntOrNull()
}

fun printProduct(arg1: String, arg2: String) {
    val x = parseInt(arg1)
    val y = parseInt(arg2)

    // Using `x * y` yields error because they may hold nulls.
    if (x != null && y != null) {
        // x and y are automatically cast to non-nullable after null check
        println(x * y)
    }
    else {
        println("either '$arg1' or '$arg2' is not a number")
    }    
}


fun main() {
    printProduct("6", "7")
    printProduct("a", "7")
    printProduct("a", "b")
}
```
or
```
fun parseInt(str: String): Int? {
    return str.toIntOrNull()
}

fun printProduct(arg1: String, arg2: String) {
    val x = parseInt(arg1)
    val y = parseInt(arg2)
    
    // ...
    if (x == null) {
        println("Wrong number format in arg1: '$arg1'")
        return
    }
    if (y == null) {
        println("Wrong number format in arg2: '$arg2'")
        return
    }

    // x and y are automatically cast to non-nullable after null check
    println(x * y)
}

fun main() {
    printProduct("6", "7")
    printProduct("a", "7")
    printProduct("99", "b")
}
```
### 타입 체크와 automatic 캐스팅
is 연산자 : 타입의 instance 체크.

is 연산자를 이용해서 특정 타입인지 체크한 후에 해당 타입일때 자동 캐스팅된 후 처리되고, 그외의 타입일땐 캐스팅하지 않는다.

```
fun getStringLength(obj: Any): Int? {
    if (obj is String) {
        // `obj` is automatically cast to `String` in this branch
        return obj.length
    }

    // `obj` is still of type `Any` outside of the type-checked branch
    return null
}


fun main() {
    fun printLength(obj: Any) {
        println("'$obj' string length is ${getStringLength(obj) ?: "... err, not a string"} ")
    }
    printLength("Incomprehensibilities")
    printLength(1000)
    printLength(listOf(Any()))
}
```
or 더 짧게
```
fun getStringLength(obj: Any): Int? {
    if (obj !is String) return null

    // `obj` is automatically cast to `String` in this branch
    return obj.length
}
```

### Using a for loop