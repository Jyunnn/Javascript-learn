# 解構賦值

可以將物件或陣列拆開,並賦予於一串變數

```js {.line-numbers}
let arr = ["Eric", "Kevin"]
let [user1, user2] = arr

console.log(user1, user2);// "Eric", "Kevin"
```

文字的部分也可以跟`split()`一起使用

```js {.line-numbers}
let [firstName, lastName] = "Eric ,Chen".split(' ,');
// "Eric" "Chen"
```

如果今天賦予值太多,可以使用`...`並再加入一個參數,將剩餘的值包成陣列賦予給這個有`...`的參數

```js {.line-numbers}
let [one, two, three, ...other] = [1, 2, 3, 4, 5, 6, 7, 8]
console.log(one, two, three, other); // 1, 2, 3, [4, 5, 6, 7, 8]
```

如果賦予值是空的,那被賦予的變數將會是`undefined`

```js {.line-numbers}
let [one, two] = []
console.log(one, two); // undefined undefined
```

