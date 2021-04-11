# Map & Set

## Map 
### 基礎

這個是ES6新增的內容,
看起來會覺得跟物件很像
但還是有差異

`Map`是一個有帶`key`的集合

```js {.line-numbers}
let newMap = new Map();

newMap.set('1', 'string1');   // 字串key
newMap.set(1, 'number1');     // 數字key
newMap.set(true, 'boolean1'); // 布林key

console.log( newMap.get('1') ); // 'string1'
console.log( newMap.get(1)   ); // 'number1'
console.log( newMap.size ); // 3
```
首先用函式建構建立一個`newMap`
並用`set`儲存`key`和`value`
最後再用`get`回傳該`key`的`value`

---

- `new Map()`  新增一個`map`
- `map.set(key, value)`  儲存該`key`與`value`
- `map.get(key)` 依據該`key`回傳`value`, 如果沒有這個`key`, 就回傳`undefined`
- `map.has(key)` 如果有這個`key`, 就回傳`true`, 反之回傳`false`
- `map.delete(key)` 刪除這個`key`的值
- `map.clear()` 清空 `map`
- `map.size` 回傳當下值的數量


---

`map`的`key`不會像物件一樣轉為`string`

```js {.line-numbers}
// 接上
console.log( newMap.get('1') ); // 'string1'
console.log( newMap.get(1)   ); // 'number1'
```

`map`也能用物件當作`key`

```js {.line-numbers}
// 接上
let user = {
  1:"Eric"
}

newMap.set(user,'KKman')
console.log(newMap.get(user)); // 'KKman'
```

`map`可以像jQuery一樣用鏈式寫法

```js {.line-numbers}
newMap.set(user,'KKman')
      .set(2,'number2')
```

---

### 迭代


如需要遍歷`map`,


`map.keys()` 遍歷並回傳所有的`key`
`map.values()` 遍歷並回傳所有的`value`
`map.entries()` 遍歷並回傳所有的新增的`key`與`value`,使用在`for..of`的默認值

```js {.line-numbers}
let newMap = new Map();

newMap.set('Eric', 28)
      .set('Polo', 54)
      .set('Kevin', 27);

console.log(newMap.keys()); // {"Eric", "Polo", "Kevin"}
console.log(newMap.values()); // {28, 54, 27}
console.log(newMap.entries()); // {"Eric" => 28, "Polo" => 54, "Kevin" => 27}
```

使用`for..of`遍歷所有的`key`

```js {.line-numbers}
for (let user of newMap.keys()){
  console.log(user); // "Eric"  "Polo"  "Kevin"
}
```

使用`for..of`遍歷所有的`value`

```js {.line-numbers}
for (let user of newMap.values()){
  console.log(user); // 28 54 27
}
```

使用`for..of`遍歷

```js {.line-numbers}

for (let user of newMap){
  console.log(user); // ["Eric", 28] ["Polo", 54] ["Kevin", 27]
}

```

`map`有內建的`forEach`方法

```js {.line-numbers}
newMap.forEach(function(v, i, arr){
  console.log(`${v} for ${i}`);
})
```


### 物件創建 Map - Object.entries

新增一個`Map`時可以在參數帶入一個陣列,直接新增`key`與`value`

```js {.line-numbers}
let userAge = new Map([
  ['Eric', 28],
  ['Polo', 54],
  ['Kevin', 27]
]);

console.log(userAge.get('Eric')); // 28
```

如果要用物件來建立一個`Map`,可以使用`Object.entries(obj)`這個方法

```js {.line-numbers}
let users = {
  'Eric': 28,
  'Kevin': 16,
}

let userAge = new Map(Object.entries(users));
console.log(userAge.get('Eric')); // 28
console.log(userAge.entries()) // {"Eric" => 28, "Kevin" => 16}
```

### Map創建Object - Object.fromEntries

這個方法剛好與`Object.entries`相反,是利用`Map`格式轉回`object`

```js {.line-numbers}
// 接上
let newObj = Object.fromEntries(userAge) // 默認 userAge.entries()
console.log(newObj); // {Eric: 28, Kevin: 16}
```


## Set
### 基礎

`Set`的特性就是,如果今天一直重複新增同樣的值,`Set`並不會重複新增,也就是不會重複紀錄這個值
是一個只有帶`value`的集合

```js {.line-numbers}
let user = new Set();

user.add('Eric');
user.add('Eric');
user.add('Polo');

console.log(user); // {"Eric", "Polo"}  沒有重複 'Eric'
```

- `new Set(iterable)`  新增一個`set`,如果有`iterable`物件,就可以將此複製到`set`
- `set.add(value)`  新增一個值,並回傳`set`本身
- `set.delete(value)`  刪除值,如果有這個值就回傳`true`,反之回傳`false`
- `set.has(value)`  如果`value`在`set`裡面,就回傳`true`,反之回傳`false`
- `set.clear`  清空`set`
- `set.size`  回傳`set`的數量


### 迭代

可以用`for..of`或是`forEach`來遍歷

```js {.line-numbers}
// 接上
for(name of user){
  console.log(name); // Eric  Polo
}

user.forEach((v)=>{
  console.log(v); // 結果跟上面的一樣
})
```