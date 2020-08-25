# Vue 組件的 data

## data 必須是函數
範例為簡單的計數器
在第8行用 data 來 return 一個物件，這時的 data 必須是函式。
如果 data 是物件的話，那 counter 是不會被宣告兩次的，但如果 data 是函式的時候，每次只要執行 +1 都會 return 出一個新物件，這樣組件在使用的時候，就不會同時被影響，因為 return 出來的物件都會是新建立的物件
```htmlmixed=
<div id='app'>
  <counter></counter>
  <counter></counter>
</div>

<script>
Vue.component('counter',{
  data(){
    return{
      count: 0,
    }
  },
  template:`
  <div>
    <h1>{{count}}</h1>
    <button @click='count+=1'>+1</button>
  </div>`
})

new Vue({
  el:'#app',
})
</script>
```
[codepen](https://codepen.io/gleofgja/pen/PoNppeB?editors=1011)
![](https://i.imgur.com/U9YN08F.png)

---
## [參考資料:精通 VueJS 前端開發完全指南](https://hiskio.com/courses/145)