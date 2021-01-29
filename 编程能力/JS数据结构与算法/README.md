### 数据结构 
转载  https://www.jianshu.com/p/38853c044156
https://www.cnblogs.com/AhuntSun-blog/p/12636718.html

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
数组是一种线性元素，可以在数组的任意位置删除和插入数据     <br>
栈也是一种受限的线性结构     <br>
只能在栈顶添加(进栈)和删除(出栈)元素，     <br>
特点：后出先出；LIFO     <br>

函数调用栈：A调用B，B调用C     <br>
A入栈B入栈C入栈，C执行完出栈，B出栈     <br>

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


  //封装栈类   创建了一个Stack构造函数, 用户创建栈的类.
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
```

### 队列Queue
特点：先进先出，一端删除元素，一端添加元素
- 基于数组实现
- 基于链表实现

```js
常见的操作：
1.enqueue(element) :向队列尾部添加一个或多个新元素
2.dequeue() :移除对了头部第一个元素，同事返回元素
3.front() :返回队列中第一个元素，不会对队列做任何修改
4.isEmpty()
5.size()
6.toString()<script>
    // 基于数组封装队列类
    function Queue() {
        // 属性
        this.items = []

        // 方法
        // 1.enqueue():将元素加入到队列中
        Queue.prototype.enqueue = element => {
            this.items.push(element)
        }

        // 2.dequeue():从队列中删除前端元素
        Queue.prototype.dequeue = () => {
            return this.items.shift()
        }

        // 3.front():查看前端的元素
        Queue.prototype.front = () => {
            return this.items[0]
        }

        // 4.isEmpty:查看队列是否为空
        Queue.prototype.isEmpty = () => {
            return this.items.length == 0;
        }

        // 5.size():查看队列中元素的个数
        Queue.prototype.size = () => {
            return this.items.length
        }

        // 6.toString():将队列中元素以字符串形式输出
        Queue.prototype.toString = () => {
            let resultString = ''
            for (let i of this.items){
                resultString += i + ' '
            }
            return resultString
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
    // 队列应用：面试题：击鼓传花
    let passGame = (nameList, num) => {
        //1.创建队列结构
        let queue = new Queue()

        //2.将所有人依次加入队列
        // 这是ES6的for循环写法，i相当于nameList[i]
        for(let i of nameList){
            queue.enqueue(i)
        }


        // 3.开始数数
        while(queue.size() > 1){//队列中只剩1个人就停止数数
            // 不是num的时候，重新加入队列末尾
            // 是num的时候，将其从队列中删除
            // 3.1.num数字之前的人重新放入队列的末尾(把队列前面删除的加到队列最后)
            for(let i = 0; i< num-1; i++ ){
                queue.enqueue(queue.dequeue())
            }
            // 3.2.num对应这个人，直接从队列中删除
            /*
              思路是这样的，由于队列没有像数组一样的下标值不能直接取到某一元素，所以采用，把num前面的num-1个元素先删除后添加到队列末尾，这样第num个元素就排到了队列的最前面，可以直接使用dequeue方法进行删除
            */
            queue.dequeue()
        }

        //4.获取剩下的那个人
        console.log(queue.size());									//104
        let endName = queue.front()
        console.log('最终剩下的人：' + endName);						   //106

        return nameList.indexOf(endName);
    }

    //5.测试击鼓传花
    let names = ['lily', 'lucy', 'Tom', 'Lilei', 'Tony']
    console.log(passGame(names, 3));
</script>
</script>
```

优先队列

优先级队列主要考虑的问题为：

每个元素不再只是一个数据，还包含数据的优先级     <br>
在添加数据过程中，根据优先级放入到正确位置     <br>

```js
function PriorityQueue() {
       // 1.1.创建QueueElement对象
       function QueueElement(element,priority) {
           this.element=element;
           this.priority=priority;
       }
       this.items=[]

       PriorityQueue.prototype.enqueue=(element,priority)=>{
           let queueElement= new QueueElement(element,priority)

           // 1.2.判断队列是否为空
           if (this.items.length===0){
               this.items.push(queueElement)
           }else {
               let add=false
               // 定义一个变量记录是否成功添加了新元素
              for (let i=0;i<this.items.length;i++){
                  // 让新插入的元素与原有元素进行优先级比较(priority越小，优先级越大)
                  if (queueElement.priority<this.items[i].priority){
                      this.items.splice(i,0,queueElement)
                      add=true
                      return
                      // 新元素已经找到插入位置了可以使用break停止循环
                  }
               }
               // 新元素没有成功插入，就把它放在队列的最前面
              if (!add){
                  this.items.push(queueElement)
              }

           }
       }
       // 2.dequeue():从队列中删除前端元素
       PriorityQueue.prototype.dequeue=()=>{
           return this.items.shift()
       }
       // 3.front():查看前端的元素
       PriorityQueue.prototype.front=()=>{
           return this.items[0]
       }
       // 4.isEmpty():查看队列是否为空
       PriorityQueue.prototype.isEmpty=()=>{
           return this.items.length ===0
       }
       // 5.size():查看队列中元素的个数
       PriorityQueue.prototype.size=()=>{
           return this.items.length
       }

   }
   let priorityQueue=new PriorityQueue()
    priorityQueue.enqueue('we',1)
    priorityQueue.enqueue('er',3)
    priorityQueue.enqueue(89,2)
    console.log(priorityQueue)
    //结果
    items: Array(3)
0: QueueElement {element: "we", priority: 1}
1: QueueElement {element: 89, priority: 2}
2: QueueElement {element: "er", priority: 3}
length: 3
```

P15
