# 使用 v-if 应对初始值为空

此时，如果刷新 /post/1 页面，就会发现终端报错  
Cannot read property 'title' of undefined"

显然这是由于在页面显示的第一时间，this.post 还未加载完成造成的。解决这个问题的方式就是采用 v-if 。

##### PostBody.vue

```js
<template>

  <div class="post-body">
    <div v-if="show">
      <h1>{{ post.title }}</h1>
    </div>
    <div v-else>
      loading...
    </div>
  </div>
</template>
<script>
  export default {
    computed: {
      show() {
        return this.post
      }
    }
  }
</script>
```

PstBody.vue 中，用带有 v-if 指令的 div 包裹会造成报错的部分，判断条件为布尔型变量 show 。如果数据没有加载完毕，我们希望页面上显示 loading 字符串，所以添加 v-else 对应的 div 即可实现这种效果。  
下面来添加计算属性 show 。数据没有加载好的时候，this.post 的值是 undefined ，其布尔型等价为 false ，而当数据加载好之后，this.post 有具体值了，布尔型就等价为 true ，所以这里直接 return this.post 作为 show 的值即可。浏览器中，刷新 /post/1 页面，可以看到首先打印出了 loading 字样，然后标题就显示出来了。
