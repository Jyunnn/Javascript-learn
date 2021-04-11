# WeakMap/WeakSet

## 前言

之前有提過如果值有被參考,那麼就不會被引擎當作垃圾回收

```js {.line-numbers}
let john = {name: "John"};
let array = [ john ];
john = null; // 覆蓋對 {name: "John"} 的參考
```

因為`{name: "John"}`被儲存在陣列中,所以不會被引擎回收掉
如果用`Map`新增鍵與值,如果該`map`存在,也不會被引擎回收

```js {.line-numbers}
let newMap = new Map()
let user = 'name'
newMap.set(user,'Eric')
user = null // 覆蓋'name'
```

## WeakMap

`WeakMap`和`Map`的結果就不一樣了,該回收的還是會被回收

`WeakMap`的鍵必須要是物件,不可以是原始值

```js {.line-numbers}
let user = {name: 'Eric'}
let newMap = new WeakMap()
newMap.set(user,'Eric')

user = null; // 覆蓋對 {name: 'Eric'} 的參考
// user 就完全從記憶體中刪除
```

`WeakMap`只有這幾種方法

- `weakMap.get(key)`
- `weakMap.set(key, value)`
- `weakMap.delete(key)`
- `weakMap.has(key)`

## WeakSet

`WeakSet`也是一樣,只能增加物件,且物件只有在有被其他地方參考才能被存在`set`中

- `weakSet.set(key, value)`
- `weakSet.delete(key)`
- `weakSet.has(key)`

```js {.line-numbers}
let visitedSet = new WeakSet();

let john = { name: "John" };
let pete = { name: "Pete" };
let mary = { name: "Mary" };

visitedSet.add(john); // John 進入網站
visitedSet.add(pete); // Pete 進入網站
visitedSet.add(john); // John 再次進入
// visitedSet 目前有兩個人進入網站

john = null;
// visitedSet 將自動清理 john
```