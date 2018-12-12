# 这里记录的一些ES5和ES6一些常用的方法，防止自己忘记

for in 和for of的区别  
* for in是ES5标准，遍历key.
* for of是ES6标准，遍历value.  

      for (var key in arr){
        console.log(arr[key]);
      }
      for (var value of arr){
        console.log(value);
      }


ES6的异步语法是geneater，ES7开始推荐的async和await  

filter()是用来过滤的，mapping()是用来循环的。
