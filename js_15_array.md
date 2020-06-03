# Array 陣列

## 建立
兩種建立的方法
```js {.line-numbers}
let arr = new Array();
let arr = [];
```

## 獲取
第一個序列是`0`

```js {.line-numbers}
let arr = ['alpha','bravo','charlie'];
console.log(arr[0]) //'alpha'
```

使用`alert`可以完全顯示陣列內所有的值(雖然實用性不高)
```js {.line-numbers}
alert(arr) // alpha,bravo,charlie
```

---
## 陣列方法 pop/push, shift/unshift

先簡單提起程式語言中,引擎處理陣列的兩個方式

### Queue
中文翻譯是對列,資料結構是水平排列,資料先放進就先出`（First-In-First-Out）`
`push`在最尾端添加一個值
`shift`取出最前端的值,後面的全部往前移,原本第二個值就變第一個

### Stack 
堆疊就像一副撲克牌,資料疊再一起,越底層的資料序列越前面,越上層序列就越尾端,也就是最後放進去的是最先接收的`(Last-In-First-Out)`
`push`在最尾端增加一個值
`pop`在最尾端取出一個值

---
Javascript中陣列可以作為`Queue`也能作為`Stack`來處理,這個又稱做`Double-ended queue`(雙端隊列)


### `pop` 取出並回傳最後一個值
```js {.line-numbers}
let arr = ['alpha','bravo','charlie'];
console.log(arr.pop()) // charlie
console.log(arr) // ["alpha", "bravo"]
```

### `push` 在陣列最後新增值
~可以一次新增多個值~
```js {.line-numbers}
let arr = ['alpha','bravo'];
arr.push('charlie')
console.log(arr) // ["alpha", "bravo","charlie"]
arr.push('delta','echo') //也可以新增多個
console.log(arr) // ["alpha", "bravo", "charlie", "delta", "echo"]
```

### `shift` 取出並回傳第一個值
```js {.line-numbers}
let arr = ['alpha','bravo','charlie'];
console.log(arr.shift()) // alpha
console.log(arr) // ["bravo","charlie"]
```

### `unshift` 在陣列最前端新增值
~可以一次新增多個值~
```js {.line-numbers}
let arr = ['bravo','charlie'];
arr.unshift("alpha") 
console.log(arr) // ["alpha", "bravo","charlie"]
```

性能上面肯定是`pop`和`push`比較快
因為`shift`和`unshift`多了還要移動陣列內其他的值(因為都是取出新增最前段,後段的值必然需要移動)
這些都會需要更多的記憶體處理

---

## 特性

陣列也是物件,特性也跟物件一樣,屬於傳址

```js {.line-numbers}
let arr = ['alpha','bravo','charlie'];
let arr2 = arr; // 傳址複製
console.log(arr == arr2) // true
arr2.push('delta')
console.log(arr) // ["alpha", "bravo", "charlie", "delta"]
```

陣列可以跳序新增

```js {.line-numbers}
let arr = ['alpha','bravo','charlie'];
arr[99] = 'error'
console.log(arr) ["alpha", "bravo", "charlie", empty × 96, "error"]
console.log(arr.lenght) // 100
```
---

## `for`循環

`for..of`可以取陣列內所有的值

```js {.line-numbers}
let arr = ['alpha','bravo','charlie'];

for(value of arr){
    console.log(value); // alpha ; bravo ; charlie
}
```

`for..in`可以取陣列內的索引

```js {.line-numbers}
let arr = ['alpha','bravo','charlie'];

for(key in arr){
    console.log(arr[key]); // alpha ; bravo ; charlie
}
```

但是不建議用這個方式,因為還有一種類陣列（Array-Like)

```js {.line-numbers}
let arrayLike = {
    0:'alpha',
    1:'bravo',
    length: 2
}

//類陣列就是像這樣的東西
```

通常是在DOM操作時會遇到,如果用這個方法會把一些不想要顯示的方法給列出來

```js {.line-numbers}
for(key in arrayLike){
    console.log(arrayLike[key]); // "alpha" , "bravo" , 2  
}
```

## `length`

```js {.line-numbers}
let arr = [1,2,3,4,5];
arr.length = 2; // 把陣列截掉剩下2個值
console.log(arr) // [1,2]

arr.length = 5; // 加回來
console.log(arr) // [1, 2, empty × 3]  原本的值不見了

arr.length = 0;
console.log(arr) // [] , 清空陣列
```