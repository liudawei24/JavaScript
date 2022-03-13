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

另外，Array.of() 和 Array.from() 方法，以及展开运算符（...）也可以创建数组。我们后面会学习它们。

### 访问数组

可以使用数组索引来获取数组元素，访问数组元素需要用到方括号 []。

```javascript
  const element = array[index];
```

根据使用场景，你可能需要一个一个地访问数组元素或者使用循环来遍历。

可以像这样使用索引来访问数组元素：

```javascript
  const arr = ['a', 'b', 'c', 'd', 'e', 'f'];
  arr[1]; // 'b'
  arr[3]; // 'd'
  arr[5]; // 'f'
```

也可以利用数组长度（length 属性）值，反向遍历访问数组元素。

```javascript
  const arr = ['a', 'b', 'c', 'd', 'e', 'f'];
  const len = arr.length;
  arr[len - 1]; // 'f'
  arr[len - 3]; // 'd'
```

可以使用一般的 for 循环或 forEach 方法来遍历数组，也可以使用其它方式来遍历。

```javascript
  const arr = ['a', 'b', 'c', 'd', 'e', 'f'];

  for(let i=0; i<arr.length; i++) {
    console.log(`Element at index ${i} is ${arr[i]}`);
  }

  // Element at index 0 is a
  // Element at index 1 is b
  // Element at index 2 is c
  // Element at index 3 is d
  // Element at index 4 is e
  // Element at index 5 is f
```

### 添加数组元素

可以使用 push() 方法向数组中插入一个元素，它会将元素追加到数组的末尾。

```javascript
  const arr = ['a', 'b', 'c', 'd', 'e', 'f'];
  arr.push('g'); // ['a', 'b', 'c', 'd', 'e', 'f', 'g']
```

>注意，push() 方法会把元素追加到数组末尾，如果想要在数组头部插入一个元素，需要使用 unshift() 方法

```javascript
  const arr = ['a', 'b', 'c', 'd', 'e', 'f'];
  arr.unshift('g'); // ['g', 'a', 'b', 'c', 'd', 'e', 'f']
```

### 移除数组元素

移除单个数组元素的最简单方式是使用 pop() 方法。每次调用 pop() 方法，都会移除数组末尾的那个元素。pop() 方法的返回值是那个被移除的元素，这个方法会改变原始数组。

```javascript
  const arr = ['a', 'b', 'c', 'd', 'e', 'f'];
  arr.pop(); // 'f'

  console.log(arr); // ['a', 'b', 'c', 'd', 'e']
```

使用 shift() 方法可以移除数组头部的一个元素。与 pop() 方法类似，shift() 方法会返回那个被移除的元素，并且会改变原始数组。

```javascript
  const arr = ['a', 'b', 'c', 'd', 'e', 'f'];
  arr.shift(); // 'a'

  console.log(arr); // ['b', 'c', 'd', 'e', 'f']
```

### 克隆数组

可以使用 slice() 方法来克隆数组。注意，slice() 方法不改变原始数组，而是创建一个原始数组的浅拷贝副本。

```javascript
  const arr = ['a', 'b', 'c', 'd', 'e', 'f'];
  const copyArr = arr.slice()

  console.log(copyArr); // ['a', 'b', 'c', 'd', 'e', 'f']

  arr === copyArr; // false
```

也可以使用 "展开" 运算符来创建数组副本，我们很快会学到。

### 判断某个值是不是数组

可以使用 Array.isArray(value) 方法来判断某个值是不是数组，如果传入的值是一个数组的话，它会返回 true。

```javascript
  Array.isArray(['a', 'b', 'c']); // true
  Array.isArray('a'); // false
  Array.isArray([]); // true
```

## 数组解构

ECMAScript 6（ES6）提供了一些新语法，可以一次性从数组中获取多个元素并赋值给多个变量。它有助于保持代码简洁明了。这个新语法被称为解构语法。

下面是使用解构语法从数组中获取多个元素的例子：

```javascript
  let [a, b, c] = ['1', '2', '3'];
  console.log(a, b, c);
```

现在就可以使用这些变量了：

```javascript
  console.log(a, b, c); // '1' '2' '3'
```

如果不使用解构语法的话，代码会是这样：

```javascript
  let arr = ['1', '2', '3'];
  let a = arr[0]
  let b = arr[1]
  let c = arr[2]
```

所以，解构语法能够有助于减少代码量、极大地提高生产力。

### 为变量指定默认值

使用解构语法时，可以为变量指定默认值，当数组中没有对应的元素或者元素的值为 undefined 时，就会使用默认值。

```javascript
  let [a, b = '2'] = ['1'];
  console.log(a); // '1'
  console.log(b); // '2'
```
### 如何跳过某个数组元素

使用解构获取数组元素时，可以跳过某个元素。比如说，你可能只关注数组的部分元素，这时候这个语法就派上用场了。

注意表达式左边变量声明中的空格。

```javascript
  let [a, ,c] = ['1', '2', '3'];
  console.log(a); // '1'
  console.log(c); // '3'
```

### 嵌套数组解构

JavaScript 中，数组是可以嵌套的。这意味着一个数组的元素可以是另一个数组。数组可以嵌套任意深度。

例如，我们创建一个嵌套数组

```javascript
  let arr = ['1', '2', '3', ['4', '5', '6']];
```

要如何获取以上数组中的 '6' 呢？同样的，不使用解构的话，可以这样做：

```javascript
  let arr1 = arr[3]; // ['4', '5', '6']
  let f = arr1[2] // '6'
```

或者，也可以使用简写语法：

```javascript
  let f = arr[3][2] // '6'
```

还可以使用解构语法：

```javascript
  let [ , , , [ , , f]] = ['1', '2', '3', ['4', '5', '6']]
```

## 如何使用展开语法（Spread Syntax）和剩余参数（Rest Parameter）

从 ES6 开始，通过 ...（连续的三个点）可以在数组解构中使用展开语法和剩余参数。

- 使用剩余参数时，... 出现在解构语法表达式的左边。
- 使用展开语法时，... 出现在解构语法表达式的右边。

### 如何使用剩余参数

通过剩余参数，可以将剩下的元素映射到一个新的数组中。剩余参数必须是解构语法中的最后一个变量。

下面的例子中，我们把数组的前两个参数分别映射到了 a 和 b 变量中，剩下的元素则使用 ... 映射到了 rest 变量中。rest 是一个新数组，其中包含了剩下的元素。

```javascript
  let [ a, b, ...rest] = ['1', '2', '3', '4', '5', '6'];
  console.log(a); // '1'
  console.log(b); // '2'
  console.log(rest); // ['4', '5', '6']
```

### 如何使用展开运算符

使用展开运算符，可以这样来克隆现有的数组：

```javascript
  let arr = ['1', '2', '3', '4', '5', '6'];
  let arrCloned = [...arr];
  console.log(arrCloned); // ['1', '2', '3', '4', '5', '6']

  arr === arrCloned; // false
```

## 解构的使用场景

我们一起来看看数组解构、展开运算符和剩余参数的一些激动人心的使用场景。

### 使用解构交换变量值

使用数组解构语法可以很轻松地交换两个变量的值。

```javascript
  let first = '1';
  let second = '2';
  [first, second] = [second, first];

  console.log(first);  // '2'
  console.log(second); // '1'
```

### 合并数组

我们可以通过合并两个数组的所有元素来创建一个新数组（不改变原始数组）。假设现在有两个数组——一个包含一些数字，另一个包含一些字母。

```javascript
  let arr1 = ['1', '2'];
  let arr2 = ['a', 'b', 'c'];
```

现在，我们要把它们合并成一个新数组。


```javascript
  let arr3 = [...arr1, ...arr2];
  console.log(arr3); // ['1', '2', 'a', 'b', 'c']
```

## JavaScript 数组方法

到目前为止，我们已经了解了一些数组属性和方法。我们做一个简单的回顾：

- push() – 在数组末尾插入一个元素。
- unshift() – 在数组头部插入一个元素。
- pop() – 移除数组末尾的最后一个元素。
- shift() – 移除数组头部的第一个元素。
- slice() – 创建数组的浅拷贝副本。
- Array.isArray() – 判断某个值是不是数组。
- length – 数组的长度。

现在我们将通过示例来学习其它重要的数组方法。

### 如何创建数组、删除数组元素、更新数组元素以及访问数组元素

这一节，我们要学习用于创建新数组、移除数组元素及清空数组、访问数组元素等操作的方法。

#### concat() 方法

concat() 方法可以将多个数组合并在一起并返回合并后的数组。这是一个不可变方法，意味着它不会改变现有的数组。

拼接两个数组：

```javascript
  const first = [1, 2, 3];
  const second = [4, 5, 6];

  const merged = first.concat(second);

  console.log(merged); // [1, 2, 3, 4, 5, 6]
  console.log(first); // [1, 2, 3]
  console.log(second); // [4, 5, 6]
```

使用 concat() 方法也可以拼接两个以上的数组。我们可以这样拼接任意数量的数组：

```javascript
  array.concat(arr1, arr2,..,..,..,arrN);
```

示例如下：

```javascript
  const first = [1, 2, 3];
  const second = [4, 5, 6];
  const third = [7, 8, 9];

  const merged = first.concat(second, third);

  console.log(merged); // [1, 2, 3, 4, 5, 6, 7, 8, 9]
```

#### join() 方法

join() 方法使用一个分隔符将数组的所有元素拼接成一个字符串，并返回这个字符串。默认的分隔符是逗号（,）。

```javascript
  const emotions = ['🙂', '😍', '🙄', '😟'];

  const joined = emotions.join();
  console.log(joined); // "🙂,😍,🙄,😟"
```

可以传入一个自定义分隔符用于拼接数组元素。下面是一个使用自定义分隔符拼接数组元素的例子：

```javascript
  const joined = emotions.join('<=>');
  console.log(joined); // "🙂<=>😍<=>🙄<=>😟"
```

在空数组上调用 join() 方法，返回一个空字符串：

```javascript
  [].join() // returns ""
```

#### fill() 方法

fill() 方法使用一个固定值填充数组。可以使用这个固定值填充整个数组，也可以只覆盖选定的元素。注意，fill() 方法会改变原始数组。

```javascript
  const colors = ['red', 'blue', 'green'];

  colors.fill('pink');
  console.log(colors); // ["pink", "pink", "pink"]
```

下面是一个使用 fill() 方法覆盖数组的最后两个元素的例子：

```javascript
  const colors = ['red', 'blue', 'green'];

  colors.fill('pink', 1,3); // ["red", "pink", "pink"]
```

这个例子中，fill() 方法的第一个参数是用来填充数组的值，第二个参数是替换的起始索引（从 0 开始计算），最后一个参数是终止索引（最大值可以是 colors.length）。

#### includes() 方法

可以使用 includes() 方法来判断一个数组中是否包含某个元素，如果包含则返回 true，否则返回 false。

```javascript
  const names = ['tom', 'alex', 'bob', 'john'];

  names.includes('tom'); // returns true
  names.includes('july'); // returns false
```

#### indexOf() 方法

可以使用 indexOf() 方法找到某个元素在数组中的索引位置。它返回这个元素在数组中首次出现的索引，如果没有找到这个元素则返回 -1。

```javascript
  const names = ['tom', 'alex', 'bob', 'john'];

  names.indexOf('alex'); // returns 1
  names.indexOf('rob'); // returns -1
```

还有一个 lastIndexOf() 方法，可以找出某个元素在数组中最后出现的位置。与 indexOf() 类似，lastIndexOf() 在找不到这个元素时也返回 -1。

```javascript
  const names = ['tom', 'alex', 'bob', 'tom'];

  names.indexOf('tom'); // returns 0
  names.lastIndexOf('tom'); // returns 3
```

#### reverse() 方法

顾名思义，reverse() 方法将数组中元素的位置颠倒，最后一个元素变成第一个、第一个元素变成最后一个。

```javascript
  const names = ['tom', 'alex', 'bob'];

  names.reverse(); // returns ["bob", "alex", "tom"]
```

> reverse() 方法会改变原始数组。

#### sort() 方法

sort() 方法可能是最常用的数组方法之一。sort() 方法默认会把元素转换为字符串再对它们进行排序。默认的排序方式是升序排列。sort() 方法会改变原始数组。

```javascript
  const names = ['tom', 'alex', 'bob'];

  names.sort(); // returns ["alex", "bob", "tom"]
```

sort() 方法接收一个可选的比较器函数作为参数，可以编写一个比较器函数传入 sort() 方法来覆盖默认的排序行为。

假设现在有一个数字数组，我们使用比较器函数将它按升序和降序排序：

```javascript
  const numbers = [23, 5, 100, 56, 9, 13, 37, 10, 1];
```

首先，调用 sort() 方法，并观察结果：

```javascript
  numbers.sort(); //  [1, 10, 100, 13, 23, 37, 5, 56, 9]
```

现在，排序后的数组为 [1, 10, 100, 13, 23, 37, 5, 56, 9]。这并不是我们预期的结果。得到这个结果是因为 sort() 方法默认会将元素转换为字符串，再基于字符串诸个字符对应的 UTF-16 编码值进行比较。

为了解决这个问题，我们编写一个比较器函数。这是用于升序排序的：

```javascript
  function ascendingComp(a, b){
    return (a-b);
  }
```

把比较器函数传入 sort() 方法：

```javascript
  numbers.sort(ascendingComp); // retruns [1, 5, 9, 10, 13, 23, 37, 56, 100]

  /* 

  也可以使用行内函数：

  numbers.sort(function(a, b) {
    return (a-b);
  });

  或者使用箭头函数的写法：

  numbers.sort((a, b) => (a-b));

  */
```

降序排序：

```javascript
  numbers.sort((a, b) => (b-a));
```

#### splice() 方法

splice() 方法可以帮助你向数组中添加元素、更新数组元素以及移除数组元素。刚开始接触这个方法可能会令人困惑，不过只要你理解了它的正确用法，就能够掌握。

splice() 方法的主要目标是从数组中移除元素。它会返回由被移除的元素组成的数组，并且会改变原始数组。你也可以用它来向数组中添加元素或者替换数组中的元素。

使用 splice() 方法向数组中添加一个元素，需要传入插入的目标位置、从目标位置算起想要删除的元素数量以及要插入的元素。

下面的例子中，我们在索引为 1 的位置上插入了一个元素 zack，没有删除任何元素。

```javascript
  const names = ['tom', 'alex', 'bob'];

  names.splice(1, 0, 'zack');

  console.log(names); // ["tom", "zack", "alex", "bob"]
```

看看下面的例子，我们移除了索引 2 位置之后的一个元素（即第三个元素），并添加了一个元素 zack。splice() 方法返回一个由移除掉的元素——bob——组成的数组。

```javascript
  const names = ['tom', 'alex', 'bob'];

  const deleted = names.splice(2, 1, 'zack');

  console.log(deleted); // ["bob"]
  console.log(names); // ["tom", "alex", "zack"]
```

### 静态数组方法

在 JavaScript 中，数组有三个静态方法。我们已经讨论过 Array.isArray()，接下来要探讨其余两个方法。

#### Array.from() 方法

假设有以下 HTML 代码片段，其中包含一个 div 和一些列表元素：

```javascript
  <div id="main">
    <ul>
      <ol type="1">
        <li>...</li>
        <li>...</li>
        <li>...</li>
        <li>...</li>
        <li>...</li>
        <li>...</li>
        <li>...</li>
        <li>...</li>
        <li>...</li>
        <li>...</li>
      </ol>
    </ul> 
  </div>
```

我们使用 getElementsByTagName() 方法获取这些列表元素。

```javascript
  document.getElementsByTagName('li');
```

它返回如下 HTMLCollection 对象：

![](https://www.freecodecamp.org/news/content/images/2021/05/htmlCollec.png)

HTMLCollection 是类数组对象

它和数组类似，我们试着使用 forEach 来遍历它：

```javascript
  document.getElementsByTagName('li').forEach(() => {
  // Do something here..
  });
```

猜猜会输出什么？会报出以下错误：

![](https://www.freecodecamp.org/news/content/images/2021/05/htmlcolc_error.png)

在类数组对象上调用 forEach 发生错误

为什么会这样？这是因为 HTMLCollection 并不是数组，而是 类数组 对象，所以不能使用 forEach 来遍历它。

![](https://www.freecodecamp.org/news/content/images/2021/05/htmlCollec_object.png)

其原型（proto）是 Object

这里就需要用到 Array.from() 方法了，Array.from() 能将类数组对象转换为数组，进而能够在它上面执行所有数组操作。

```javascript
  const collection = Array.from(document.getElementsByTagName('li'));
```

这里的 collection 是一个数组：

![](https://www.freecodecamp.org/news/content/images/2021/05/collection.png)

其原型为 Array

#### Array.of() 方法

Array.of() 可以使用任意数量任意类型的元素创建一个新数组。

```javascript
  Array.of(2, false, 'test', {'name': 'Alex'});
```

输出如下：

![](https://www.freecodecamp.org/news/content/images/2021/05/image-49.png)

Array.of() 方法的输出结果

### 数组迭代器方法

现在我们要学习数组迭代器方法。这些方法在执行数组迭代、计算、做判断、过滤元素等操作时很有用。

到目前为止，我们还没见过对象数组的示例。在这一节，我们将会使用下面的对象数组来解释和演示这些迭代器方法。

这个数组包含了一些订阅各种付费课程的学生的信息：

```javascript
  let students = [
    {
        'id': 001,
        'f_name': 'Alex',
        'l_name': 'B',
        'gender': 'M',
        'married': false,
        'age': 22,
        'paid': 250,  
        'courses': ['JavaScript', 'React']
    },
    {
        'id': 002,
        'f_name': 'Ibrahim',
        'l_name': 'M',
        'gender': 'M',
        'married': true,
        'age': 32,
        'paid': 150,  
        'courses': ['JavaScript', 'PWA']
    },
    {
        'id': 003,
        'f_name': 'Rubi',
        'l_name': 'S',
        'gender': 'F',
        'married': false,
        'age': 27,
        'paid': 350,  
        'courses': ['Blogging', 'React', 'UX']
    },
    {
        'id': 004,
        'f_name': 'Zack',
        'l_name': 'F',
        'gender': 'M',
        'married': true,
        'age': 36,
        'paid': 250,  
        'courses': ['Git', 'React', 'Branding']
    } 
  ];
```

让我们开始吧。所有数组迭代器方法都接收一个函数作为参数，需要在这个函数中声明迭代逻辑。

#### filter() 方法

filter() 方法用所有满足过滤条件的元素来创建一个新数组。我们要找出女学生，所以过滤条件应该是 gender === 'F'。

```javascript
  const femaleStudents = students.filter((element, index) => {
    return element.gender === 'F';
  })

  console.log(femaleStudents);
```

输出如下：

![](https://www.freecodecamp.org/news/content/images/2021/05/image-50.png)

结果是正确的，名为 Rubi 的学生是目前唯一的女学生。

#### map()方法

map() 方法遍历整个数组，依次对数组元素执行回调函数并用这些返回值创建一个新数组。我们将会创建一个由 students 数组中所有学生的全名组成的新数组。

```javascript
  const fullNames = students.map((element, index) => {
    return {'fullName': element['f_name'] + ' ' + element['l_name']}
  });

  console.log(fullNames);
```

输出如下：

![](https://www.freecodecamp.org/news/content/images/2021/05/image-51.png)

这里我们可以看到由包含 fullName 属性的对象组成的数组，fullName 是由 student 对象的 f_name 和 l_name 属性计算得到的。

#### reduce() 方法

reduce() 方法对每个数组元素执行 reducer 函数，并将其结果汇总为单个返回值。我们将会在 students 数组中应用一个 reducer 函数来计算所有学生支付的总额。

```javascript
  const total = students.reduce(
    (accumulator, student, currentIndex, array) => {
        accumulator = accumulator + student.paid;
        return (accumulator);
    }, 
  0);

  console.log(total); // 1000
```

在上面的代码中，

- 我们将累加器（accumulator）初始化为 0。
- 我们对每个 student 对象执行 reduce 方法，读取 paid 属性值并把它累加在累加器上。
- 最后，返回累加器。

#### some() 方法

some() 方法返回一个布尔值（true/false），其返回值取决于数组中是否至少有一个元素符合回调函数中的判断条件。我们来看看是否有学生的年龄小于 30 岁。

```javascript
  let hasStudentBelow30 = students.some((element, index) => {
    return element.age < 30;
  });

  console.log(hasStudentBelow30); // true
```

是的，我们看到至少有一个学生的年龄是小于 30 岁的。

#### find() 方法

使用 some() 方法，我们已经看到有一个 30 岁以下的学生。让我们找出这个学生。

为此，我们会用到 find() 方法，它会返回数组中第一个满足判断条件的元素。

还有另一个相关的方法 findIndex()，这个方法返回我们使用 find() 方法找到的元素的索引，如果没有符合条件的元素则返回 -1。

下面的例子中，我们向 find() 方法中传入了一个函数用来判断学生的年龄，它会返回满足判断条件的学生。

```javascript
  const student = students.find((element, index) => {
    return element.age < 30;
  });

  console.log(student);
```

输出如下：

![](https://www.freecodecamp.org/news/content/images/2021/05/image-52.png)

可以看到，他就是 22 岁的 Alex，我们找到他了。

#### every() 方法

every() 方法检查是否数组的每个元素都满足给定的判断条件。让我们检查一下是不是所有学生都订阅了至少两门课程。

```javascript
  const atLeastTwoCourses = students.every((elements, index) => {
    return elements.courses.length >= 2;
  });

  console.log(atLeastTwoCourses); // true
```

正如预期，我们看到结果为 true。