# 从头学习JS 第 4 天

## 对象

### 定义属性 Object.defineProperty()

这个方法接收 3 个参数：
要给其添加属性的对象、属性的名称和一个描述符对象。最后一个参数，即描述符对象上的属性可以包
含：数据属性（configurable、enumerable、writable 和 value）或 访问器属性（configurable、enumerable、get 和 set），跟相关特性的名称一一对应。根据要修改
的特性，可以设置其中一个或多个值。


```javascript
  let person = {}; 
  Object.defineProperty(person, "name", { 
    writable: false, 
    value: "Nicholas" 
  }); 
  console.log(person.name); // "Nicholas" 
  person.name = "Greg"; 
  console.log(person.name); // "Nicholas"
```

```javascript
  let person = {}; 
  Object.defineProperty(person, "name", { 
    configurable: false, 
    value: "Nicholas" 
  }); 
  console.log(person.name); // "Nicholas" 
  delete person.name; 
  console.log(person.name); // "Nicholas"
```

```javascript
  let person = {}; 
  Object.defineProperty(person, "name", { 
    configurable: false, 
    value: "Nicholas" 
  }); 
  // 抛出错误
  Object.defineProperty(person, "name", { 
    configurable: true, 
    value: "Nicholas" 
  });
```

```javascript
  // 定义一个对象，包含伪私有成员 year_和公共成员 edition 
  let book = { 
    year_: 2017, 
    edition: 1
  }; 
  Object.defineProperty(book, "year", { 
    get() { 
    return this.year_; 
    }, 
    set(newValue) { 
      if (newValue > 2017) { 
        this.year_ = newValue; 
        this.edition += newValue - 2017; 
      } 
    } 
  }); 
  book.year = 2018; 
  console.log(book.edition); // 2
```

### 定义多个属性 Object.defineProperties()

这个方法可以通过多个描述符一次性定义多个属性。它接收两个参数：要为之添
加或修改属性的对象和另一个描述符对象，其属性与要添加或修改的属性一一对应。

```javascript
  let book = {}; 
  Object.defineProperties(book, { 
    year_: { 
      value: 2017 
    }, 
    edition: { 
      value: 1 
    }, 
    year: { 
      get() { 
        return this.year_; 
      },
      set(newValue) { 
        if (newValue > 2017) { 
          this.year_ = newValue; 
          this.edition += newValue - 2017; 
        } 
      } 
    } 
  });
```

### 读取属性的特性 Object.getOwnPropertyDescriptor()

这个方法接
收两个参数：属性所在的对象和要取得其描述符的属性名。返回值是一个对象，对于访问器属性包含
configurable、enumerable、get 和 set 属性，对于数据属性包含 configurable、enumerable、
writable 和 value 属性。

```javascript
  let book = {}; 
  Object.defineProperties(book, { 
    year_: { 
      value: 2017 
    }, 
    edition: { 
      value: 1 
    }, 
    year: { 
      get: function() { 
        return this.year_; 
      }, 
      set: function(newValue){ 
        if (newValue > 2017) { 
          this.year_ = newValue; 
          this.edition += newValue - 2017; 
        } 
      } 
    } 
  }); 
  let descriptor = Object.getOwnPropertyDescriptor(book, "year_"); 
  console.log(descriptor.value); // 2017 
  console.log(descriptor.configurable); // false 
  console.log(typeof descriptor.get); // "undefined" 
  let descriptor = Object.getOwnPropertyDescriptor(book, "year"); 
  console.log(descriptor.value); // undefined 
  console.log(descriptor.enumerable); // false 
  console.log(typeof descriptor.get); // "function"
```

### 读取多属性的特性 Object.getOwnPropertyDescriptors()

这个方法实际上
会在每个自有属性上调用 Object.getOwnPropertyDescriptor()并在一个新对象中返回它们。

```javascript
  let book = {}; 
  Object.defineProperties(book, { 
  year_: { 
    value: 2017 
  }, 
  edition: { 
    value: 1 
  }, 
  year: { 
    get: function() { 
      return this.year_; 
    }, 
    set: function(newValue){ 
      if (newValue > 2017) { 
        this.year_ = newValue; 
        this.edition += newValue - 2017; 
      } 
    } 
  } 
  }); 
  console.log(Object.getOwnPropertyDescriptors(book)); 
  // { 
  //  edition: { 
  //    configurable: false, 
  //    enumerable: false, 
  //    value: 1, 
  //    writable: false 
  //  }, 
  //  year: { 
  //   configurable: false, 
  //    enumerable: false, 
  //    get: f(), 
  //    set: f(newValue), 
  //  }, 
  //  year_: { 
  //    configurable: false, 
  //    enumerable: false, 
  //    value: 2017, 
  //    writable: false 
  //  } 
  // }
```

### 合并对象 Object.assign()

这个方法接收一个目标对象和一个
或多个源对象作为参数，然后将每个源对象中可枚举（Object.propertyIsEnumerable()返回 true）
和自有（Object.hasOwnProperty()返回 true）属性复制到目标对象。以字符串和符号为键的属性
会被复制。对每个符合条件的属性，这个方法会使用源对象上的[[Get]]取得属性的值，然后使用目标
对象上的[[Set]]设置属性的值。

```javascript
  let dest, src, result; 
  /** 
   * 简单复制
   */ 
  dest = {}; 
  src = { id: 'src' }; 
  result = Object.assign(dest, src); 
  // Object.assign 修改目标对象
  // 也会返回修改后的目标对象
  console.log(dest === result); // true 
  console.log(dest !== src); // true 
  console.log(result); // { id: src } 
  console.log(dest); // { id: src } 
  /** 
   * 多个源对象
   */ 
  dest = {}; 
  result = Object.assign(dest, { a: 'foo' }, { b: 'bar' }); 
  console.log(result); // { a: foo, b: bar } 
  /** 
   * 获取函数与设置函数
   */ 
  dest = { 
  set a(val) { 
    console.log(`Invoked dest setter with param ${val}`); 
  } 
  }; 
  src = { 
    get a() { 
      console.log('Invoked src getter'); 
    return 'foo'; 
  } 
  }; 
  Object.assign(dest, src); 
  // 调用 src 的获取方法
  // 调用 dest 的设置方法并传入参数"foo" 
  // 因为这里的设置函数不执行赋值操作
  // 所以实际上并没有把值转移过来
  console.log(dest); // { set a(val) {...} }
```

Object.assign()实际上对每个源对象执行的是浅复制。如果多个源对象都有相同的属性，则使
用最后一个复制的值。

```javascript
  let dest, src, result; 
  /** 
   * 覆盖属性
   */ 
  dest = { id: 'dest' }; 
  result = Object.assign(dest, { id: 'src1', a: 'foo' }, { id: 'src2', b: 'bar' }); 
  // Object.assign 会覆盖重复的属性
  console.log(result); // { id: src2, a: foo, b: bar } 
  // 可以通过目标对象上的设置函数观察到覆盖的过程：
  dest = { 
  set id(x) { 
    console.log(x); 
  } 
  }; 
  Object.assign(dest, { id: 'first' }, { id: 'second' }, { id: 'third' }); 
  // first 
  // second 
  // third 
  /** 
   * 对象引用
   */ 
  dest = {}; 
  src = { a: {} }; 
  Object.assign(dest, src); 
  // 浅复制意味着只会复制对象的引用
  console.log(dest); // { a :{} } 
  console.log(dest.a === src.a); // true
```

如果赋值期间出错，则操作会中止并退出，同时抛出错误。Object.assign()没有“回滚”之前
赋值的概念，因此它是一个尽力而为、可能只会完成部分复制的方法。

```javascript
  let dest, src, result; 
  /** 
   * 错误处理
   */ 
  dest = {}; 
  src = { 
    a: 'foo', 
    get b() { 
      // Object.assign()在调用这个获取函数时会抛出错误
      throw new Error(); 
    },
    c: 'bar' 
  }; 
  try { 
    Object.assign(dest, src); 
  } catch(e) {} 
  // Object.assign()没办法回滚已经完成的修改
  // 因此在抛出错误之前，目标对象上已经完成的修改会继续存在：
  console.log(dest); // { a: foo }
```

### 对象标识及相等判定 Object.is()

这个方法必须接收两个参数。

```javascript
  console.log(Object.is(true, 1)); // false 
  console.log(Object.is({}, {})); // false 
  console.log(Object.is("2", 2)); // false 
  // 正确的 0、-0、+0 相等/不等判定
  console.log(Object.is(+0, -0)); // false 
  console.log(Object.is(+0, 0)); // true 
  console.log(Object.is(-0, 0)); // false 
  // 正确的 NaN 相等判定
  console.log(Object.is(NaN, NaN)); // true
```

### 获取对象的原型 Object.getPrototypeOf()

ECMAScript 的 Object 类型有一个方法叫 Object.getPrototypeOf()，返回参数的内部特性
[[Prototype]]的值。

```javascript
  console.log(Object.getPrototypeOf(person1) == Person.prototype); // true 
  console.log(Object.getPrototypeOf(person1).name); // "Nicholas"
```

### 写入对象的原型 Object.setPrototypeOf()

```javascript
  let biped = { 
    numLegs: 2 
  }; 
  let person = { 
    name: 'Matt' 
  }; 
  Object.setPrototypeOf(person, biped); 
  console.log(person.name); // Matt 
  console.log(person.numLegs); // 2 
  console.log(Object.getPrototypeOf(person) === biped); // true
```

### 创建对象 Object.create()

```javascript
  let biped = { 
    numLegs: 2 
  }; 
  let person = Object.create(biped); 
  person.name = 'Matt'; 
  console.log(person.name); // Matt 
  console.log(person.numLegs); // 2 
  console.log(Object.getPrototypeOf(person) === biped); // true
```
