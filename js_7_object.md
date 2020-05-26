# 物件 Object

```js {.line-numbers}
let user = {
    name:"Eric",
    age:29
}
```

在 user 物件內, name 和 age 是 key , "Eric" 和 29 是 value

假如說 key 帶有空格,建立時需要加入引號,呼叫時必須用方括號

```js {.line-numbers}
let user = {
    name:"Eric",
    age:29,
    "calc year":2020-1911,
}

console.log(user["calc year"]); // 109
```

### in
有時候我們需要測試某個 key 有沒有在 目前物件裡面
```js {.line-numbers}
"key" in object
```
<small>*注意:一定要加引號*</small>

範例:
```js {.line-numbers}
let user = {
    name:"Eric",
    age:29
}
console.log("age" in user) // true
console.log("foo" in user) // false
```

in 可以拿來判斷 undefined , 因為有時候 某個 key 的 value 是 undefined , 可能就會誤判這個 key 是不存在的

```js {.line-numbers}
let user = {
    name:"Eric",
    age:29,
    foo:undefined
}
console.log(user.foo) // undefined
console.log(user.boo) // 真的不存在的也是 undefined
console.log("foo" in user) // true
```

### for...in 
可以將一個物件所有的 key 全部循環一次
```js {.line-numbers}
for (key in object) {
  // 可以在這裡對每個key進行操作
}
```

範例
```js {.line-numbers}
let user = {
    name:"Eric",
    age:29
}

for (key in user) {
  console.log(key) // name age
}
```

而且會對數字自動升序排列
```js {.line-numbers}
let user = {
    20:"Eric",
    1:"Polo",
    9:"Kevin"
}

for (key in user) {
  console.log(key)
}
```

---
### 複製引用

原始型別跟物件的差別,在於原始型別是傳值

```js {.line-numbers}
let text = "Hello!";
let message = text;
text = "Hi!"

console.log(text) // Hi!
console.log(message) // Hello!
```

物件是傳址(傳參考),動了被傳遞的物件值,原始物件的值也會一起被更動

```js {.line-numbers}
let user1 = {name:"Eric"};
let user2 = user1;

console.log(user1) //{name:"Eric"}
console.log(user2) //{name:"Eric"}

user2.name = "Polo"

console.log(user1) //{name: "Polo"}
console.log(user2) //{name: "Polo"}
console.log(user1 === user2); // true 絕對相等
```

### const 物件更改

const 是一個不能被改變的常數
但是如果是物件的話,是可以被改變的

```js {.line-numbers}
const user1 = {
    name:"Eric"
}
console.log(user1.name); // Eric

user1.name = "Polo"
console.log(user1.name); // Polo
```


### 如果要將物件複製(傳值)給另一個變數

可以先創建一個新的物件,在傳遞所有屬性 

```js {.line-numbers}
let user1 = {
    name:"Eric"
}
let user2 = {}

for (key in user1){
    user2[key] = user1[key]
}

user1.name = "Polo"
console.log(user2.name) // Eric
console.log(user1.name) // Polo

```

或是使用 Object.assign

```js {.line-numbers}
Object.assign(要存入的物件,[ 導入的物件1, 導入的物件2, 導入的物件3...])
```

把上一個方式改用 Object.assign 的寫法

```js {.line-numbers}
let user1 = {
    name:"Eric"
}
let user2 = {}

Object.assign(user2,user1)
console.log(user2); //{name: "Eric"}
console.log(user1 === user2); // false 成功複製
```

當然也可以直接賦予
```js {.line-numbers}
let user1 = {
    name:"Eric"
}
let user2 = Object.assign({},user1)

console.log(user2); //{name: "Eric"}
console.log(user1 === user2); // false 
```

---

### 回收

只要物件無法被存在於全域變數訪問,那麼引擎會自動啟用回收機制,把引擎認為是垃圾的數據給回收.(釋放記憶體)

今天有一個物件,並有一個 user 變數指向這個物件,這個物件就不會被JS引擎回收,如下圖

```js{.line-numbers}
let user = {
    name:"Eric"
}
```
但如果之後這個變數取消指向這個物件,那麼這個物件就會因為引擎覺得這個是沒有用的數據內容而回收

```js{.line-numbers}
let user = null;
```

如果今天有兩個變數指向這個物件,但後來 user 取消指向這個變數, admin 一樣可以訪問到這個物件

```js{.line-numbers}
let user = {
    name:"Eric"
}

let admin = user
user = null
console.log(admin) // {name:"Eric"}
```

---

## 物件自動轉換

一般型別會因為運算符的關係而改變型別
```js{.line-numbers}
typeof ("9"-"2") //number
```

物件可以用`Symbol`裡面的一種方法來判斷要如何輸出,
而輸出你提供的條件相對應的型別

### `Symbol.toPrimitive`

可以將這個方法寫入物件,因為是`Symbol`,必須要用方括號來調用

```js{.line-numbers}
obj[Symbol.toPrimitive] = function(hint) {
  // 判斷條件 並回傳一個期望輸出的值
  // hint = "string"、"number" 和 "default" 其中一個
}
```


有三種變換的`hints`
1. `string`

```js{.line-numbers}
alert(obj)
otherObj[obj] // 把物件作為其他物件的 key 
```
2. `number`
```js{.line-numbers}
let num = Number(obj);

// 數學運算 除了二元加法
let n = +obj; // 一元加法
let delta = date1 - date2;
// 比較
let greater = user1 > user2;
```
3. `default`

```js{.line-numbers}
// 不確定的期望的類型 二元加法
let total = obj1 + obj2;
// 判斷相等
if (user == 1) { ... };
```

使用範例

在一個物件新增一個`[Symbol.toPrimitive](hint)`的方法後,提供條件,如果`hint`等於`string`,就輸出`name`的值,否則都輸出`money`的值

```js{.line-numbers}
let user = {
  name: "John",
  money: 1000,

  [Symbol.toPrimitive](hint) {
    console.log(`hint: ${hint}`);
    return hint == "string" ? this.name : this.money;
  }
};

alert(user); // hint: string -> "John"
alert(+user); // hint: number -> 1000
alert(user + 500); // hint: default -> 1500
```

如果沒有使用`[Symbol.toPrimitive](hint)`的方法,那就會用物件裡都有個方法`valueOf`和`toString`


### toString/valueOf

- 類似於需要字串的轉換
   - 會先使用 `toString`
- 其他情況的轉換
   - 使用`valueOf`

跟`[Symbol.toPrimitive](hint)`一樣,需在物件內寫判斷,才會有作用

```js{.line-numbers}
let user = {name: "Eric"}; //沒寫判斷

alert(user); // [object Object]  使用 toString 轉成字串了 
console.log(-user) // NaN 其他狀況使用 valueOf , 變成 -{name: "Eric"} , 所以回傳 NaN

console.log(user.toString()) // [object Object]
console.log(user.valueOf()) // {name: "Eric"}

```

寫判斷後,就會依照回傳需求值,而且還能直接運算

```js{.line-numbers}
let user = {
        name: "Eric",
        money: 1000,
        toString(){
            return this.name
        },
        valueOf(){
            return this.money
        }
    };

console.log(user); // "Eric"
console.log(user*2); // 2000

```
