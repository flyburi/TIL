Link
https://kotlinlang.org/docs/reference/packages.html

# Packages

```
package foo.bar

fun baz() { ... }
class Goo { ... }

// ...
```

# Default Imports

## default imports
```
kotlin.*
kotlin.annotation.*
kotlin.collections.*
kotlin.comparisons.* (since 1.1)
kotlin.io.*
kotlin.ranges.*
kotlin.sequences.*
kotlin.text.*
```
## platform 에 따라 추가로 import 가능.
```
JVM:
java.lang.*
kotlin.jvm.*

JS:
kotlin.js.*
```

## Imports
```
import foo.Bar // Bar is now accessible without qualification

import foo.* // everything in 'foo' becomes accessible

import foo.Bar // Bar is accessible
import bar.Bar as bBar // bBar stands for 'bar.Bar'
```

import 키워드는 제한없이 쓸 수 있다.
```
top-level functions and properties;
functions and properties declared in object declarations;
enum constants.

```
Java와는 다르게 Kotlin은  "import static" 문법이 따로 없다. 그냥 import 키워드를 사용하면 된다.

## Visibility of Top-level Declarations
만약 top-level 이 private으로 선언되어있으면 선언된 파일도 private이다.




