# 快照 vs 最新值
## jser经典一坑
```js
  function t1(){
    for (var i = 0; i< 9; i++) {
      setTimeout(() => console.log(i));
    }
  }
  t1();
  // 9
  // 9
  // 9
  // 9
  // 9
  // 9
  // 9
  // 9
  // 9
```
解释: 

var变量只有函数作用域，没有块级作用域

### 爬坑之道：
1.  通过IIFE制造函数作用域
```js
  function t2(){
    for (var i = 0; i< 9; i++) {
      ((v) => setTimeout(() => console.log(v)))(i);
    }
  }
  t2();
  // 0
  // 1
  // 2
  // 3
  // 4
  // 5
  // 6
  // 7
  // 8
```
2.  通过bind制造函数作用域
```js
  function t3(){
    for (var i = 0; i< 9; i++) {
      setTimeout(((v) => console.log(v)).bind(null, i));
    }
  }
  t3();
  // 0
  // 1
  // 2
  // 3
  // 4
  // 5
  // 6
  // 7
  // 8
```

3.  通过setTimeout第三个参数制造函数作用域
```js
  function t4(){
    for (var i = 0; i< 9; i++) {
      setTimeout((v) => console.log(v), 0, i);
    }
  }
  t4();
  // 0
  // 1
  // 2
  // 3
  // 4
  // 5
  // 6
  // 7
  // 8
```

4.  let变量具有块级作用域
```js
  function t5(){
    for (var i = 0; i< 9; i++) {
      let v = i;
      setTimeout(() => console.log(v));
    }
  }
  t5();
  // 0
  // 1
  // 2
  // 3
  // 4
  // 5
  // 6
  // 7
  // 8
```

## 快照
```js
  function s1(){
    for (let i = 0; i< 9; i++) {
      setTimeout(() => console.log(i));
    }
  }
  s1();
  // 0
  // 1
  // 2
  // 3
  // 4
  // 5
  // 6
  // 7
  // 8
```
## 最新值
```js
  function c1(){
    for (var i = 0; i< 9; i++) {
      setTimeout(() => console.log(i));
    }
  }
  c1();
  // 9
  // 9
  // 9
  // 9
  // 9
  // 9
  // 9
  // 9
  // 9
```

## 最新值 转 快照
爬坑之道给出了4种方法

## 快照 转 最新值
```js
  const ref = {current: null};
  function c2(){
    for (let i = 0; i< 9; i++) {
      ref.current = i;
      setTimeout(() => console.log(ref.current));
    }
  }
  c2();
  // 8
  // 8
  // 8
  // 8
  // 8
  // 8
  // 8
  // 8
  // 8
```

