#條件運算( if 和 ? )

`if..else` 很常用, 比較初階的用法就不解釋
`?` 的部分

```js {.line-numbers}
//如果是if..else的寫法
if ( i > 10 ) {
    console.log("true")
} else {
    console.log("false")
}
//如果是?的寫法
( i > 10 ) ? "true" : "false"
```


一個的話就還好,但如果是很多個`?`的話

```js {.line-numbers}
//如果是if..else的寫法
( i < 10 ) ? "Hi" :
( i < 18 ) ? "Hello" :
( i < 25 ) ? "Hmmm..." : "Too old"
```

流程是這樣,先檢查第一行,如果是 `ture` ,則回傳 "Hi" ; 如果是 `false` , 則執行 : 右方的判斷。

---

# &&(與) 和 ||(或)

- A與B要是 `ture`
  - 意思就是兩個都要是 `ture`
  - 由左至右
  - 如果有一個是 `false` 就會回傳那個 `false` , 後面就略過  
  - 到最後一個都沒有找到 `false` , 就回傳最後一個值

- A或B要是 ture
  - 意思是兩個只要其中一個是 `ture`
  - 由左至右
  - 如果有一個是 `ture` 就會回傳那個 `ture` , 後面就略過 
  - 到最後一個都沒有找到 `ture` , 就回傳最後一個值

</br>
</br>

> ### 注意 
> `&&` 比 `||` 還優先運算
> ```js {.line-numbers}
> let a = null || 3 && 4 || 5
> console.log(a) // 4
> // 一開始先比較 3 && 4 ,回傳第一個假值 ,沒有的話回傳最後一個值 4
> // 就變成 null || 4 || 5 ,回傳第一個真值 , 回傳 4 , 所以 a = 4
> ```