### 嵌套数组指定层次展开 flat扁平化

  嵌套数组指定层次展开 flat扁平化   <br>
  数组的扁平化即为将一个嵌套多层的数组转换为只有一层的数组   <br>
  [1, 2, [3, 4, [5, 6]]] => [1, 2, 3, 4, 5, 6]   <br>
  递归  通过遍历最外层数组的每一个元素，看看是否还是数组，如果是的话，继续递归执行，不是的话，放到最后的结果数组当中   <br>
  
  方法一：递归不适应闭包
  ```js
   //递归 递：展开  归：合并
    // Array.concat(arr1,arr2...)，合并两个或多个数组，生成一个新的数组。原数组不变
    function flattenMd(arr) {
        let result=[]
        arr.forEach(item=>{
            if (Array.isArray(item)){
                result=result.concat(flattenMd(item))
            }else {
                result.push(item)
            }
        })
        return result
    }
    var ary = [1, [2, [3, [4, 5]]], 6]
    console.log(flattenMd(ary))
```
