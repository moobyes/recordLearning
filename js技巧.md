

# ；js 技巧总计1

1. 判断对象的数据类型

```js
const isType = type => target => `[object ${type}]` === Object.prototype.toString.call(target)
const isArray = isType('Array')
console.log(isArray([]))
```

2. es5实现数组 map 方法

```js
const selfMap = function(fn, context) {
    let arr = Array.protoType.slice.call(this)
    let mappedArr = []
    for(let i = 0; i < arr.length; i++) {
        if (!arr.hasOwnProperty(i)) continue
        mappedArr.push(fn.call(context, arr[i], i, this))
    }
    return mappedArr
}
```

3. 使用reduce实现数组map方法

```js
const sefmap2 = function(fn, context) {
    let arr = Array.prototype.slice.call(this)
    return arr.reduce((pre, cur, index) => {
        return [...pre, fn.call(contetxt,cur, index, this)]
    }, [])
}
```

4. es5实现数组filter 方法

```js
const selfFilter = function (fn, context) {
    let arr = Array.prototype.slice.call(this)
    let filteredArr = []
    for (let i = 0; i < arr.length; i ++){
        if (!arr.hasOwnProperty(i)) continue
        fn.call(context, arr[i], i, this) && filteredArr.push(arr[i])
    }
    return filteredArr
}
```

5. 使用reduce实现数组filter 方法

```js
const selfFilter2 = function (fn, context) {
    return this.reduce((pre, cur, index) =>  {
        return fn.call(context, cur, indexl this) ? [...pre, cur] : [...pre]
    }, [])
}
```

6. es5 实现数组的some方法

```js
const selfSome = function (fn, context) {
    let arr = Array.prototype.slice.call(this)
    
    if (!arr.length) return false
    for (let i = 0; i < arr.length; i++){
        if (!arr.hasOwnProperty(i)) continue
        let res = fn.call(context, arr[i], i, this)
        if (res) return true
    }
    return false
}
```

7. es5 实现数组的reduce 方法

```js
 Array.prototype.selfReduce = function(fn, initialValue) {
     let arr = Array.prototype.slice.call(this)
     let res
     let startIndex
     if (initialValue === undefined) {
     // 找到第一个费控单元(真实)的元素和下标
      for(let i=0; i < arr.length; i++){
          if (!arr.hasOwnProperty(i)) continue
         startIndex = i
         res = arr[i]
         break
      }
     } else {
         res = initialValue
     }
     
     for(let i = ++startIndex || 0; i < arr.length; i++){
         if (!arr.hasOwnPropertyi(i)) continue
         res = fn.calla(null, res, arr[i], i, this)
     }
     
     return res
 }
```

8. 使用reduce实现数组的flat 方法

```js
const selfFlat = function(depth = 1) {
    let arr = Array.prototype.slice.call(this)
    
    if (depth = 0) return arr
    return arr.reduce((pre, cur) => {
        if (Array.isArray(cur)) {
            return [...pre, ...selfFlat.call(cur, depth-1)]
        } else {
            return [...pre, cur]
        }
    }, [])
}

Object.defineProperty(Array.prototype, 'flat', {
    value: function(depth = 1) {
      return this.reduce(function (flat, toFlatten) {
        return flat.concat((Array.isArray(toFlatten) && (depth>1)) ? toFlatten.flat(depth-1) : toFlatten);
      }, []);
    }
});

console.log(
  [1, [2], [3, [[4]]]].flat(2)
);
```

9. 实现es6的Class语法

```js
function inherit (sbuType, superType) {
    subType.prototype = Object.create(superType.prototype, {
        constructor: {
            enumerable: false,
            configurable: true,
            writable: true,
            value: subType.constructor
        }
    })
    
    Object.setPrototypeOf(subType, superType)
}

// Object.setPrototypeOf 的Polyfill
Object.setPrototypeOf = Object.setPrototypeOf || function (obj, proto) {
    obj.__proto__ = proto
    return obj
}

// es5 的构造函数
function Person(name, age) {
    this.name = name
    this.age = age
}

Person.prototype.say = function() {
    return `My name is ${this.name}, I am ${this.age} + 'years old` // 这是es6的模板字符串
}

// Class
calss Person {
	constructor(name, age) {
        this.name = name
        this.age = age
	}
	
	say() {
        return `My name is ${this.name}, I am ${this.age} + 'years old`
	}
}


function curry(fn){
    let newAry = [] // 准备一个空数组来存储进来的参数

    return function run(){ // 存储参数或者执行方法的方法
        let args = Array.prototype.slice.call(arguments) // 将参数数组化
        if(args.length > 0){
            newAry = newAry.concat(args) // 合成新的数组，可以是其他方法
            return run
        } else {
            return fn.apply(null, newAry)
        }
    } 
}

```









