### 数据结构
计算机中，存储和组织数据的方式
### 算法
解决问题的方法/步骤逻辑
### log
10^4=10000
log(10)(10000)=4
二分查找：以2为底
log(2)(8)=3

### 补充
java可以封装一个object数组，不然不能存储不同数据类型的数据，容量不能自动扩容，插入，删除操作效率低

### 栈
数组是一种线性元素，可以在数组的任意位置删除和插入数据
栈也是一种受限的线性结构
只能在栈顶添加(进栈)和删除(出栈)元素，
特点：后出先出；LIFO

函数调用栈：A调用B，B调用C
A入栈B入栈C入栈，C执行完出栈，B出栈

实现栈结构
- 基于数组实现
- 基于链表实现

常见的操作：
```js
1.push(element) :添加一个新元素到栈顶位置
2.pop() :移除栈顶元素，同事返回栈顶元素
3.peek() :返回栈顶元素，不会对栈做任何修改
4.isEmpty() :如果栈里没有任何元素就返回true,否则返回false
5.size() :返回栈里元素个数
6.toString() :将栈内容以字符串形式返回
```js

  //封装栈类
  ```js
    function Stack() {
        this.items =[];
        //将元素压入栈,prototype在类中添加方法
        Stack.prototype.push=function (element) {
            this.items.push(element);
        }
        //从栈中删除元素，取出元素
        Stack.prototype.pop =function () {
            return this.items.pop();
        }
        //查看栈顶元素
        Stack.prototype.peek=function () {
            return this.items[this.items.length-1];
        }
        //判断栈是否为空
        Stack.prototype.isEmpty= function () {
            return this.items.length ===0;
        }
        //获取栈中元素的个数
        Stack.prototype.size= function () {
            return this.items.length
        }
        //toString方法
        Stack.prototype.toString=function () {
            var string='';
            for (var i=0;i<this.items.length;i++){
                string +=this.items[i]+ '';
            }
            return string;
        }
    }
    var s=new Stack();
    
    //十进制转二进制 
     function dec2bin(number) {
        var stack=new Stack()
      while(number>0){
            stack.push(number%2);
          number=Math.floor(number/2);
      }
      var binString='';
        while(!stack.isEmpty()){
            binString+=stack.pop();
        }
        return binString;
  }
  alert(dec2bin(100));
```js

### 队列Queue
特点：先进先出，一端删除元素，一端添加元素
- 基于数组实现
- 基于链表实现
常见的操作：
1.enqueue(element) :向队列尾部添加一个或多个新元素
2.dequeue() :移除对了头部第一个元素，同事返回元素
3.front() :返回队列中第一个元素，不会对队列做任何修改
4.isEmpty()
5.size()
6.toString()
```js
<script>
    function Queue() {
        this.items=[];
        //往队列添加元素
        Queue.prototype.enqueue=function (element) {
            this.items.push(element);
        }
        Queue.prototype.dequeue=function () {
            return this.items.shift();
        }
        //查看队列头元素
        Queue.prototype.front=function () {
            return this.items[0]
        }
        Queue.prototype.size=function () {
            return this.items.length;
        }
        Queue.prototype.toString=function () {
            var string='';
            for (var i=0;i<this.items.length;i++){
                string +=this.items[i]+ '';
            }
            return string;
        }
    }
    var queue=new Queue();
    queue.enqueue("a");
    queue.enqueue("b");
    queue.enqueue("c");
    alert(queue);
    queue.dequeue();
    alert(queue);
    alert(queue.front());
</script>
```js
P15
