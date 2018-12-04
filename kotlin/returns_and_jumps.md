Returns and Jumps

Link https://kotlinlang.org/docs/reference/returns.html

kotlin에서 jump expressions은 세가지
```
- return. By default returns from the nearest enclosing function or anonymous function.
- break. Terminates the nearest enclosing loop.
- continue. Proceeds to the next step of the nearest enclosing loop.
```

```
val s = person.name ?: return
```

# Break and Continue Labels

kotlin에서 label을 이용하여 @ 기호를 뒤에 붙여준다.
```
loop@ for (i in 1..100) {
    // ...
}
```


if문에서 break가 걸리면, @loop가 없을땐 해당 for문에서 loop가 끝나지만, @loop를 붙여준 반복문에서 종료가 된다.
```
loop@ for (i in 1..100) {
    for (j in 1..100) {
        if (...) break@loop
    }
}
```

# Return at Labels

