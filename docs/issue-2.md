# 从头学习JS 第 2 天

## 两个栈实现一个队列

本文转载自 小羊快码大佬的 [字节面试：两个栈实现一个队列](https://mp.weixin.qq.com/s/CCL2dIsIaQ-eC9yqRBuJCg)

大家好，我是小羊~

面过字节的小伙伴们都知道，字节面试中特别喜欢考察算法和数据结构。小羊曾经就被问到如何用两个栈实现一个队列，后来这道题也被纳入了我面试候选人的考察范围中

说到栈和队列，他们都属于一种顺序存储的数据结构，但是两者还是有较大区别。下面小羊就用一个故事来解释栈和队列的特点。

### 队列：先进先出

大雄、胖虎和静香想去无人岛玩，于是多啦A梦拿出了任意门

![img1](https://mmbiz.qpic.cn/mmbiz_jpg/A2lPWZgVALPbzicob95efUAxLuWibnYsAyxxKjRhJ0JfGAWBE0icobxQzCumFOzkiblrBFBLm1nJBHdjyXfN0nY6Nw/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)

由于任意门每次只能进去一个，所以大家要排队进去，顺序依次为胖虎、大雄、静香、多啦A梦

![img2](https://mmbiz.qpic.cn/mmbiz_jpg/A2lPWZgVALPbzicob95efUAxLuWibnYsAymg3sFxKT03icMAugFdX0ib3Ijk3dnPBb47AiaAXr8aFDoILs7kwXVusfA/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)

由于胖虎是第一个，所以他每次都能先到达目的地。出来的顺序依次为：胖虎、大雄、静香、多啦A梦

![img3](https://mmbiz.qpic.cn/mmbiz_jpg/A2lPWZgVALPbzicob95efUAxLuWibnYsAyoS4I4hjVLDnqExTowrLLHGsiadZW7vMH1TXy8sZWpW0QRejW436cdnQ/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)

> 分析：胖虎一行人排队进入任意门就是典型的队列形式，大家遵循“先进先出”的原则，从任意门的一端进入，另一端出去。因此队列的特点表现为两端都"开口"，在表的一端进行插入操作，在另一端进行删除操作。最先进队列的数据元素，同样要最先出队列。

### 栈：先进后出

大家玩到了傍晚，准备回家了，但是这时候多啦A梦发现他的任意门坏了，所以他拿出了另一个道具：神奇漂流瓶

![img4](https://mmbiz.qpic.cn/mmbiz_jpg/A2lPWZgVALPbzicob95efUAxLuWibnYsAy94LC3lA3e70IA24PojsQIiaH2VPuNebdliadfcdBtoBvq6P1NndtwBmQ/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)

于是，大家还是按照之前的顺序进入到了漂流瓶里，进入的顺序为：胖虎、大雄、静香、多啦A梦

![img5](https://mmbiz.qpic.cn/mmbiz_jpg/A2lPWZgVALPbzicob95efUAxLuWibnYsAyWmBW8RydvnHDfy5Qy49D3pUYqNyhFbZc0hKejEBNFoRHbibS6pXNPNA/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)

漂流了好久，终于靠岸了，大家依次从瓶子里跳了出来，这时出来的次序为：多啦A梦、静香、大雄、胖虎。胖虎最先进去的反而最后出来

![img6](https://mmbiz.qpic.cn/mmbiz_jpg/A2lPWZgVALPbzicob95efUAxLuWibnYsAyrfccoPaQ5aaAKVHCUuz2FJdmnCldNUXpEiaqdcXO54zI8sjQVWHVVcQ/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)

> 分析：因为漂流瓶只有一个入口，所以大家只能从瓶口进入，再从瓶口出来，因此最后进入漂流瓶的会最先出来。这里漂流瓶就是一个栈，遵循“后进先出”的原则。栈的特点表现为一端开口，开口端被称为栈顶，封口端被称为栈底。向栈中添加元素，此过程被称为"入栈"，向栈中删除元素，被称为“出栈“

### 两个栈实现一个队列

上面详细介绍了栈和队列的特点，那么如何用两个栈实现一个队列呢？

首先创建两个栈 stack1 和 stack2，当有新元素插入时，直接把新元素压入stack1。依次压入1、2、3

![img7](https://mmbiz.qpic.cn/mmbiz_png/A2lPWZgVALPbzicob95efUAxLuWibnYsAyUsCXQeetNPEbdvHgtI5qeQ2ibZcdCEyCWFpWYNcXZ29VQtoc929dcYg/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

当要删除元素时，分为两步：

第一步：将stack1里的元素依次弹出并压入stack2，往stack2依次压入3、2、1

![img8](https://mmbiz.qpic.cn/mmbiz_jpg/A2lPWZgVALPbzicob95efUAxLuWibnYsAyEgSYSOwkvPAmeXyBHMybpCIjNSzURvNf4uT4dkVGvCg7d7zCaNXNjA/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)

第二步：依次弹出stack2栈顶元素1、2、3，直到栈为空

![img9](https://mmbiz.qpic.cn/mmbiz_jpg/A2lPWZgVALPbzicob95efUAxLuWibnYsAywjSC0mh9ds0QiaTlpOmGFRiaUfqXfMbDV1UkPWklFVFibAIcicWO6RbzHQ/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)

最终用两个栈 stack1 和 stack2 达到了“先进先出”的目的。

### 代码实现

最后附上代码实现（JS版本）

```javascript
  class Queue {
    constructor() {
      this.stack1 = [];
      this.stack2 = [];
    }

    push(value) {
      this.stack1.push(value);
    }

    pop() {
      // 如果stack2有数据，弹出stack2栈顶元素
      if (this.stack2.length) {
        return this.stack2.pop();
        // 如果stack2和stack1都为空，返回-1
      } else if (!this.stack1.length) {
        return -1;
      } else {
        // 如果stack1有数据，将stack1里的元素依次弹出并压入stack2，并重新执行删除方法
        while (this.stack1.length) {
          this.stack2.push(this.stack1.pop());
        }

        return this.pop();
      }
    }
  }

  const queue = new Queue();
  queue.push(1);
  queue.push(2);
  queue.pop(); // 1
  queue.pop(); // 2
```
