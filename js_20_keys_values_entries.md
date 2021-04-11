# Object.keys, values, entries

在`Map & Set`章節中有提到這些方法,這些也能使用在物件上
這些方法帶入物件並回傳該物件鍵或值的陣列,是真正的`Array`

- `Object.keys(obj)` 回傳該物件`keys`的陣列
- `Object.values(obj)` 回傳該物件`values`的陣列
- `Object.entries(obj)` 回傳該物件`[key, value]`的陣列

```js {.line-numbers}
let users = {
    person01:'Eric',
    person02:'Polo',
    Person03:'Kevin'
}

console.log(Object.keys(users)); // ["person01", "person02", "Person03"]
console.log(Object.values(users)); // ["Eric", "Polo", "Kevin"]
console.log(Object.entries(users)); 
// [["person01", "Eric"], ["person02", "Polo"], ["Person03", "Kevin"]]
```
---

相反的,如果今天使用`Object.entries(obj)`將物件轉為陣列並用陣列方法對值做處理,在將此陣列轉回物件時,可以使用`Object.fromEntries`這個方法

```js {.line-numbers}
let products = {
    Apple: 10,
    Banana: 5,
    Orange: 8
}

// 轉換成 陣列並對值操作
let ProductTax = Object.entries(products).map(([key, value]) => [key ,value * 0.05 ])
// 轉回 物件
console.log(Object.fromEntries(ProductTax));
// {Apple: 0.5, Banana: 0.25, Orange: 0.4}
```

要注意`map`裡的參數, 因為`entries`回傳陣列的`value`是一個陣列,裡面是`[key, value]`

```js {.line-numbers}
Object.entries(products)
// [ ["Apple", 10], ["Banana", 5], ["Orange", 8] ]
```

所以`map`參數中必須要傳入的`value`就是一個陣列值`[key, value]`
