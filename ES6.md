# ES6


```javascript
函式縮寫
count: function(){} = count(){}，function 冒號拔掉

字串模板
${days*24}

${x<7}?'':'long time long see';
如果小於7 會顯示空字串，如果不是小於7會顯示後面字串，冒號是如果不是就顯示後面字串的意思
----------------------------------

ES5
var double = function(){
  return x*2;
}
宣告一個匿名函式，指定給變數 double


ES6箭頭函式，ES6 省略 ES5 function 關鍵字
const double = (x) =>{
  return x*2;
}


ES6 特性
當參數只有一個的時候可以把小括號省略
const double = x =>{
  return x*2;
}


當函式本體只有一行，又只有 return 的時候可以把大括號省略
const double = x => x*2;




當參數有兩個就不能省略括號
const double = (x,y) =>{
  return x*2;
}


```

ex:
```javascript
ES5
arr.map(function(elm,idx){
  return elm+idx;
});

ES6
arr.map((elm,idx)=>{
  return elm+idx;
})
本體只有一行，所以可以簡化
arr.map((elm,idx) => elm+idx);

```

偵聽ES6寫法
```javascript
btn.addEventListener('click',function(){
  console.log('')
})

變成
btn.addEventListener('click',()=>console.log(''))
```
總結 ES5到ES6 就是把 function & {} 拔掉

---
## 自動綁定
箭頭函式內部的 this 與外部相同
```javascript
const a= () =>{
  console.log(this)
}
console.log(this)
這時候裡面的 this 跟外面的 this 是一樣的
-----------------------------------------
const a= () => {
  console.log(this)
}

const b= () => {
  console.log(this)
}

console.log(this)
那這時候 b 的this 會不會等於外面的 this 就要看情況

不管怎麼執行 a 或是把 a 當物件的屬性，裡面的 this 一定等於外面的 this，
但是 函式 b 的 this 會不會等於外面的 this 要看怎麼執行而定

```


```javascript
const a = () =>{
  console.log(this)
  const aa = () => {
    console.log(this)
  }
}
 console.log(this)
```
如果再 a 函式內又宣告 aa 裡面的 this 一定等於 a 裡面的 this ，也等於最外面的 this ，所以不管在甚麼情境下呼叫箭頭函式裡面的 this ，一定會等於 aa 函式的 this 一定等於 a 的 this ，定等於最外層的 this

---
## this
this 是甚麼東西取決的函式的情境，簡單講就是-怎麼執行這個函式的
### EX1:直接執行 window(global)
```javascript
const name = 'PKTseng'
const sayMyName = function(){
  console.log(this.name)
}
sayMyName()//PKTseng
```
執行 sayMyName this 會指向 window(global) ，那 window 的 name 就是 PKTseng

### EX2:作為物件的成員執行:該物件
宣告一個 teacher 物件，並將 sayMyName 函式指定給 teacher 物件，作為的 sayMyName  的成員函式，當函式被當成物件成員被執行的時候，sayMyName 裡面的 this 就會等於 teacher物件
```javascript
const name = 'PKTseng'
const sayMyName = function(){
  console.log(this.name)
}

const teacher  ={
  name='ken',
}
teacher.sayMyName = sayMyName 

sayMyName();//這邊的 this 是 global 所以 global 的 name 是 PKTseng
teacher.sayMyName();//這就是物件成員函式，這邊的 this 是 teacher 物件
```

### EX3:作為 DOM 的偵聽函式執行: 該 DOM
當我點擊 btn ，這時候的 this 會指向 btn 裡面的 `name="that's really cool"`
```javascript
const name = 'PKTseng'
const sayMyName = function(){
  console.log(this.name)
}

const teacher  ={
  name='ken',
}
teacher.sayMyName = sayMyName 

sayMyName();//PKTseng
teacher.sayMyName();//ken

//這時候有個 btn 
// <button id:btn name="that's really cool">response</button>
btn.addEventListener('click',sayMyName)//that's really cool

// 放一起
sayMyName();//PKTseng
teacher.sayMyName();//ken
btn.addEventListener('click',sayMyName)//that's really cool
```
## 但是!!!
如果我把 sayMyName 改成箭頭函式，這時候 this 會是(global) PKTseng
```javascript
const sayMyName = () => {
  console.log(this.name)
}

sayMyName();//PKTseng
teacher.sayMyName();//PKTseng
btn.addEventListener('click',sayMyName)//PKTseng
```















