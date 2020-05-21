#型別

Javascript 有8種資料型別
#### String

```js {.line-numbers}
let user1 = 'John' ;
let user2 = "Sam" ;
let user3 = `Eric` ;
```
#### Number

```js {.line-numbers}
let num = 123;
num = 1.2345;
typeof Infinity //"number"
typeof NaN //"number"
```

其中 Infinity 和 NaN 都是 Number

Infinity 無限大的 Number
```js {.line-numbers}
9999999999999999999999999999 > Infinity
// false
```

NaN 一個不正確或為定義的數學計算產生的
```js {.line-numbers}
console.log("error"/100)
// NaN
```
#### BigInt

這個是新的型別,
因為在JS中,`Number`無法顯示 大於或小於`2^53^`的整數
在整數末端加上==n==就可以創建一個`BigInt`

*目前只有chrome和firefox支援*

```js {.line-numbers}
const bigInt = 1234567890123456789012345678901234567890n;
```

#### Boolean

只有兩個給你選擇
`true` 和 `false`

```js {.line-numbers}
let num1 = 5;
let num2 = 9;
let a = num1 > num2
a // false
```

#### object



#### symbol
#### null

`null`是一種型別,表示空值、無、未知, 但是...
```js {.line-numbers}
let a = null;
typeof a //"object" 無言
```
因為有些網站有依賴這個規則,所以是不會修正這個了

#### undefined

意思就是未賦予值
```js {.line-numbers}
let a ;
typeof a //"undefined"
```

---

## 型別轉換

運算的時候(運算符或是函數執行),會自動把型別轉換成能處理型別.
```js {.line-numbers}
let boo = false
alert(typeof boo) //跳出視窗顯示 false

alert("9"/"3") // 數字3
```
#####number轉換規則
|值|轉換|
|:--:|:---:|
|undefined|NaN|
|null|0|
|ture、false|1、0|
|string|去除頭尾空格,留下如果是數字就為數字;如果是空值,轉換成0;如不符合上述規則,就會在剩下來的字串轉換,出現error時回傳NaN|


#####boolean轉換規則

空值都回傳 `false` ( `0`, `null` , `undefined` 和 `NaN` )
其他非空值都回傳 true
```js {.line-numbers}
alert( Boolean(1) ); // true
alert( Boolean(0) ); // false
alert( Boolean("hello") ); // true
alert( Boolean("") ); // false
alert( Boolean("0") ); // true 字串 0
alert( Boolean(" ") ); // true 空白字元也是字串
```