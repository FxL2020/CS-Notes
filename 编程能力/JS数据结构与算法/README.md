### 数据结构 
转载  https://www.jianshu.com/p/38853c044156

https://www.cnblogs.com/AhuntSun-blog/p/12636718.html

https://www.cnblogs.com/AhuntSun-blog/p/?page=1

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

#### 优先队列

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

### 链表
#### 单向链表
单向链表简介      <br>
链表和数组一样，可以用于存储一系列的元素，但是链表和数组的实现机制完全不同。链表的每个元素由一个存储元素本身的节点和一个指向下一个元素的引用     <br>

head属性指向链表的第一个节点；     <br>
链表中的最后一个节点指向null；     <br>
当链表中一个节点也没有的时候，head直接指向null；     <br>
数组存在的缺点：

数组的创建通常需要申请一段连续的内存空间（一整块内存），并且大小是固定的。所以当原数组不能满足容量需求时，需要扩容（一般情况下是申请一个更大的数组，比如2倍，然后将原数组中的元素复制过去）。     <br>
在数组的开头或中间位置插入数据的成本很高，需要进行大量元素的位移。     <br>
链表的优势：   

链表中的元素在内存中不必是连续的空间，可以充分利用计算机的内存，实现灵活的内存动态管理。     <br>
链表不必在创建时就确定大小，并且大小可以无限地延伸下去。     <br>
链表在插入和删除数据时，时间复杂度可以达到O(1)，相对数组效率高很多。     <br>

链表的缺点：

链表访问任何一个位置的元素时，都需要从头开始访问（无法跳过第一个元素访问任何一个元素）。     <br>
无法通过下标值直接访问元素，需要从头开始一个个访问，直到找到对应的元素。     <br>
虽然可以轻松地到达下一个节点，但是回到前一个节点是很难的。     <br>

append（element）：向链表尾部添加一个新的项；     <br>
insert（position，element）：向链表的特定位置插入一个新的项；     <br>
get（position）：获取对应位置的元素；     <br>
indexOf（element）：返回元素在链表中的索引。如果链表中没有该元素就返回-1；     <br>
update（position，element）：修改某个位置的元素；     <br>
removeAt（position）：从链表的特定位置移除一项；根据位置     <br>
remove（element）：从链表中移除一项；根据元素删除     <br>
isEmpty（）：如果链表中不包含任何元素，返回trun，如果链表长度大于0则返回false；     <br>
size（）：返回链表包含的元素个数，与数组的length属性类似；     <br>
toString（）：由于链表项使用了Node类，就需要重写继承自JavaScript对象默认的toString方法，让其只输出元素的值；     <br>

```js
head  -> node1  ->node2  - >node3  ->null

head指向node1
往链表头加一个元素，newNode.next=this.head(此时值是node1)
this.head(此时值是newNode)=newNode
previous指向current前一个node

<script>
    // 封装单向链表类
    function LinkedList() {
        // 属性
        // 属性head指向链表的第一个节点
        this.head =null
        this.length =0
        // 封装一个内部类：节点类
        function Node(data) {
            this.data=data
            this.next=null
        }

        //append方法
        LinkedList.prototype.append=function (data) {
            //1.创建新节点
            let newNode=new Node(data)
            //2.添加新节点
            //情况1：只有一个节点时候
            if (this.length===0){
                this.head=newNode
            }else {
                //情况2：节点数大于1，在链表的最后添加新节点
                let current=this.head
                //让变量current指向第一个节点
                while (current.next){
                    current=current.next
                    //当current.next(下一个节点不为空)不为空时，一直循环，直到current指向最后一个节点
                }
                // 最后节点的next指向新的节点
                current.next=newNode
            }
            //3.添加完新结点之后length+1
            this.length+=1
        }

        //toString
        LinkedList.prototype.toString=function () {
            let current =this.head
            let string =""
            while (current){
                string+=current.data+' '
                current=current.next
            }
            return string

        }
        //insert
        LinkedList.prototype.insert=function (position,data) {
            let newNode= new Node(data)
            if (position<0||position>this.length){
                return false
            }

            if (position===0){
                newNode.next= this.head
                this.head=newNode
            }else{
                var index=0
                var previous =null
                let current =this.head
                while (index++<position){
                    previous=current;
                    current=current.next;
                }
                newNode.next=current
                previous.next =newNode
            }
            this.length+=1
            return true
        }
        //get(position)
        LinkedList.prototype.get=function (position) {
            if (position<0||position>this.length){
                return false
            }
            var current =this.head
            var index =0
            while (index++<position){
                current=current.next
            }
            return current.data

        }

        //indexOf(element)
        LinkedList.prototype.indexOf=function (element) {
            var current =this.head
            var index=0
            while (current){
                if (current.data===element){
                    return index
                }
                current=current.next
                index+=1
            }
            return  -1
        }

        //update
        LinkedList.prototype.update=function (position,element) {
            if (position<0||position>this.length){
                return false
            }
            var current =this.head
            let index =0
            while(index++<position){
                current=current.next
            }
            current.data=element
            return true
        }

        //removeAt(position)
        LinkedList.prototype.removeAt=function (position) {
            if (position<0||position>this.length){
                return false
            }
            let current =this.head
            let index=0
            let previous=null
            if (position===0){
                this.head=this.head.next
            }else {
                while (index++<position){
                    previous=current
                    current=current.next
                }
                previous.next =current.next
            }
            this.length-=1
            return current.data
        }

        //remove
        LinkedList.prototype.remove=function (element) {
            let position=this.indexOf(element)
            return this.removeAt(position)
        }

        //isEmpty
        LinkedList.prototype.isEmpty=function () {
            return this.length===0
        }

        //size
        LinkedList.prototype.size=function () {
            return this.length
        }
    }
    let list=new LinkedList()
    list.append('a')
    list.append('b')
    list.append('c')
    //3.测试insert方法
    list.insert(0, '在链表最前面插入节点');
    list.insert(2, '在链表中第二个节点后插入节点');
    console.log(list.toString())//a b c
    console.log(list.get(0))
    console.log(list.indexOf('b'))
    console.log(list.update(0,'abc'))
    console.log(list)


</script>

```

#### 双向链表
双向链表：既可以从头遍历到尾，又可以从尾遍历到头。也就是说链表连接的过程是双向的，它的实现原理是：一个节点既有向前连接的引用，也有一个向后连接的引用。

双向链表的缺点：

每次在插入或删除某个节点时，都需要处理四个引用，而不是两个，实现起来会困难些；     <br>
相对于单向链表，所占内存空间更大一些；     <br>
但是，相对于双向链表的便利性而言，这些缺点微不足道。     <br>

双向链表不仅有head指针指向第一个节点，而且有tail指针指向最后一个节点；     <br>
每一个节点由三部分组成：item储存数据、prev指向前一个节点、next指向后一个节点；     <br>
双向链表的第一个节点的prev指向null；     <br>
双向链表的最后一个节点的next指向null；     <br>

append（element）：向链表尾部添加一个新的项；     <br>
insert（position，element）：向链表的特定位置插入一个新的项；     <br>
get（position）：获取对应位置的元素；     <br>
indexOf（element）：返回元素在链表中的索引。如果链表中没有该元素就返回-1；     <br>
update（position，element）：修改某个位置的元素；     <br>
removeAt（position）：从链表的特定位置移除一项；根据位置     <br>
remove（element）：从链表中移除一项；根据元素删除     <br>
isEmpty（）：如果链表中不包含任何元素，返回trun，如果链表长度大于0则返回false；     <br>
size（）：返回链表包含的元素个数，与数组的length属性类似；     <br>
toString（）：由于链表项使用了Node类，就需要重写继承自JavaScript对象默认的toString方法，让其只输出元素的值；     <br>
forwardString: 正向遍历转成字符串的方法     <br>
reverseString: 反向遍历转成字符串的方法     <br>
toString: 正向遍历转成字符串的方法     <br>

```js

 function DoubleLinkedList(){
        function Node(data) {
            this.data=data
            this.next=null
            this.prev=null
        }
        this.head=null
        this.tail=null
        this.length=0

        DoubleLinkedList.prototype.append=function (data) {
            let newNode=new Node(data)
            //添加的是第一个节点
            if (this.length===0){
                this.head=newNode
                this.tail =newNode
            }else{
                //添加不是第一个节点
                newNode.prev=this.tail;
                this.tail.next=newNode
                this.tail=newNode
            }
            this.length+=1
        }

        DoubleLinkedList.prototype.forwardString=function () {
            let current=this.head
            let string=""
            while (current){
                string+=current.data+ " "
                current=current.next
            }
            return string
        }
        DoubleLinkedList.prototype.backString=function () {
            let current =this.tail
            let string=""
            while (current){
                string+=current.data+ " "
                current=current.prev
            }
            return string
        }
        DoubleLinkedList.prototype.toString=function () {
            return this.forwardString()
        }

        DoubleLinkedList.prototype.insert=function (position,element) {
            if (position<0||position>this.length){return false}
            let newNode= new Node(element)
            if (this.length==0){
                this.head=newNode
                this.tail=newNode
            }else if(position===0){
                this.head.prev=newNode
                newNode.next=this.head
                this.head=newNode
            }else if(position==this.length){
                this.tail.next=newNode
                newNode.prev=this.tail
                this.tail=newNode
            }else{
                let index=0
                let current=this.head
                while(index++<position){
                    current=current.next
                }
                newNode.next=current
                newNode.prev =current.prev
                current.prev.next=newNode
                current.prev=newNode
            }
            this.length+=1
            return true
        }
    }
    var list=new DoubleLinkedList()
    list.append('abc')
    list.append('bcd')
    list.append('gth')
    console.log(list)
    console.log(list.forwardString())
    console.log(list.backString())
    console.log(list.forwardString())
    list.insert(1,'a')
    console.log(list.toString())









```


