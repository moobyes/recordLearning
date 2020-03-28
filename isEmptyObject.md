# 判断Object是否为空的方法

## 1. 字符串方法

将json对象转化为json字符串，再判断该字符串是否为"{}"
```js
let obj = {}
let b = (JSON.stringify(obj) === "{}")
console.log(b) //true
```

## 2. for in 循环

> 这个方法有一定的局限，Object.create(null)创建对象的时候就不能用for...in判断了。
```js
let obj = {}
let b = () => {
	for(var key in obj) {
		return false
	}
	return true
}
console.log(b()) //true
```

## 3. Object.getOwnPropertyNames()方法

此方法是使用Object对象的getOwnPropertyNames方法，获取到对象中的属性名，存到一个数中，返回数组对象，我们可以通过判断数组的length来判断此对象是否为空
注意：此方法不兼容ie8

```js
let obj = {}
let arr = Object.getOwnPropertyNames(obj)
console.log(arr.length === 0) //true
```

## 4. 使用ES6的Object.keys()方法

与4方法类似，是ES6的新方法, 返回值也是对象中属性名组成的数组

```js
let obj = {}
let arr = Object.keys(obj)
console.log(arr.length === 0) //true
```

在Jquery 里有一个方法，源码如下：

```js
isEmptyObject: function( obj ) {
  for ( var name in obj ) {
  	return false
  }
  return true;
}
```

居然和我们的方法2相差仿佛！
下面我们写一个自己的isEmptyObject方法：

```js
const isEmptyObject = (obj) => {
	const result = obj.toString()
	if (result !== '[object object]') {
		throw new Error('不是真实对象！')
	}
	const keys = Object.keys(obj)
	if (keys.length === 0) {
		return trues's
	} else {
		return false
	}
}
```