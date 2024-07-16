## Vue的核心语法

### 1、插值语法

插值语法在Vue.js中用于动态将数据绑定到DOM中的一种语法，它允许开发者在HTML模板中嵌入JavaScript表达式，Vue会自动将这些表达式的结果插入到页面中。插值语法通常使用双花括号`{{}}`包围表达式

插值语法简单的用法举例：

```html
<div id="app">
  <p>{{ message }}</p>
</div>

<script>
  const app = Vue.createApp({
    data() {
      return {
        message: 'Hello, Vue 3!'
      }
    }
  });
  app.mount('#app');
</script>
```

在页面渲染过程中，`{{message}}`中的值会被替换成JavaScript代码`data`中`message`的值。

**对data的简单解释：**

在Vue.js中，`data`是一个用于定义组件或应用程序状态的对象。它包含了Vue实例中所有的响应式数据属性，这些数据属性可以在模板中进行绑定和使用。每当这些数据属性发生变化时，Vue会自动更新相关的DOM。

### 2、插值语法的分类

##### 2.1、文本插值

将数据绑定到HTML元素的文本内容——使用`{{}}`

```html
<div id="app">
  <p>{{ message }}</p>
</div>

<script>
  const app = Vue.createApp({
    data() {
      return {
        message: 'Hello, Vue 3!'
      }
    }
  });
  app.mount('#app');
</script>

```

##### 2.2、表达式插值

在插值语法中使用简单的JavaScript表达式——使用`{{}}`

```html
<p>{{ number + 1 }}</p>
<p>{{ ok ? 'Yes' : 'No' }}</p>
<p>{{ message.split('').reverse().join('') }}</p>
```

##### 2.3、特性插值

动态绑定HTML元素属性——指令为`v-bind`

```html
<div v-bind:id="dynamicId"></div>
<!-- 缩写形式 -->
<div :id="dynamicId"></div>

<script>
  const app = Vue.createApp({
    data() {
      return {
        dynamicId: 'unique-id'
      }
    }
  });
  app.mount('#app');
</script>
```

##### 2.4、元素插值

将原始的HTML插入到DOM中——指令为`v-html`

```html
<p v-html="rawHtml"></p>

<script>
  const app = Vue.createApp({
    data() {
      return {
        rawHtml: '<span style="color: red;">This is red</span>'
      }
    }
  });
  app.mount('#app');
</script>
```

##### 2.5、列表插值

用于在模板中循环渲染列表——指令为`v-for`

```html
<ul>
  <li v-for="item in items" :key="item.id">{{ item.text }}</li>
</ul>

<script>
  const app = Vue.createApp({
    data() {
      return {
        items: [
          { id: 1, text: 'Item 1' },
          { id: 2, text: 'Item 2' },
          { id: 3, text: 'Item 3' }
        ]
      }
    }
  });
  app.mount('#app');
</script>
```

##### 2.6、条件插值

根据条件渲染内容——指令为`v-if`、`v-else`

```html
<p v-if="seen">现在你看到我了</p>
<p v-else>现在你看不到我了</p>

<script>
  const app = Vue.createApp({
    data() {
      return {
        seen: true
      }
    }
  });
  app.mount('#app');
</script>

```

##### 2.7、样式和类插值

用于动态绑定HTML元素的class和style

**绑定类**

```html
<div :class="{ active: isActive, 'text-danger': hasError }"></div>

<script>
  const app = Vue.createApp({
    data() {
      return {
        isActive: true,
        hasError: false
      }
    }
  });
  app.mount('#app');
</script>

```

**绑定样式**

```html
<div :style="{ color: activeColor, fontSize: fontSize + 'px' }"></div>

<script>
  const app = Vue.createApp({
    data() {
      return {
        activeColor: 'red',
        fontSize: 14
      }
    }
  });
  app.mount('#app');
</script>
```

##### 2.8、事件处理

用于事件绑定——指令为`v-on`

```html
<button v-on:click="doSomething">点击我</button>
<!-- 缩写形式 -->
<button @click="doSomething">点击我</button>

<script>
  const app = Vue.createApp({
    methods: {
      doSomething() {
        alert('按钮被点击了');
      }
    }
  });
  app.mount('#app');
</script>
```

在方法中，可以使用`this`关键字来访问获取和修改`data`中的属性：

```html
<div id="app">
  <p>{{ message }}</p>
</div>

<script>
  const app = Vue.createApp({
    data() {
      return {
        message: 'Hello, Vue 3!'
      }
    },
    methods: {
  	  changeMethod() {
        this.message = '你好 vue！';
      }
    }
  });
  app.mount('#app');
</script>
```

### 3、计算属性

```html
<div id="app">
    <p>{{getResult}}</p>
</div>

<script>
    const { createApp } = Vue
    createApp({
        data() {
            return {
                massage: 'hello'
            }
        },

        computed: {
            getResult() {
                return 100;
            }
        }
    }).mount('#app')
</script>
```

