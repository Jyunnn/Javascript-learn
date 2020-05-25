# this

之前上課內容,講師是說`this`的指向取決於怎麼呼叫,也就是當前的對象

```js{.line-numbers}
function callName(){
    console.log(this.userName);
}

callName() //直接呼叫就是取全域 (Window) undefined

let user1 = {
    userName:"Eric",
    callName: callName,
}

user1.callName() //由user1呼叫 , "Eric"

```

如果是在嚴格模式,直接呼叫`this`是`undefined`,所以直接執行`callName()`將會報錯


當我們呼叫`user1.callName()`,`this`判斷流程如下

1. `.`點符號先取得呼叫的物件
2. 然後由括號`()`執行

如果今天改用這樣呼叫

```js{.line-numbers}
function callName(){
    console.log(this.userName);
}

let user1 = {
    userName:"Eric",
    callName: callName,
}

let callUser01Name = user1.callName
console.log(callUser01Name()) // undefined
```

當把這兩個條件拆開了,`this`就會丟失,所以就回傳`undefined`

解決方式就是在外面再包一層,讓裡面的條件不要分開

```js{.line-numbers}
let callUser01Name = function(){
    user1.callName()
}
console.log(callUser01Name()) // Eric
```


## 函數綁定

上個例子中,因為將其拆開呼叫 丟失了`this`

函數中有提供一個內建的方法 `bind`

### `Function.prototype.bind()`

在把上個例子拿出來,用`bind`來綁定`user1`物件
此時`this`等於`user1`,這樣就可以正常呼叫

```js{.line-numbers}
function callName(){
    console.log(this.userName);
}

let user1 = {
    userName:"Eric",
    callName: callName,
}

let callUser01Name = user1.callName.bind(user1)
console.log(callUser01Name())// Eric
```

`bind`還可以綁定參數,下列範例是
新增一個函數`double`,不指向物件(因為函式中不需要,綁定對象無法省略)並固定帶入參數`2`


```js{.line-numbers}
function mul(a, b) {
  return a * b;
}

let double = mul.bind(null, 2);

console.log( double(3) ); // = mul(2, 3) = 6
console.log( double(4) ); // = mul(2, 4) = 8
console.log( double(5) ); // = mul(2, 5) = 10

```

## 箭頭函式

箭頭函式比較特別,沒有自己的`this`,它會從外層取得,如果外層也沒有,就回傳`undefined`

```js{.line-numbers}
let callName = () => {
    console.log(this.userName);
}

let user1 = {
    userName:"Eric",
    Age:20,
    callName: callName,
}

console.log(user1.callName()) // undefined
```