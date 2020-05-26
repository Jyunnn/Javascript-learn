# 原始型別方法

## 原始型別
Javascript有以下幾種型別
`string` `number` `bigint` `boolean` `symbol` `null` `undefined` `object`
其中除了 `object` 是物件型別,之外其他都為原始型別

`object`可以儲存多個鍵`key`與其值`value`
然後用`[]`或`.`來調用裡面的鍵取其值

後來因為使用者想對字串或數字做其他事情,就變成原始型別可以做類似物件呼叫方法(函式),例如:

```js {.line-numbers}
let name = 'eric'
console.log(name.toUpprtCase()) // 'ERIC'
```

雖然原始型別看起來變得像物件型別一樣可以,但是它依然是原始型別, `string` `number` `boolean` `symbol` 有他們自己專用的方法可以使用.

原始型別調用方法的流程如下
1. 先創建一個包含字串值的特殊物件,裡面有`toUpprtCase()`這個函式.

2. 這個函式會回傳一個處理過後新的字串 (上個例子是回傳到`console.log` 並顯示 )

3. 剛剛創建的特殊物就會被銷毀,留下原始字串值

---

## 函式構造器

我們也可以使用構造器 `new` 來創建原始型別,但不太建議用這個方法,因為有可能會出錯

```js {.line-numbers}
console.log( typeof 1) // 'number'
console.log( typeof new Number(1)) // 'object'

let a = new Number(1)
if(a){
    console.log("Hi")
}
// 一定會顯示 Hi , 因為物件轉換成 'ture'
```

如果不用構造器 , 只單純使用`String/Number/Boolean`函數 ,這個就不會發生上列的情況,就會單純的轉換型別(前提是合理的轉換)

>null和undefined 沒有函式方法可以使用
 