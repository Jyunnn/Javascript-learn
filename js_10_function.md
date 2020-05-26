# 函數

> 基礎的東西略過

函數參數如果沒有使用, 則會變成 `undefined`
所以可以預設參數為某個值

```js {.line-numbers}
function hello(name, text = "Hello"){
    console.log( `${text},${name}`);
}
hello('Eric') // Hello,Eric
```

但這個預設參數是ES6出來的,如果用舊版的會無法使用,可改用 || 來判斷
```js {.line-numbers}
function hello(name, text){
    text = text || 'Hello' 
    console.log( `${text},${name}`);
}
hello('Eric') // Hello,Eric
```

### return 
> 基礎的東西略過

`return` 可以沒有回傳值,回傳出來的是 `undefined`

```js {.line-numbers}
function boo (){
    return
}

var a = boo()

console.log ( a == undefined ) //true

```

`return` 的回傳值並須是同一行, 分行後回傳的會是 `undefined`


---

函數命名建議
- "show..."
- "get..."
- "calc..."
- "create..."
- "check"

---

### 函式聲明

```js {.line-numbers}
function foo(txt) {
    console.log(txt)
}
```

### 函式表達式

```js {.line-numbers}
let foo = function(txt) {
    console.log(txt)
}
```

### 箭頭函式

單行箭頭函式
```js {.line-numbers}
let foo = (txt) => console.log(txt) 
```

多行箭頭函式 (多行一定要加花括號)
```js {.line-numbers}
let foo = (num1, num2) => {
    let newNum = num1 +num2
    return newNum
} 
```

箭頭函式沒有`this`,會直接從外層取得

箭頭函式沒有`arguments`,也不能用`new `