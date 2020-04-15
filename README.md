# VueDemo
项目是引用本地下载的vue.js的方式，进行学习Vue

### 事件修饰符：

* .stop       阻止冒泡

* .prevent    阻止默认事件

* .capture    添加事件侦听器时使用事件捕获模式

* .self       只当事件在该元素本身（比如不是子元素）触发时触发回调

* .once       事件只触发一次

### 使用class样式

1. 数组

``` 
<h1 :class="['red', 'thin']">这是一个邪恶的H1</h1>
```

2. 数组中使用三元表达式

``` 
<h1 :class="['red', 'thin', isactive?'active':'']">这是一个邪恶的H1</h1>
```

3. 数组中嵌套对象

``` 
<h1 :class="['red', 'thin', {'active': isactive}]">这是一个邪恶的H1</h1>
```

4. 直接使用对象

``` 
<h1 :class="{red:true, italic:true, active:true, thin:true}">这是一个邪恶的H1</h1>
```

### 使用内联样式

1. 直接在元素上通过 `:style` 的形式，书写样式对象

``` 
<h1 :style="{color: 'red', 'font-size': '40px'}">这是一个善良的H1</h1>
```

2. 将样式对象，定义到 `data` 中，并直接引用到 `:style` 中

 + 在data上定义样式：

``` 
data: {
        h1StyleObj: { color: 'red', 'font-size': '40px', 'font-weight': '200' }
}
```

 + 在元素中，通过属性绑定的形式，将样式对象应用到元素中：

``` 
<h1 :style="h1StyleObj">这是一个善良的H1</h1>
```

3. 在 `:style` 中通过数组，引用多个 `data` 上的样式对象

 + 在data上定义样式：

``` 
data: {
        h1StyleObj: { color: 'red', 'font-size': '40px', 'font-weight': '200' },
        h1StyleObj2: { fontStyle: 'italic' }
}
```

 + 在元素中，通过属性绑定的形式，将样式对象应用到元素中：

``` 
<h1 :style="[h1StyleObj, h1StyleObj2]">这是一个善良的H1</h1>
```

## Vue指令之 `v-if` 和 `v-show` 

* v-if 是惰性的，如果在初始渲染时条件为假，则什么也不做——直到条件第一次变为真时，才会开始渲染条件块。
* v-show 不管初始条件是什么，元素总是会被渲染。v-show 只是简单地切换元素的 CSS 属性 display。
* 一般来说，v-if 有更高的切换消耗，而 v-show 有更高的初始渲染消耗。

 因此，如果需要频繁切换 v-show 较好，如果在运行时条件不大可能改变 v-if 较好。

## Vue调试工具 `vue-devtools` 的安装步骤和使用

[Vue.js devtools - 翻墙安装方式 - 推荐](https://chrome.google.com/webstore/detail/vuejs-devtools/nhdogjmejiglipccpnnnanhbledajbpd?hl=zh-CN)

## 过滤器

概念：Vue.js 允许你自定义过滤器，**可被用作一些常见的文本格式化**。过滤器可以用在两个地方：**mustache 插值和 v-bind 表达式**。过滤器应该被添加在 JavaScript 表达式的尾部，由“管道”符指示；
私有过滤器和全局过滤器名称一致的话，优先调用私有过滤器。

### 私有过滤器

``` 
filters: { // 私有局部过滤器，只能在 当前 VM 对象所控制的 View 区域进行使用
    dataFormat(input, pattern = "") { // 在参数列表中 通过 pattern="" 来指定形参默认值，防止报错
        return ...
  }

```

### 全局过滤器

* 过滤器定义语法：  Vue.filter('过滤器名称', function (data) { return ... })//funnction中第一个参数是管道符前面那个值，后面还可以加参数，是过滤器传值
* 过滤器调用格式：{{name | 过滤器名称}}

## 键盘修饰符以及自定义键盘修饰符

### [2.x中自定义键盘修饰符](https://cn.vuejs.org/v2/guide/events.html#键值修饰符)

1. 通过 `Vue.config.keyCodes.名称 = 按键值` 来自定义案件修饰符的别名：

``` 
Vue.config.keyCodes.f2 = 113;

```

2. 使用自定义的按键修饰符：

``` 
<input type="text" v-model="name" @keyup.f2="add">

```

## [自定义指令](https://cn.vuejs.org/v2/guide/custom-directive.html)

1. 自定义全局和局部的 自定义指令：

``` 
    //自定义全局指令 v-focus，为绑定的元素自动获取焦点：
    Vue.directive('focus', {
      inserted: function (el) { // inserted 表示被绑定元素插入父节点时调用
        el.focus();
      }
    });
```

2. 自定义局部的 自定义指令：

``` 
    //自定义局部指令 v-color 和 v-font-weight，为绑定的元素设置指定的字体颜色 和 字体粗细：
      directives: {
        color: { // 为元素设置指定的字体颜色
          bind(el, binding) {
            el.style.color = binding.value;
          }
        },
        'font-weight': function (el, binding2) { // 自定义指令的简写形式，等同于定义了 bind 和 update 两个钩子函数
          el.style.fontWeight = binding2.value;
        }
      }

```

3. 自定义指令的使用方式：

``` 
<input type="text" v-model="searchName" v-focus v-color="'red'" v-font-weight="900">

```

## [vue实例的生命周期](https://cn.vuejs.org/v2/guide/instance.html#实例生命周期)

* 主要的生命周期函数分类：

 - 创建期间的生命周期函数：

    - beforeCreate：实例刚在内存中被创建出来，此时，还没有初始化好 data 和 methods 属性
    - created：实例已经在内存中创建OK，此时 data 和 methods 已经创建OK，此时还没有开始 编译模板
    - beforeMount：此时已经完成了模板的编译，但是还没有挂载到页面中
    - mounted：此时，已经将编译好的模板，挂载到了页面指定的容器中显示

 - 运行期间的生命周期函数：
 	+ beforeUpdate：状态更新之前执行此函数， 此时 data 中的状态值是最新的，但是界面上显示的 数据还是旧的，因为此时还没有开始重新渲染DOM节点
 	+ updated：实例更新完毕之后调用此函数，此时 data 中的状态值 和 界面上显示的数据，都已经完成了更新，界面已经被重新渲染好了！
 - 销毁期间的生命周期函数：
 	+ beforeDestroy：实例销毁之前调用。在这一步，实例仍然完全可用。
 	+ destroyed：Vue 实例销毁后调用。调用后，Vue 实例指示的所有东西都会解绑定，所有的事件监听器会被移除，所有的子实例也会被销毁。

## [vue-resource 实现 get, post, jsonp请求](https://github.com/pagekit/vue-resource)

除了 vue-resource 之外，还可以使用 `axios` 的第三方包实现实现数据的请求

## 组件的学习

## 路由的学习

