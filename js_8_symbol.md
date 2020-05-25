# Symbol (標示符)
### 定義
在規範中物件的key只能是字串或是`Symbol`
`Symbol` 可以用 `Symbol()` 來創建

```js {.line-numbers}
let id = Symbol("id");
```

`Symbol` 是唯一的,如果創建同一個敘述的 `Symbol`


```js {.line-numbers}
let id1 = Symbol("id");
let id2 = Symbol("id");
console.log(id1==id2) //false
```

依據型別自動轉換,如果今天用 `alert()` 來輸出一個數字,那個數字會被轉為字串輸出,但`Symbol`是不會被自動轉換,如果真的要使用的話,可以使用`symbol.description`

```js {.line-numbers}
alert(id1) //Cannot convert a Symbol value to a string

alert(id1.description) //id
```


### 用於物件屬性(key)

使用`Symbol`便無法使用`.`來訪問
必須使用方括號`[]`

```js {.line-numbers}
let user = {
    name:"Eric"
};

let id = Symbol("id");
user[id] = 1;
console.log(user[id]) // 1
console.log(user.id) // undefined
```

因為`id`是一個變數,就必須要用方括號

如果用字串來新增,也不會複寫到剛剛創建的`Symbol`
```js {.line-numbers}
user.id = 256;
console.log(user[id]) // 1
console.log(user.id) // 256
```

#### 無法在`for...in`中顯示

用`Symbol`新增的屬性無法在`for...in`顯示
```js {.line-numbers}
for(key in user){
    console.log(key) // name
}
```

也無法用`Object.keys(user)`來顯示它們,因為用`Symbol`創建的物件屬性是屬於隱藏的屬性,這個是隱藏標示的原則


之前有提到物件可以用`assign`來複製一份新的物件,`Symbol`可以被`assign`方法複製
```js {.line-numbers}
let id = Symbol("id");
let user = {
  [id]: 1
};

let clone = Object.assign({}, user);

console.log(clone[id]) //1
```


### 全域中的symbol

在剛剛的範例中,了解到`symbol`是唯一的,但有時候需要可以指向一樣的`symbol`,這時就必需建立一個全域的`symbol`

全域的`symbol`需要用`Symbol.for(key)`來建立,如果已經建立,使用這個方法則是讀取已建立的全域`symbol`

```js {.line-numbers}
let id1 = Symbol.for("id");
let id2 = Symbol.for("id");
console.log(id1 == id2) // true
```

結果與只使用`Symbol("id")`的結果是不一樣的


#### Symbol.keyFor

全域中的`symbol`可以使用`Symbol.keyFor`這個方法來反向取得描述值

```js {.line-numbers}
let id1 = Symbol.for("id");

console.log(Symbol.keyFor(id1)) // id
```