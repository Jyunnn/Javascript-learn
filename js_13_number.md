# Number

先前在型別有提到`Number`及`BigInt`
因為`Number`無法顯示大於 2^53^ 或小於 -2^53^ 
所以才有一個`BigInt`的型別來處理這個比較特殊的數字


## 數字縮寫

一般來說 1萬可以寫作
```js {.line-numbers}
let i = 10000;
```
可以縮寫成
```js {.line-numbers}
let i = 1e4; //意思是 1後面 4個0
```
小數點可以寫作
```js {.line-numbers}
let i = 1e-4; //意思是 1左邊 4個0  等於 0.0001
```

## 、二、八、十六進位制 

### toString(base)
這個方法可以將數字轉換成需要的的進位制,參數`base`就是進位制的型式,可以是`2`到`36`,默認是`10`(進位)
```js {.line-numbers}
let num = 255;
console.log(num.toString(16)) // ff
console.log(num.toString(8)) // 377
console.log(1024..toString(8)) // 2000
```
上方有用兩個`.`,是因為如果只用一個,引擎會誤判為小數點,這樣會報錯,故使用兩個點才會是正確,`.`後面其實會有一個可以省略的`0`
```js {.line-numbers}
console.log(1024.0.toString(8)) // 2000
console.log(1024..toString(8)) // 2000
```

## Rounding 捨去/進位

***`Math.floor`***
無條件捨去 `3.1`變成`3` , `-1.2`變成`-2`]

***`Math.ceil`***
無條件進位 `3.1`變成`4` , `-1.2`變成`-1`

***`Math.round`***
四捨五入 `3.1`變成`3` , `3.6`變成`4`

***`Math.trunc`***
完全移除小數點後的數字 `1.2`變成`1` , `-1.1`變成`-1`

***`Math.toFixed(n)`***
將小數四捨五入制小數點後`n`位
```js {.line-numbers}
let num = 12.3456;
console.log(num.toFixed(2)) //12.35
```


---

接下來看一個例子
```js {.line-numbers}
console.log(0.1 + 0.2 == 0.3) // false
```

因為它其實是
```js {.line-numbers}
console.log(0.1 + 0.2) // 0.30000000000000004
```

這個問題主要是二進位制時,小數會有循環小數
解決這個問題,需要自行轉回整數,在除回來
不過要注意,這個方法只能減少狀況發生,還是會有少數無法用這個方法來解決

```js {.line-numbers}
console.log( (0.1*10+0.2*10)/10 ) // 0.3
```

---

## isFinite / inNaN

`Infinity`是一個特殊數值,它比任何數字還要大
`NaN`就是 Not a Number,即代表一個錯誤
之前有提到,`NaN`不代表任何值,包含它自己

```js {.line-numbers}
console.log( NaN == NaN) // false
```

這樣我們就能用`isNaN`來判斷是否為`NaN`

```js {.line-numbers}
console.log( isNaN(NaN) ) // true
console.log( isNaN("String") ) // true
```

`isFinite`會把參數轉為數字,如果是常規數字就回傳`true`


```js {.line-numbers}
console.log( isFinite(20) ) // true
console.log( isFinite("String") ) // false , 因為會先轉為NaN
console.log( isFinite(Infinity) )  // false , 它是特殊值,無法轉數字
```

> 有個方式可以判斷 NaN 與自身相等 
> `Object.is(val1, val2)`
> ```js {.line-numbers}
> console.log(Object.is(NaN,NaN)) // true
> ```

---
## parseInt/parseFloat

如果用`+`或是`Number()`轉成數字型別,那會變得比較嚴格,如果要轉換的不是數字就會失敗

```js {.line-numbers}
console.log(+"100px") // NaN
```
- **`parseInt`** 可以在字串內讀取數字,直到沒有數字,會回傳一個整數數字
```js {.line-numbers}
console.log(parseInt('100px')) // 100
console.log(parseInt('100px10020')) // 100,因為遇到'p'讀不到數字就停止了
```
- **`parseFloat`** 會在字串內讀取數字,可以回傳小數點後的數字

```js {.line-numbers}
console.log(parseFloat('12.55px')) // 12.55
console.log(parseFloat('3.14.15px')) // 3.14 第二個點出現錯誤 停止讀取
```

---

## 其他函數

- **`Math.random()`** 會產生一個介於`0`到`1`之間的隨機數字
```js {.line-numbers}
Math.random() // 0.07977325033093607
Math.random() // 0.39051666135249663
```

- **`Math.max(a, b, c...) / Math.min(a, b, c...)`** 回傳數字堆最大或最小值
```js {.line-numbers}
Math.max(2,4,-8,9,0) // 9
Math.min(2,4,-8,9,0) // -8
```

- **`Math.pow(n, power)`** 數字`n` 的 `power` 次方
```js {.line-numbers}
Math.pow(2, 10) // 1024
Math.pow(3, 2) // 9
```