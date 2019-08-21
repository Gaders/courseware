# Vue.js #

在我们学习vue.js之前，了解vue.js是什么东西，它的设计理念又是怎样的，它又有什么不可忽视的特定。这对我们来说是十分必要的东西。

## Vue.js是什么东西 ##

对于这种概念性的问题，vue的官方文档就能给我们一个答案，那么这里就先引用一段vue官方文档的话。

**Vue** (读音 /vjuː/，类似于 **view**) 是一套用于构建用户界面的**渐进式框架**。与其它大型框架不同的是，Vue 被设计为可以**自底向上逐层应用** 。Vue 的核心库只关注视图层，不仅易于上手，还便于与第三方库或既有项目整合。另一方面，当与[现代化的工具链](https://cn.vuejs.org/v2/guide/single-file-components.html)以及各种[支持类库](https://github.com/vuejs/awesome-vue#libraries--plugins)结合使用时，Vue 也完全能够为复杂的单页应用提供驱动。

啊 为什么这些字我都认识但是把他们连在一起之后。。。我怎么就看不是很懂了。虽然我不晓得各位看到这段话的时候是什么感觉，反正我是挺懵的。那我们针对这段话进行一下解析。

- ### 渐进式框架 ###

Vue向我们提供了很多的选择，其官方文档里边数不胜数的各种api就是一个很好的例子。但与此同时，Vue并没有给我们很多强制性的要求。就像官方文档里说的那样，这是一个渐进式的框架，渐进就是一步一步的意思，在我们使用Vue框架进行开发的时候，我们不需要用上所有的东西，而是根据我们的实际需求去选择性地使用。

![图片1](https://upload-images.jianshu.io/upload_images/17668445-d154c4e3d6f59b6d.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1000/format/webp)

在图中我们可以很轻易地看出声明式渲染和组件系统是Vue的核心库内容，而其他的几项，诸如路由，状态管理，构建工具都有各自独立的解决方案。我们在开发时可以以声明式渲染和组件系统为基础，然后根据自己需求渐进地使用其他部分，而不是将其全部整合在一起。

- ### 自下而上逐从层应用 ###

由基层开始做起，把基础的东西写好，再逐层往上添加效果和功能。在我们开发一些样式功能较为复杂的组件时，我们总是会先把最为底层的结构先写出来，再往上添加css样式以及我们希望它实现目标功能的js代码。

## 我们为什么需要学习Vue ##

Vue作为近年来最火的几种前端框架之一，其使用的普遍性已经不容我们去质疑。为了更好地提升我们的开发速度，学习使用框架已经是不可避免的了。就像这次暑假的项目，要是用原生的js去写，天知道会多花多长时间，而且代码的维护性和复用性会变得很差，可以说是吃力还不讨好的事情了。

#### Vue和jQuery的区别 ####

1. 操作思想的转变-----在我们还在使用jQuery的时候，我们频繁地使用$( )去获取我们的DOM元素，然后再去修改相应的属性，值，抑或是绑定事件。此时我们的操作是以DOM元素作为核心的。

   ```html
   <html>
       <input type="text">
   </html>
   <script>
       $("input").val("我要改变框内的值")
   </script>
   ```



   ​	而在Vue中，数据和视图完全分离了出来，我们操作数据不需要获取相对应的DOM元素。

```vue
<template>
  <div id="app">
    <input type="text" v-model="value">
    {{value}}
  </div>
</template>

<script>
export default {
  name: 'app',
  data() {
    return {
      value: "我要改变框内的值"
    }
  },
}
</script>

```

这里使用了v-model进行数据和视图的双向绑定，对数据的修改不再依赖对相应视图的获取，它们是完全分离的，但是通过双向绑定这一功能，数据能够影响着视图，视图也能够改变数据。这也就是我们所说的MVVM。

2.代码的便利性--在我们使用原生的js或是jQurey去实现点击按钮去添加一条数据的时候，我们需要去手动写一个新的标签。

```html
<body>
    <div id="app">
        <ul id="list">
            <li>第1条数据</li>
            <li>第2条数据</li>
        </ul>
        <button id="add">添加数据</button>
    </div>

</body>
<script>
    var i=2;
    $('#add').click(function() { 
       i++; 
       //通过dom操作手动添加一个li标签
      $("#list").children("li").last().append("<li>第"+i+"条数据</li>")
    });  
</script>
```

但是一旦DOM的结构变得十分复杂，或者是我们需要添加的元素结构十分复杂的时候，我们编写代码以及维护代码就会变得十分困难。但是如果我们使用Vue来实现这个功能，我们只需要用v-for来渲染数据，然后往数组里push一条新数据即可。

```vue
<template>
  <div id="app">
     <ul>
        <!--根据数组自动渲染页面-->
        <li v-for="item in msg">{{item}}</li>
      </ul>
      <button @click="add">添加数据</button>
  </div>
</template>

<script>
export default {
  name: 'app',
  data() {
    return {
      msg: ["第1条数据","第2条数据"]
    }
  },
  methods: {
    add() {
      this.msg.push("第"+(this.msg.length+1)+"条数据")
    }
  }
}
</script>
```

## 学习Vue ##

### 安装Vue ###

学习第一步，从安装开始。这里就只介绍Vue官方文档中所提供的npm方法安装Vue，虽然我知道大家应该都已经安装过了。

```shell
# 最新稳定版
$ npm install vue
```



以及Vue的脚手架Vue-CLI的安装

```shell
npm install -g @vue/cli
# OR
yarn global add @vue/cli
```

安装完成之后我们就可以愉快地使用Vue来快速创建我们的项目了。

```shell
vue create my-project
```

### 目录结构 ###

### 插值 ###

按照国际惯例，我们从写一个hello world开始介绍Vue的一些写法。以下代码会在页面中显示hello world。

```vue
<template>
  <div id="app">
    {{msg}}
  </div>
</template>

<script>
export default {
  name: 'app',
  data() {
    return {
      msg: "hello world"
    }
  },
}
</script>


```

当然在{{}}里我们还能够写入js表达式.要注意控制流是不被允许的，我们应该用三元表达式去代替它。

```vue
<template>
  <div id="app">
    {{msg == "hello world"}}
  </div>
</template>

<script>
export default {
  name: 'app',
  data() {
    return {
      msg: "hello world"
    }
  },
}
</script>
```

### v-html ###

我们可以使用v-html插入html语句

```vue
<template>
  <div id="app" v-html="msg">
  </div>
</template>

<script>
export default {
  name: 'app',
  data() {
    return {
      msg: "<p style='color:red'>插入的html</p>"
    }
  },
}
</script>
```

### v-for ###

接下来我们可以尝试输出一串组成hello world的列表。v-for用于遍历一个数组或对象，然后根据遍历的结果来渲染出一串列表。

``` vue
<template>
  <div id="app">
    <ul>
      <li v-for="(item,index) in arr ">{{item}}--{{index}}</li>
    </ul>
  </div>
</template>

<script>
export default {
  name: 'app',
  data() {
    return {
      arr: ["h","e","l","l","o","w","o","r","l","d"],
      str: "helloworld",
      obj: {
        name: "helloworld"
      }
    }
  },
}
</script>
```

### v-if ###

在使用v-for遍历数组的时候我们会得到一个index属性可供使用，如果我们配合上v-if就能实现简单的交错显示。

``` vue
<template>
  <div id="app">
    <ul>
      <li v-for="(item,index) in msg " v-if="index % 2 == 0">{{item}}</li>
    </ul>
  </div>
</template>

<script>
export default {
  name: 'app',
  data() {
    return {
      msg: [1，2，3，4，5] 
    }
  },
}
</script>
```

### v-bind ###

v-bind用于动态地绑定特性。可以缩写为 ：进行使用，我们通常使用v-bind来绑定一些需要动态变化的特性，例如图片或者视频的地址我们可以用v-bind:src进行绑定，div的style和class也可以进行绑定。

```vue
<template>
  <div id="app">
    <ul>
      <li v-for="(item,index) in msg " v-bind:style="{color:'red'}" v-bind:class="{blue: true }">{{item}}</li>
    </ul>
  </div>
</template>

<script>
export default {
  name: 'app',
  data() {
    return {
      msg: "helloworld"
    }
  },
}
</script>

<style lang="scss" scoped>
.blue {
  color:blue;
}
</style>
```

### v-on ###

v-on是用来绑定事件监听器的，就跟js里的addEventListener()差不多。通常我们写成v-on:click，或者直接简写为@click也是可以的。举个栗子，我们可以用v-on来制作一个能让上面列表颜色交替显示的简单事件。

```vue
<template>
  <div id="app">
    <ul>
      <li v-for="(item,index) in msg " v-bind:class="{red: (flag + index) % 2 == 0}">{{item}}</li>
    </ul>
    <button @click="changeColor()">点我切换颜色</button>
  </div>
</template>

<script>
export default {
  name: 'app',
  data() {
    return {
      msg: ["h","e","l","l","o","w","o","r","l","d"] ,
      flag: 1,
    }
  },
  methods: {
    changeColor() {
      this.flag ? this.flag = 0 : this.flag = 1
    }
  }
}
</script>

<style lang="scss" scoped>
.red {
  color:red;
}
</style>
```

### v-model

v-model常用于实现双向绑定，它工作的预期表现会跟据其表单控件类型的不同而有所差异。

```vue
<template>
  <div id="app">
      <input type="text" v-model="input">{{input}}
      <textarea v-model="textarea"></textarea>{{textarea}}
      <input type="checkbox" v-model="checkbox">{{checkbox}}
  </div>
</template>

<script>
export default {
  name: 'app',
  data() {
    return {
      input:"我是文本框",
      textarea:"我是文本域",
      checkbox:"我是单选框"
    }
  },
}
</script>
```

### computed

Vue所提供的计算属性功能，它可以用于处理复杂的逻辑。例如我们在使用{{}}直接插入一段js表达式的时候，如果我们所插入的内容逻辑过于复杂，会对我们浏览代码，理解代码以及维护代码造成很大的阻碍，所以我们可以通过computed来进行较为复杂的逻辑处理。例如我们可以相应式地获取上面helloworld字符串的倒序，并且渲染在页面中。

```vue
<template>
  <div id="app">
    <ul>
      <li v-for="(item,index) in reserveStr ">{{item}}--{{index}}</li>
    </ul>
  </div>
</template>

<script>
export default {
  name: 'app',
  data() {
    return {
      str: "helloworld",
    }
  },
  computed: {
    reserveStr: function() {
      return this.str.split("").reverse().join("")
    }
  }
}
</script>
```

### data以及methods

数据以及方法，上面的各种例子中已经包括了这两种选项的简单用法，前者为我们提供页面中需要的数据，后者存放了我们各种事件处理方法。

### 生命周期与钩子

[这里有个中文注释的生命周期图](https://www.cnblogs.com/zdz8207/p/vue-lifecycle.html)

Vue实例有一个完整的生命周期，也就是从开始创建、初始化数据、编译模板、挂载Dom、渲染→更新→渲染、销毁等一系列过程，我们称这是Vue的生命周期。通俗说就是Vue实例从创建到销毁的过程，就是生命周期。

每一个组件或者实例都会经历一个完整的生命周期，总共分为三个阶段：初始化、运行中、销毁。

1. 实例、组件通过new Vue() 创建出来之后会初始化事件和生命周期，然后就会执行beforeCreate钩子函数，这个时候，数据还没有挂载呢，只是一个空壳，无法访问到数据和真实的dom，一般不做操作
2. 挂载数据，绑定事件等等，然后执行created函数，这个时候已经可以使用到数据，也可以更改数据,在这里更改数据不会触发updated函数，在这里可以在渲染前倒数第二次更改数据的机会，不会触发其他的钩子函数，一般可以在这里做初始数据的获取
3. 接下来开始找实例或者组件对应的模板，编译模板为虚拟dom放入到render函数中准备渲染，然后执行beforeMount钩子函数，在这个函数中虚拟dom已经创建完成，马上就要渲染,在这里也可以更改数据，不会触发updated，在这里可以在渲染前最后一次更改数据的机会，不会触发其他的钩子函数，一般可以在这里做初始数据的获取
4. 接下来开始render，渲染出真实dom，然后执行mounted钩子函数，此时，组件已经出现在页面中，数据、真实dom都已经处理好了,事件都已经挂载好了，可以在这里操作真实dom等事情...
5. 当组件或实例的数据更改之后，会立即执行beforeUpdate，然后vue的虚拟dom机制会重新构建虚拟dom与上一次的虚拟dom树利用diff算法进行对比之后重新渲染，一般不做什么事儿
6. 当更新完成后，执行updated，数据已经更改完成，dom也重新render完成，可以操作更新后的虚拟dom
7. 当经过某种途径调用$destroy方法后，立即执行beforeDestroy，一般在这里做一些善后工作，例如清除计时器、清除非指令绑定的事件等等
8. 组件的数据绑定、监听...去掉后只剩下dom空壳，这个时候，执行destroyed，在这里做善后工作也可以



### components

​        组件化的开发对我们来说是很重要的一种思想。组件化的开发模式可以给我们的项目代码带来以往难以想象的复用性，可维护性。例如网页中一些常见的，需要大量复用的按钮部分，如果我们不把他们抽离出来变成组件去开发，我们可能就要做大量的复制粘贴的体力活。并且最后如果需要修改其样式或者value，我们可能又要一个一个辛酸地去改。这样就极大地降低了代码的复用性和可维护性。因此，组件化的思想是极其必要的。

以下是单文件组件，也就是.vue文件的基本格式。

```vue
<template>
    <div id="root"> 
        <!-- 组件内规定所有元素都要被一个根元素包裹 -->
    </div>
</template>

<script>
export default {

}
</script>

<style lang="scss" scoped> //scoped代表此处的css样式仅在当前组件内生效，不会影响到外部

</style>
```

组件的导入以及注册也是十分简单的，只要看过一遍就很容易学会。

```vue
<template>
  <div id="app">
    <myComponents></myComponents> <!-- 组件的实例 -->
  </div>
</template>

<script>
import myComponents from './components/test' //以组件的相对路径导入组件
export default {
  name: 'app',
  components: {
    myComponents, //注册组件
  }
}
</script>
```

#### slot插槽

slot可以说是组件内一个相当好用的标签了，它可以快捷地把内容嵌入到组件内你预先设定好的位置，比如给按钮组件嵌入不同的文字就能快速实现组件的复用。虽然给组件传参也能实现这个功能，但是用slot来实现简单的文本插入更加快捷。

```vue
<template>
  <div id="app">
    <myComponents>
      通过slot插槽插入的文字
      <button>通过slot插槽插入的按钮</button>
    </myComponents>
  </div>
</template>

<script>
import myComponents from './components/test'
export default {
  name: 'app',
  components: {
    myComponents,
  }
}
</script>

```

#### prop

我们可以通过设置组件的prop来实现自定义属性的功能，并且可以自由地设置各属性的名称以及接受的参数类型。

```vue
<script>
export default {
    props: {
        title: String,
        num: Number,
        obj: Object,
        ary: Array,
    }
}
</script>
```

然后在使用这个组件的时候把希望其属性获得的参数填上即可。												

```vue
<template>
  <div id="app">
    <myComponents :title="'我是字符串'" :obj="{1:'我是对象'}" :num="1" :ary="[1,2,3]">
    </myComponents >
  </div>
</template>
```

如果传入的参数类型与之前所规定的类型不一致则会报错。

## 总结

在对Vue的学习中确实获益良多，虽然我也才刚刚入门，能够讲的东西也十分简单。我对Vue的学习很可能不及各位，但是Vue这个框架确实不仅提高了我的开发效率，也改变了我的一些开发思路。希望大家都能在对Vue的学习之中有所收获。



## 一些参考链接

[我们为什么要学习Vue](https://www.jianshu.com/p/c4e892715be1)

[Vue生命周期中英文版](https://www.cnblogs.com/zdz8207/p/vue-lifecycle.html)

