# 構造器 New

- 需用大寫字母開頭
- 需用`new`來創建

```js{.line-numbers}
function User(name,age){
    this.name = name;
    this.age = age
}

let user1 = new User("Eric",20)
console.log(user1) //  {name: "Eric", age: 20}
```

當函數使用`new`的創建流程
1. 會先建立一個空物件,並將`this`指向這個物件
2. 開始執行時,會依據內容建立鍵值(key)
3. 最後回傳`this` (即物件)

基本上結果就與物件是一樣的
```js{.line-numbers}
let user1 = {
    name:"Eric",
    age:20
}
```
差別在於閱讀性和便捷性