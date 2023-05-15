# 一、数组篇

## 1 \_.chunk(array, [size=1])

将数组（array）拆分成多个 size 长度的区块，并将这些区块组成一个新数组。 如果 array 无法被分割成全部等长的区块，那么最后剩余的元素将组成一个区块。

```js
let arr = [1, 2, 3, 4, 5, 6, 7, 8, 9];
_.chunk(arr, 2);
// => [[1, 2], [3, 4], [5, 6], [7, 8], [9]]

// 等价于
arr.reduce((acc, cur, index) => {
  if (index % 2 === 0) {
    acc.push([cur]);
  } else {
    acc[acc.length - 1].push(cur);
  }
  return acc;
}, []);
```

## 2 \_.compact(array)

创建一个新数组，包含原数组中所有的非假值元素。例如 false, null,0, "", undefined, 和 NaN 都是被认为是“假值”。

```js
let arr = [0, 1, false, 2, "", 3, null, undefined, NaN];
_.compact(arr);
// => [1, 2, 3]

// 等价于
arr.filter((item) => item);
```

## 3 \_.concat(array, [values])

创建一个新数组，将 array 与任何数组 或 值连接在一起。

```js
let arr = [1];
_.concat(arr, 2, [3], [[4]]);
// => [1, 2, 3, [4]]

// 等价于
arr.concat(2, [3], [[4]]);
```

## 4 \_.difference(array, [values])

创建一个具有唯一 array 值的数组，每个值不包含在其他给定的数组中。（注：即创建一个新数组，这个数组中的值，为第一个数字（array 参数）排除了给定数组中的值。）该方法使用 SameValueZero 做相等比较。结果值的顺序是由第一个数组中的顺序确定。

```js
let arr = [2, 1];
lei difference = [2, 3]
_.difference(arr, difference);
// => [1]

// 等价于
arr.filter((item) => !difference.includes(item));
```

## 5 \_.differenceBy(array, [values], [iteratee=_.identity])

这个方法类似\_.difference ，除了它接受一个 iteratee （注：迭代器）， 调用 array 和 values 中的每个元素以产生比较的标准。 结果值是从第一数组中选择。iteratee 会调用一个参数：(value)。（注：首先使用迭代器分别迭代 array 和 values 中的每个元素，返回的值作为比较值）。

```js
let add = [3.1, 2.2, 1.3];
let difference = [4.4, 2.5];
_.differenceBy(add, difference, Math.floor);
// => [3.1, 1.3]

// 等价于
add.filter((item) => !difference.map(Math.floor).includes(item));

_.differenceBy([{ x: 2 }, { x: 1 }], [{ x: 1 }], "x");
// => [{ 'x': 2 }]
```

## 6 \_.differenceWith(array, [values], [comparator])

这个方法类似\_.difference ，除了它接受一个 comparator （注：比较器），它调用比较 array，values 中的元素。 结果值是从第一数组中选择。comparator 调用参数有两个：(arrVal, othVal)。

```js
var objects = [
  { x: 1, y: 2 },
  { x: 2, y: 1 },
];
// isEqual 为自定义比较器
// 执行深比较来确定两者的值是否相等。
_.differenceWith(objects, [{ x: 1, y: 2 }], _.isEqual);
// => [{ 'x': 2, 'y': 1 }]

// 等价于
let isEqual = (value, other) => {
  if (value === other) return true;
  if (typeof value !== typeof other) return false;
  if (typeof value !== "object") return false;
  if (Array.isArray(value) !== Array.isArray(other)) return false;
  if (Object.keys(value).length !== Object.keys(other).length) return false;
  for (let key in value) {
    if (!isEqual(value[key], other[key])) return false;
  }
  return true;
};
objects.filter((item) => !isEqual(item, { x: 1, y: 2 }));
```

## 7 \_.drop(array, [n=1])

创建一个切片数组，去除 array 前面的 n 个元素。（n 默认值为 1。）

```js
_.drop([1, 2, 3]);
// => [2, 3]

// 等价于
[1, 2, 3].slice(1);
```

## 8 \_.dropRight(array, [n=1])

创建一个切片数组，去除 array 尾部的 n 个元素。（n 默认值为 1。）

```js
_.dropRight([1, 2, 3]);
// => [2, 3]

// 等价于
[1, 2, 3].shift();
```

## 9 \_.dropRightWhile(array, [predicate=_.identity])

创建一个切片数组，去除 array 中从 predicate 返回假值开始到尾部的部分。predicate 会传入 3 个参数： (value, index, array)。

```js
let arr = [1, 2, 3, 4];
_.dropRightWhile(arr, (item) => item > 2);
// => [1, 2]

// 等价于
arr.filter((item) => item <= 2);
```

## 10 \_.dropWhile(array, [predicate=_.identity])

创建一个切片数组，去除 array 中从起点开始到 predicate 返回假值结束部分。predicate 会传入 3 个参数： (value, index, array)。

```js
let arr = [1, 2, 3, 4];
_.dropWhile(arr, (item) => item < 3);
// => [3, 4]

// 等价于
arr.filter((item) => item >= 3);
```

## 11 \_.fill(array, value, [start=0], [end=array.length])

使用 value 值来填充（替换） array，从 start 位置开始, 到 end 位置结束（但不包含 end 位置）。

```js
let arr = [1, 2, 3];
_.fill(arr, "a");
// => ['a', 'a', 'a']

// 等价于
arr.fill("a");

_.fill(Array(3), 2);
```

<!-- ## 12 \_.findIndex(array, [predicate=_.identity], [fromIndex=0]) -->
