# vuex_todos
用vuex，axios做了个TodoApp

跟着brad做了个todoapp，用的是vuex，axios，

* [视频项目](https://www.youtube.com/watch?v=5lVQgZzLMHc)
* [项目源代码](https://github.com/bradtraversy/vuex_todo_manager)
* [他的频道](https://www.youtube.com/channel/UC29ju8bIPH5as8OGnQzwJyA)

他用的是组件的形式来完成项目，我用的是cdn，功能一模一样，作为初学者在完成项目的过程中发现了下面几种问题

项目结构:
  1. index.html  主页，
  2. store.js vuex的store再这个文件
  3. 用的是这个[开源数据](https://jsonplaceholder.typicode.com/todos)，不知道是否需要科学上网

1. vuex用cdn的时候如果用mapGetters,mapActions之类的话前面加个Vuex就行了，比如Vuex.mapActions()
2. 一定要记住getters要是改变的数据的话只能改变一边。
3. 需要改变的数据都在mutations里完成的。
4. 用axios来获取数据一定要注意异步，asynx/await 来完成，然后数据提交给mutations的方法，修改数据的操作mutations里的方法完成
5. 重要的一点是获取数据也就是maoGetters的话用在computed里，所有的mapActions在methods来完成的，方法在这儿写，调用的话其他地方也可以调用。比如第一次获取初始化数据，在methods里边的方法写个函数，然后再created或mounted等方法中调用该函数就行了。
6. 最后一个要点要是能掌握辅助函数可以大大大的提高效率了。

做个笔记：

```html
 <select name="" @change="filterTodos($event)" id="">
          <option value="200" selected>choose</option>
          <option value="150">150</option>
          <option value="50">50</option>
          <option value="10">10</option>
          <option value="5">5</option>
          <option value="1">1</option>
  </select>
```

用vue怎么获取select的值呢？？

```javascript
 async filterTodos({commit},e){
          
            var limit=parseInt(e.target.options[e.target.options.selectedIndex].innerText)
            const response=await axios.get(`https://jsonplaceholder.typicode.com/todos?_limit=${limit}`);
            commit('setTodos',response.data);
            
        }
```
再调用函数的时候要要有个参数一定是$event,在函数中用个变量来获取就行，获取那个调用事件的元素，一般用e来拿取。

* 用async的函数一般返回promise

最后一点有个小bug就是自己添加数据，然后改变状态不起作用，因为我们的数据不是添加的服务器，改变状态的函数是获取服务器数据的

```javascript
// 要发到服务器，我们的数据不在服务器内，所以不起作用，要注意。
 async updateTodo({commit}, updTodo){
            const response=await axios.put(`https://jsonplaceholder.typicode.com/todos/${updTodo.id}`,updTodo);
            console.log(response.data);
            commit('updateTodo',response.data);
        }

```









