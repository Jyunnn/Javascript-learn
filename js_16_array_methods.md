# 陣列方法 (重要)

先前有提到新增值的方法,本篇這些在未來也會經常使用

- `array.push()`
- `array.pop()`
- `array.shift()`
- `array.unshift()`

## 刪除陣列值 `splice`

`delete`也能在陣列中使用,但是會有個問題

```js {.line-numbers}
let arr = ['alpha','bravo','charlie'];
delete arr[1];
console.log(arr, arr.length)// ["alpha", undefined, "charlie"] , 3
```

陣列值的數量依然是3個,且刪除的直接變成 `undefined`
因此我們應該要使用`splice`

```js {.line-numbers}
arr.splice(index[, deleteCount, elem1, ..., elemN])
```

語法解釋為: 在`arr`中,從`index`開始,刪除`deleteCount`個值,並在當下的位置新增`elem1, ..., elemN`,然後回傳**被刪除的值(這個值為陣列)**

```js {.line-numbers}
let arr = ['alpha','bravo','charlie'];
let del = arr.splice(1, 1, 'B', 'C')

console.log(del) // ["bravo"] 被刪除的
console.log(arr) // ["alpha", "B", "C", "charlie"]
```

當然我們也能把刪除數量`deleteCount`設為`0`,做為在陣列內指定的排序後新增值

```js {.line-numbers}
let arr = ['alpha','bravo','charlie'];
let del = arr.splice(1,0,'B','C')

console.log(del) // [] 沒刪除任何東西
console.log(arr) // ["alpha", "B", "C", "bravo", "charlie"]
```

## 抓取複製 `slice`

```js {.line-numbers}
arr.slice([start], [end])
```

語法解釋為: 這個方法會回傳一個陣列,其陣列值為`arr`內,從`start`到`end`之前(就是不包含`end`的意思),也可以是負數,負數會從尾端算起

```js {.line-numbers}
let arr = ['alpha','bravo','charlie'];
console.log(arr.slice(1, 2)) // ["bravo"]
console.log(arr.slice(-2)) // ["bravo", "charlie"]
```

## 創建複製並新增 `concat`

```js {.line-numbers}
arr.concat(arg1, arg2...)
```

語法解釋為:這個會回傳一個新的陣列,其值為`arr`的值和`arg1, arg2...`的集合

```js {.line-numbers}
let arr = ['alpha','bravo','charlie'];
let arr2 = ['A','B']
let arr3 = ['a','b']

let n = arr.concat(arr2,arr3)

console.log(n) // ["alpha", "bravo", "charlie", "A", "B", "a", "b"]
```

如果是類陣列`(arrayLike)` 那將會把這個類陣列以物件的方式直接放入陣列中

```js {.line-numbers}
let arr = ['alpha','bravo','charlie'];
let arraylike = {
    0:'A',
    length: 1
}

let n = arr.concat(arraylike)
console.log(n) // ["alpha", "bravo", "charlie", {0: "A", length: 1}]

```

但是類陣列中有`[Symbol.isConcatSpreadable]`這個值的話,會直接被當作陣列一樣,僅傳入其值

```js {.line-numbers}
let arr = ['alpha','bravo','charlie'];
let arraylike = {
    0:'A',
    [Symbol.isConcatSpreadable]: true,
    length: 1
}

let n = arr.concat(arraylike)
console.log(n) // ["alpha", "bravo", "charlie", "A"]

```

## 遍歷陣列值 `forEach`

```js {.line-numbers}
arr.forEach(function(item, index, array) {
  // ... do something with item
});
```

語法解釋: 這個方法不會回傳值, 可以對`arr`陣列的值做操作,`item`為`arr`內的值,`index`為索引(鍵),`array`則為自身陣列`arr`

```js {.line-numbers}
let arr = ['alpha','bravo','charlie'];

arr.forEach((item,index,array) => {
    console.log(`第${index}個為${item},在${array}中`)
})
// 第0個為alpha,在alpha,bravo,charlie中
// 第1個為bravo,在alpha,bravo,charlie中
// 第2個為charlie,在alpha,bravo,charlie中
```

## 在陣列中搜尋

### indexOf/lastIndexOf/includes

- `arr.indexOf(item, from)`
從`from`開始搜尋`item`,如果找到則回傳索引(鍵),沒有的話回傳`-1`
- `arr.lastIndexOf(item, from)`
與`indexOf`相同,但是是由右至左搜尋
- `arr.includes()`
從`from`開始搜尋`item`,如果找到則回傳`true`,沒有的話就回傳`false`

```js {.line-numbers}
let arr = ['alpha','bravo','charlie'];

console.log(arr.indexOf('bravo')); // 1
console.log(arr.includes('alpha')); // true
```

`includes`可以處理`NaN`

```js {.line-numbers}
let arr = [NaN];
console.log(arr.includes(NaN)); // true
```

### find/findIndex

```js {.line-numbers}
let result = arr.find(function(item, index, array) {
    return 條件
});
```

`item`為陣列的值
`index`為陣列的索引
`array`為陣列本身

這個方法需要回傳,如果條件結果為`true`就回傳`item`,並停止搜尋
如果結果為`false`,則回傳`undefined`

```js {.line-numbers}
let arr = [10,15,3,8,19];
let findNum = arr.find((e)=>{
   return e > 11
})
console.log(findNum) // 15  (第一個符合條件的)
```

同樣也能用在陣列值為物件上

```js {.line-numbers}
let users = [
    {id: 1,name: "Eric"},
    {id: 2,name: "Polo"},
    {id: 3,name: "Kevin"},
]

let findUser = users.find((e)=>{
    return e.id == 2
})

console.log(findUser.name); // 'Polo'
```

`findIndex`與`index`相同,但如字面上,回傳的是符合條件的索引

### 過濾 filter

```js {.line-numbers}
let result = arr.filter(function(item, index, array) {
    return 條件
});
```

`filter`會回傳一個陣列,並把符合條件的值`push`到該陣列中,並不會像`find`一樣,遇到`true`就停止,而是會尋找到最後.

```js {.line-numbers}
let users = [
    {id: 1,name: "Eric"},
    {id: 2,name: "Polo"},
    {id: 3,name: "Kevin"},
    {id: 4,name: "Lisa"},
    {id: 5,name: "Linma"},
]

let findUser = users.filter((e)=>{
    return e.id > 3
})

console.log(findUser); // [{id: 4, name: "Lisa"},{id: 5, name: "Linma"}]

```

## 陣列操作轉換

### map 操作

```js {.line-numbers}
let result = arr.map(function(item, index, array) {
  // 返回新值而不是当前元素
})
```

可以對陣列內所有值做操作,並回傳操作後的新陣列

```js {.line-numbers}
let arr = [2,4,5,6,8]

let newArr = arr.map((item)=>{
    return item * 2
})

console.log(newArr); // [4, 8, 10, 12, 16]
```

### sort(fn) 重新排序

參數內的函數可以選擇是否要使用,如果沒有使用,那們陣列內的值就會使用**Unicode**排序,如果有使用,這個有一個規則

1. `fn(a, b)`小於 0 , 則 a 會被排到 b 前面
2. `fn(a, b)`等於 0 , 則 a 和 b 位置不變
3. `fn(a, b)`大於 0 , 則 b 會被排到 a 前面

```js {.line-numbers}
let arr = [9,2,7,6,4,8,3]

function compareNumber(a, b){
    if (a > b) return 1;
    if (a == b) return 0;
    if (a < b) return -100
}

arr.sort(compareNumber)
console.log(arr); // [2, 3, 4, 6, 7, 8, 9]
```

但事實上只要回傳的是正整數,就是大於;負數就是小於
所以對於數字比較最快的寫法就是

```js {.line-numbers}

arr.sort((a, b)=> a -b )
console.log(arr); // [2, 3, 4, 6, 7, 8, 9]
```

### reverse 反轉

會把陣列內的值做反轉,最後的會到最前端,最前端的會到最後端

```js {.line-numbers}
let arr = [9,2,7,6,4,8,3]
arr.reverse()
console.log(arr); // [3, 8, 4, 6, 7, 2, 9]
```

### split 分割 / join 接合

`str.split([separator[, limit]])`可以將一個字串依照指定`separator`切割,並回傳切割後的陣列,`limit`是回傳後的數量限制

```js {.line-numbers}
let names = 'Eric, kevin, Polo';
let arr = names.split(', '); //逗點後面有空白,用這樣條件切割
console.log(arr); // ["Eric", "kevin", "Polo"]
```

```js {.line-numbers}
let names = 'Eric,kevin,Polo'; // 把空白去掉
let arr = names.split(',',1); // 用逗點來切割,並回傳一個值就好
console.log(arr); // ["Eric"]
```

```js {.line-numbers}
let names = 'Eric'
let arr = names.split(''); // 空值
console.log(arr); // ["E", "r", "i", "c"]  // 全切割
```

`arr.join([separator])`剛好相反,可以把陣列值用`separator`接合起來

```js {.line-numbers}
let arr = ["E", "r", "i", "c"];
let names = arr.join("") // 中間不含任何字元接合
console.log(names);  // Eric
```

### reduce/reduceRight

`arr.reduce(callback(accumulator, currentValue[, index[, array]])[, initialValue])`

這個方法比較複雜點

- accumulator 函式上一個結果,如果有提供`initialValue`參數,第一次則會使用這個當作初使值

- currentValue 當下的陣列值

```js {.line-numbers}
let arr = [2,4,5,6,8,7,9]

let news = arr.reduce(function(last,item,index,arr){
    console.log(last,item,index,arr); // 結果有點長,執行看看
    return last + item
},0) // initialValue 為 0

console.log(news); // 41
```

首先,有設定`initialValue`參數為`0`

1. 第一遍的時候 `last` 套用初始值 `initialValue` 為 `0` , 當下`item`為`2` , 兩者相加回傳 `2`

2. 第二遍時`last`套用上個回傳值`2`,當下`item`為`4`,兩者相加回傳 `6`
`...中間略過`
3. 最後求得總和`41`,並回傳該值

`reduceRight`也是相同用法,但是流程是由右至左
