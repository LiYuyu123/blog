# 排序算法
## 选择排序
~~~
递归写法
let sort=arr=>{
    if(arr.length>2){
       let index=minIdex(arr)
       let min=arr[index]
       arr.splice(index,1)
       return [min].concat(sort(arr))
    }else{
       return arr[0]>arr[1] ? arr.reverse():arr
    }    
}
 let minIndex=arr=>{
   arr.indexOf(min(arr))
} 
let min=arr=>{
   if(arr.length>2){
   return min([arr[0],min(arr.slice(1))])
   }else{
   return Marh.min.apply(null,arr)
   }
}
~~~
~~~
循环写法
let minIndex=arr=>{
  let index=0
  for(let i=1;i<arr.length;i++){
   if(arr[i]<arr[index]){
        index=i
   }
  }
  return index
}
let swap=(array,i,j){
  let temp=array[i]
  array[i]=array[j]
  array[j]=temp
}
let sort=arr=>{
  for(let i=0;i<arr.length;i++){}
      let index=minIndex(arr.slice(i))+i
      if(index!==i){
        swap(arr,index,i)
      }
  return arr
}
~~~
## 快速排序
~~~
let quickSort=arr=>{
if(arr.length<=1){return arr}
let pivoIndex=Marh.floor(arr.length/2)
let pivot=arr.splice(pivoIndex,1)[0]
let left=[]
let right=[]
for(let i=0;i<arr.length;i++){
  if(arr[i]<pivot){left.push(arr[i])}else{right.push(arr[i])}
}
return quickSort(left).concat([pivot],quickSort(right))
}
~~~
## 归并排序
~~~
let mergeSort=arr=>{
   if(arr.length===1){return arr}
   let left=arr.slice(0,Math.floot(arr.length/2))
   let right=arr.slice(Math.floot(arr.length/2))
   return merge(mergeSort(left),mergeSort(right))
}
let merge=(a,b)=>{
  if(a.length===0)return b
  if(b.length===0)retutn a
  return a[0]>b[0] ? [b[0].concat(merge(a,b.slice(1)))]
                     :[a[0].concat(merge(a.slice(1),b))]
}
~~~
## 计数排序
~~~
let countSort=arr=>{
   let hashTable={}
   let max=0
   let result=[]
   for(let i=0;i<arr.length;i++){
     if(!(arr[i] in hashTable)){
        hashTble[arr[i]]=1
     }else{
        hashTable[arr[i]]+=1
     }
     if(arr[i]>max){max=arr[i]}
   }
   for(let j=0;j<=max;j++){
      if(j in hashTable){
        for(let i=0;i<hashTable[j];i++){
          result.push(j)
        }
      }
   }
   return result
}
~~~