# 運算

有分一元運算式和二元運算式
一元就是只有一個運算元
```js {.line-numbers}
let x = 1
x = -x
console.log( x ) // -1
```
二元就是有兩個運算元
```js {.line-numbers}
let x = 1 , y = 2
console.log( x + y ) // 3
```

---


一元運算符如果對非數字,可以將其轉化成數字
(可是對數字無效)
```js {.line-numbers}
let x = 1;
console.log( +x ); // 1 

let y = -2;
console.log( +y ); // -2 無效

console.log( +true ); // 1
console.log( +"" );   // 0

```

---

減 乘 除 只能對數字或數字字串有效,並轉為數字
```js {.line-numbers}
console.log( "2" - 1 ) // 1
console.log( "2" * 1 ) // 2
```

加號比較特別,
`string` 互加會合併相加的字串
```js {.line-numbers}
let s = "my" + "string";
alert(s); // mystring
```

數字相加就不用提
但是混入一個 `string` 就變成..
```js {.line-numbers}
console.log( "9" + 1 ) //"91"
console.log( 8 + "1" ) //"81"
console.log( 8 + 8 + "1" ) //"161"
```
*因為運算是由左至右,所以第三個範例是先8+8=16,再由數字16和字串1相加變成"161"*

---

`%` 可以求餘數
`**` 可以求次方

```js {.line-numbers}
console.log( 8 % 3 ) // 2
console.log( "9" % 2 ) // 1

console.log( "2" ** 10 ) // 2的十次方 1024
```


---
接下來是頗重要的部分
遞增 `++` 和遞減 `--`
只對變數有效


```js {.line-numbers}
let x = 1
x++
console.log( x ) // 2
console.log( 5++ ) //error
```

有前置和後置兩種形式
`x++` 和 `++x`
兩種是不一樣的,但只有使用回傳的時候才有區別

```js {.line-numbers}
let counter = 1;
let a = ++counter;

console.log( a ) // 2
```
前置型式先對counter做遞增
且回傳新值 `2` ,所以 `a = 2`;

```js {.line-numbers}
let counter = 1;
let a = counter++;

console.log( a ) // 1
```
後置型式是回傳舊的值
`a = 1 `, 然後 `counter` 在遞增為 `2`

再用幾個範例解釋
```js {.line-numbers}
let x = 1 , y = 1;
console.log( 2 * ++x ) // 4 , x = 2
console.log( 2 * y++ ) // 2 , 因為先傳舊值 y = 1 在相乘 ; 之後 y = 2
```

---
#### 修改

如果數字要修改
```js {.line-numbers}
let x = 1
x = x + 1
console.log( x ) // 2
```
這個可以簡化為
```js {.line-numbers}
let x = 1
x += 1
console.log( x ) // 2
```
---

# 值的比較

比較後會回傳 `Boolean` 值 , 也可以賦予變數
```js {.line-numbers}
console.log( 2 > 1 ) // true
console.log( 4 > 5 ) // false

let x = 4 > 5 ;
console.log( x ) // false
```

`String` 的比較是用字的 `unicode` 碼的順序
會先比較字首,如果有一方比較大(或比較小),就會回傳
如果字首相等,就會在比較下一個,如果都沒有結果,就會判斷相等
```js {.line-numbers}
console.log( "APPLE" > "ABPLE" ) // true
console.log( "APPLE" < "BANANA" ) // true  B 比 A 大
console.log( "aPPLE" < "BANANA" ) // false  小寫 比 大寫 大 (小寫順序較後面)
```
如果是不同的型別比較
會先轉成數字比較
```js {.line-numbers}
console.log( "12" > 10 ) // true
console.log( "01" < 2 ) // false

console.log( true == 1 ) // true 會轉會成 1
console.log( false == 0 ) // 同上 , false 轉成 0
```
---
# 嚴格相等

剛剛有舉例 `true` 和 `false`

```js {.line-numbers}
console.log( false == 0 ) // true
```
但是照這樣看來,可能沒辦法區分 0 和 false
所以就有 === 的出現

```js {.line-numbers}
console.log( false === 0 ) // false
```

## null 和 undefined

```js {.line-numbers}
console.log( null == undefined ) // true 它們是相等的
console.log( null === undefined ) // false
```

可是剛剛明明說 `null` 會轉成 `0` , `undefined` 會轉成 `NaN`
(這就是很奇怪的地方)
更奇怪的是 `null`

```js {.line-numbers}
console.log( null == 0 ) // false
console.log( null > 0 ) // false
console.log( null >= undefined ) // true
```
ㄏㄏ 只能記起來了

`undefined` 就還好
```js {.line-numbers}
console.log( undefined == 0 ) // false , 因為 undefined 只跟 null 相等
console.log( undefined > 0 ) // false , 轉成數字是 NaN
console.log( undefined >= undefined ) // false
```