# 从头学习JS 第 2 天

## 数组

### 创建数组

在 JavaScript 中有多种方式可以创建数组，最直接的方式是把数组字面量赋值给一个变量。

```javascript
  const arr = [1, 2, 3, 4 ,5];
```

也可以使用 Array 构造函数来创建数组。

```javascript
  const arr = new Array(1, 2, 3, 4 ,5);
```

> 注意：new Array(2) 会创建一个长度为 2 的空数组，然而 new Array(1,2) 则会创建一个包含两个元素（1 和 2）的数组。