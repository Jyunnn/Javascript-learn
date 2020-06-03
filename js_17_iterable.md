# 可迭代物件

根據維基百科說明,迭代就是為了更接近目標或結果,每一次的過程就稱為一次==迭代==,每一次迭代的結果會替換掉上一次的迭代結果

可迭代與類陣列是不同的,等等會解釋

一般來說物件是沒辦法使用`for..of`來迭代,但是可以透過新增方法來讓物件變得可以迭代

## `Symbol.iterator`

設有一個物件`objRange`裡面有兩組`keys`和`values`

```js {.line-numbers}
let objRange = {
    from: 1,
    to: 6
};
```
但這樣是沒有辦法迭代,會顯示錯誤
必須要加入`Symbol.iterator`這個方法
當你使用`for..of`時,會先調用`Symbol.iterator`這個方法,如果沒有就會報錯,這個方法需回傳迭代物件(裡面包含一個`next()`方法)


```js {.line-numbers}
let objRange = {
  from: 1,
  to: 5
};

// 1. for..of 會先執行這個
objRange[Symbol.iterator] = function() {

  // 回傳一個迭代物件（iterator object）
  // 2. for..of 只與這個 iterator一起執行
  return {
    iteratorFrom: this.from,
    iteratorTo: this.to,

    // 3. next() 在 for..of 的每一次迴圈迭代中執行
    next() {
      // 4. 會回傳 {done:.., value :...} 格式的物件
      if (this.iteratorFrom <= this.iteratorTo) {
        return { done: false, value: this.iteratorFrom++ };
      } else {
        return { done: true };
      }
    }
  };
};

for (let num of objRange) {
  console.log(num); // 1, 然後 2, 3, 4, 5
}
```

這個方法是要自行建立的,`range`物件本身沒有`[Symbol.iterator]`這個方法,這個方法會回傳一個可迭代物件.也可以整理一下寫法,直接在物件內新增方法.

```js {.line-numbers}
let objRange = {
  from: 1,
  to: 5,

  [Symbol.iterator]() {
      this.iteratorFrom = this.from
      return this;
  },

  next() {
    if (this.iteratorFrom <= this.to) {
      return { done: false, value: this.iteratorFrom++ };
    } else {
      return { done: true };
    }
  }
};

for (let num of objRange) {
  console.log(num);
}
```

但這個方法用的`this`對象是自己,所以會新增一個`iteratorFrom`在物件裡面
```js {.line-numbers}
// 接上
console.log(objRange);
// {from: 1, to: 5, iteratorFrom: 6, next: ƒ, Symbol(Symbol.iterator): ƒ}
```

---

字串是可以直接使用`for..of`迭代

```js {.line-numbers}
for (str of 'Eric'){
  console.log(str); // E 然後分別輸出 r i c
}
```


## 可迭代(Iterable)與類陣列(Array-like)

- `Iterable`是內有`Symbol.iterator`方法使用的物件
- `Array-like`是有`key`和`length`屬性的物件,不可迭代,但字串可以
 (字串有`length`也有`key`)