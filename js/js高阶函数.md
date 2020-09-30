#### filter/map/reduce

```
const nums = [10,60,30,20]

// 去除所有小于100的数字
let newNums = nums.filter(function(n){
	return n < 100
})

let newNums = nums.map(function(n){
	return n < 100
})

reduce函数的使用，作用对数组中的数据进行汇总
nums.reduce(function(preValue,n){
	return preValue + n
},0)
第一次：preValue 10
第二次：preValue 70
第三次：preValue 100
第四次：preValue 120
1.for(let n of nums){}


```

