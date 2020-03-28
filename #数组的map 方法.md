#数组的map 方法

## map 的参数

map() 方法创建一个新数组，其结果是该数组中的每个元素都调用一个提供的函数后返回的结果。
就是说，用map方法的时候，数组的每一项值都会在它的参数fn里跑一遍，然后返回到一个新的数组里。

map 方法有两个参数：
1. 第一个参数：函数，改函数会对数组每一项都执行，它有三个参数：
	a）数组项的值
	b）数组项的下标
	c）数组本身
2. 指定this的作用域对象

用代码实现：
```js
	Array.map(function(value, index, Array){}, this)
```

具体使用实例：
```js
let nums = [1, 2, 3, 4, 5]
let newNums = []
newNums = nums.map(item => {
    return item + 1
})
console.log(nums) // [1, 2, 3, 4, 5]
console.log(newNums) // [2, 3, 4, 5, 6]
```

其他的使用方法：
```js
var map = Array.prototype.map
var a = map.call("Hello World", function(x) { 
  return x.charCodeAt(0); // 获取字符串中每个字符所对应的 ASCII 码,返回的是ASCII码组成的数组
})
// a的值为[72, 101, 108, 108, 111, 32, 87, 111, 114, 108, 100]

// 如何去遍历用 querySelectorAll 得到的动态对象集合
var elems = document.querySelectorAll('select option:checked');
var values = Array.prototype.map.call(elems, function(obj) {
  return obj.value;
})

// 反转字符串
var str = '12345';
Array.prototype.map.call(str, function(x) {
  return x;
}).reverse().join(''); 
// 输出: '54321'
```

map的实现：Polyfill
```js
// 实现 ECMA-262, Edition 5, 15.4.4.19
// 参考: http://es5.github.com/#x15.4.4.19
if (!Array.prototype.map) {
  Array.prototype.map = function(callback, thisArg) {

    var T, A, k;
    if (this == null) {
      throw new TypeError(" this is null or not defined");
    }
    // 1. 将O赋值为调用map方法的数组.
    var O = Object(this);
    // 2.将len赋值为数组O的长度.
    var len = O.length >>> 0;
    // 3.如果callback不是函数,则抛出TypeError异常.
    if (Object.prototype.toString.call(callback) != "[object Function]") {
      throw new TypeError(callback + " is not a function");
    }

    // 4. 如果参数thisArg有值,则将T赋值为thisArg;否则T为undefined.
    if (thisArg) {
      T = thisArg;
    }

    // 5. 创建新数组A,长度为原数组O长度len
    A = new Array(len);

    // 6. 将k赋值为0
    k = 0;

    // 7. 当 k < len 时,执行循环.
    while(k < len) {

      var kValue, mappedValue;

      //遍历O,k为原数组索引
      if (k in O) {

        //kValue为索引k对应的值.
        kValue = O[ k ];

        // 执行callback,this指向T,参数有三个.分别是kValue:值,k:索引,O:原数组.
        mappedValue = callback.call(T, kValue, k, O);

        // 返回值添加到新数组A中.
        A[ k ] = mappedValue;
      }
      // k自增1
      k++;
    }

    // 8. 返回新数组A
    return A;
  };      
}
```
