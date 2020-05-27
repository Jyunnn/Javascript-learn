# Switch

`Switch` 可以替帶很多個 `if`

```js {.line-numbers}
// 用 if
if ( i == 1 ){
    console.log("xs")
} else if ( i == 2) {
    console.log("s")
} else if ( i == 3) {
    console.log("m")
} else if ( i == 4) {
    console.log("l")
} else {
    console.log("xl")
}

//用 switch
switch (i) {
    case 1 :
        console.log('xs')
        break
    case 2 :
        console.log('s')
        break
    case 3 :
        console.log('m')
        break
    case 4 :
        console.log('l')
        break
    default:
        console.log('xl')
}

```

假如 `i = 3` , 則會顯示 `m`
但如果沒有 `break` , 就不會驗證之後的規則 , 顯示 `m,l,xl`
