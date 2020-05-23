# 迴圈 while , for

這個很常用,非常常用也很好用,所以很重要
### while 迴圈
```js{.line-numbers}
while (condition) {
  // 循環區塊
}
```
如果 `condition` 是 `ture` 的話, 則執行循環區塊

```js{.line-numbers}
let i = 0
while ( i < 3 ) {
  console.log(i);
  i++
}
```
<small>以上範例解說
執行時 `i = 0` , 符合 `i < 3` , 所以執行循環區塊 , 先傳入 `console.log` 裡, 此時 `i` 為 `0` , 在執行 `i++` , 此時 `i = 1`;
到了 `i = 3` 時 , 不符合 `i < 3` , 所以停止循環區塊
</small>

<br/>

如果只有一行code的話,可寫作
```js{.line-numbers}
let i = 0
while ( i < 3 ) i++ 
```
<br/>
### do...while 迴圈

```js{.line-numbers}
do {
  // 循環區塊
} while (condition)
```
這個方式是先循環,在判斷是否為真

```js{.line-numbers}
let i = 0
do {
    console.log(i);
    i++
} while ( i < 3 )
```
除非你要讓這個循環至少執行一次,不然就用 while 即可
*如果一開始就讓 `i = 3` ,就會有區別*

<br />

### for 迴圈

這個很常用,功能也比較複雜
```js{.line-numbers}
for (begin; condition; step) {
  // 循環區塊
}
```
|參數|範例|解釋|
|:--:|:--:|:--:|
|begin|i = 0|第一次進入循環時先執行一次|
|condition|	i < 3|每次進循環區塊時都檢查一次,如果是假值就停止|
|step|i++|每次進循區塊後執行一次|
|循環區塊|console.log(i)|檢查是真值,就執行|


> 開始執行 > 執行 begin >
> >判斷 condition > 執行 循環區塊 > 執行 step
> >判斷 condition > 執行 循環區塊 > 執行 step
> ... 直到 condition 判斷為 false

<br />

但是要注意 , `begin` 是用 `let` , 所以它只存在於這個區塊 , 全域區塊是沒有這個變數的存在 

```js{.line-numbers}
for (let i = 0; i < 3 ; i++) {
  console.log(i)
}
alert(i) //error , i is not defined
```

如果要讓它存在於全域,必須先在全域先宣告

---
#### 跳出迴圈 break

只要是條件被判斷為 `false` 時 , 就會跳出循環
也可以使用 `break` 強制停止

```js{.line-numbers}
let i = 0
while ( i < 5 ) {
  i++
  if ( i = 3) break;
}
console.log(i) // 3
```

#### 跳出本次迴圈,執行下一個循環 `continue` 

這個不會馬上停止 , 它只是跳過這個循環 , 然後執行下一個循環 

```js{.line-numbers}
for ( let i = 0 ; i < 5 ; i++ ) {
    if ( i % 2 == 0 ) continue
    console.log(i) // 1 , 3
}
```

#### break標籤

假如說今天迴圈寫得很巢狀
我需要在某個地方就跳出迴圈至開頭
就可以使用標籤

```js{.line-numbers}
out :for( let i = 100 ; i > 1 ; i-- ) {
      for (let x = 2 ; x < 100 ; x++ ) {
          if ( i % x == 0 && i != x) continue out
      };
      console.log(i);
};
```
這是一個求質數,當 `i` 除上 `x` 的餘數為 `0` 且 `i` 不等於 `x` , 就返回 out 這個標籤 ,也就是跳出本次迴圈並回到第一行 ,而不執行最後的 `console.log`, 如果用 `break` 的話, 只是跳脫本行,但是還是繼續執行下一行  
 