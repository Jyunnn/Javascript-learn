# String

現在字串最好使用` `` `反引號來表示,優點在於可以換行
```js {.line-numbers}
let users = `
    Eric
    Kevin
`;
```
以及可以使用`${}`來插入表達式

```js {.line-numbers}
console.log(`1+1 = ${1+1}`) // 1+1=2
```

如果真的必須要用單引號或雙引號,可以使用換行符號
```js {.line-numbers}
let users = "Eric\nKevin"
```
這個是一種跳脫字元,跳脫字元有`\`當開始,比方說要在字串內加入引號
```js {.line-numbers}
console.log('Hi , I'm Eric') // 報錯,缺少符號
console.log('Hi , I\'m Eric') // Hi , I'm Eric
```

調用字串內的某個字符,可以使用陣列`[n]`,或使用`string.charAt(n)`
```js {.line-numbers}
let name = "Hi , I'm Eric"
console.log(name[3]); // , (包含空白第四個是 逗號)
console.log(name.charAt(3)) // 同上
```
兩者區別在於,超過字串數量顯示的方式
```js {.line-numbers}
let name = "Hi , I'm Eric"
console.log(name[100]); // undefined
console.log(name.charAt(100)) // " "  (空白)
```

我們也可以用`for..of`來取字串內所有的字符
```js {.line-numbers}
let name = "Eric"

for ( n of name ){
    console.log(n); // "E" "R" "I" "C"
}
```

## 字串方法

`length`
先說,現在說的`length`這不是一個方法,它是在字串內的一個屬性,而不是函數,所以使用時不用`()`,這個是可以取得字串長度,回傳長度數字

### 大小寫

`toLowerCase()`和`toUpperCase()`可以改變文字大小寫
```js {.line-numbers}
console.log('Eric'.toLowerCase()) // eric
console.log('Eric'.toUpperCase()) // ERIC
```

### 查詢子字串(單詞)

`str.indexOf(substr,startNum)` 從 `startNum`開始,查詢`substr`單字在`str`的哪個位置,如果沒找到就回傳`-1`,有的話就回傳所在位置

```js {.line-numbers}
let user = `Eric in Jyunnn`
console.log(user.indexOf('in')); // 5
```
如果在判斷上面使用,以下是錯誤例子

```js {.line-numbers}
let user = `Eric in Jyunnn`
if(user.indexOf('Eric')){
    console.log('is find')
}
```
因為當在第一個就找到,會回傳`0`,判斷上會變成`false`,所以必須要這樣寫
```js {.line-numbers}
let user = `Eric in Jyunnn`
if( user.indexOf('Eric') != -1){
    console.log('is find')
}
```



`str.includes(substr,startNum)`跟`indexOf`一樣是查詢字串,不同的是`includes`回傳的是`boolean`
```js {.line-numbers}
let user = `Eric in Jyunnn`
console.log(user.includes('Eric')); //true
```
還有`str.startsWith`和`str.endsWith`,分別是判斷字母開頭單字和結尾單字,回傳`boolean`
```js {.line-numbers}
console.log('Refrigerator'.startsWith('ref')); // false 大小寫不對
console.log('Refrigerator'.startsWith('Ref')); // true
console.log('Refrigerator'.endsWith('ator')); // true
```

### 獲取字串字母

`str.slice(start [, end])` 可以取得`str`字串內,從`start`開始至`end`前(不包含`end`)的字母
(但`end`不可以大於`start`,否則回傳空白` `)
```js {.line-numbers}
let user = `Eric in Jyunnn`
console.log(user.slice(0,2)); //Er
```

`str.substring(start [, end])`  與上個方法很像,但這個允許`end`大於`start`
```js {.line-numbers}
console.log(`Eric in Jyunnn`.substring(8,3)) // c in
```

`str.substr(start [, length])` 也是很像`slice`,但是意思是從`start`開始,取得`length`個字母
```js {.line-numbers}
console.log(`Eric in Jyunnn`.substr(3,3)) // c i
```

我可以這個來限制文字數量,讓超過的字變成`...`
```js {.line-numbers}
function truncate(txt, num){
    if (txt.length < num) return txt; //如果字母少於需求,直接回傳字串
    let newTxt = txt.substr(0,num) + '...'
    return newTxt;
}

truncate("What I'd like to tell on this topic is:", 20) // Hello~~!
truncate("Hi ,Today is a nice day", 20) // Hi ,Today is a nice ...
```
