# Vue代码规范

## 目录
[命名规范](#命名规范)

[结构化规范](#结构化规范)

[注释规范](#注释规范)

[编码规范](#编码规范)

[CSS规范](#css规范)

[Sass规范](#sass规范)

[特殊规范](#特殊规范)

[参考](#参考)
## 命名规范
### 变量命名
* 命名方法 ：驼峰命名法
* 命名规范 ：
命名需有相关性如
 ```javascript
const mySchool = "我的学校";
```
命名是复数的时候需要加s 
```javascript
const names = new Array();
```

### 常量命名

* 命名方法 : 全部大写
* 命名规范 : 使用大写字母和下划线来组合命名，下划线用以分割单词。
```javascript
const MAX_COUNT = 10
const URL = 'https://www.baidu.com/'
```

### 组件命名规范
PascalCase (单词首字母大写命名)是最通用的声明约定
kebab-case (短横线分隔命名) 是最通用的使用约定

* 组件名应该始终是多个单词的，根组件 App 除外
* 有意义的名词、简短、具有可读性
* 命名遵循 PascalCase 约定
    * 基础组件名: 以Base(次选App、V) 开头。
    
        Good： BaseDatePicker,BaseTable (AppContainer) 
        
        Bad: VueHeader,MyHeader
        
    * 紧密耦合的组件名: 和父组件紧密耦合的子组件应该以父组件名作为前缀命名。
    
        Good: TodoList.vue TodoListItem.vue

* 使用遵循 kebab-case 约定
    * 在页面中使用组件需要前后闭合，并以短线分隔
    
        Good:<base-component></base-component>
        
        Bad: <basecomponent></basecomponent>
* 完整单词的组件名
    * 组件名应该倾向于完整单词而不是缩写 
    
        Good: UserProfileOptions.vue
        
        Bad: UProfOpts.vue
* Prop 名大小写
    * 在声明 prop 的时候，其命名应该始终使用 camelCase，而在模板和 JSX 中应该始终使用 kebab-case
    
        Good:
        ```javascript
          props: {
            greetingText: String
          }
          <welcome-message greeting-text="hi"></welcome-message>
        ```
        Bad:
        ```javascript
          props: {
            greetingText: String
          }
          <welcome-message greetingText="hi"></welcome-message>
        ```
       
* method 方法命名规范
    * 驼峰式命名，统一使用动词或者动词+名词形式 
    * 尽量使用常用单词开头（set、get、go、can、has、is）
    
## 结构化规范
### 目录文件夹及子文件规范
待更
### vue文件基本结构
```html
  <template>
    <div>
      <!--必须在div中编写页面-->
    </div>
  </template>
  <script>
    export default {
      components : {
      },
      data () {
        return {
        }
      },
      mounted() {
      },
      methods: {
      }
   }
  </script>
  <!--声明语言，并且添加scoped-->
  <style lang="scss" scoped>
  </style>

```
### 组件选项顺序
```
  - components
  - props
  - data
  - computed
  - watch
  - created
  - mounted
  - metods
  - filter
  - beforeDestroy

```
## 注释规范

1. 公共组件使用说明
2. 各组件中重要函数或者类说明
3. 复杂的业务逻辑处理说明
4. 特殊情况的代码处理说明,对于代码中特殊用途的变量、存在临界值、函数中使用的 hack、使用了某种算法或思路等需要进行注释描述
5. 多重 if 判断语句

### 单行注释
注释单独一行，不要在代码后的同一行内加注释，//后面要加空格。例如：
```javascript
  // bad

  var name = 'aaa' // 姓名
  //姓名    
  var name = 'aaa'    

  // good

  // 姓名
  var name = 'aaa'
```

### 多行注释
注释单独一行，不要在代码后的同一行内加注释，//后面要加空格。例如：
```javascript
// 组件使用说明，和调用说明
     /**
     * 组件名称
     * @module 组件存放位置
     * @desc 组件描述
     * @author 组件作者
     * @date 2017年12月05日17:22:43
     * @param {Object} [title]    - 参数说明
     * @param {String} [columns] - 参数说明
     * @example 调用示例
     *  <hbTable :title="title" :columns="columns" :tableData="tableData"></hbTable>
     **/
```
## 编码规范
统一的编码规范，有利于项目代码的一致性，易于阅读、理解和维护。大大提高开发效率。
### 源码风格
1. 定义变量使用 let ,定义常量使用 const
2. 静态字符串一律使用单引号或反引号，动态字符串使用反引号
    ```javascript
      // bad
      const a = 'foobar'
      const b = 'foo' + a + 'bar'
      const c = `foobar`
    
      // good
      const a = 'foobar'
      const b = `foo${a}bar`
      const c = 'foobar'
    ```
3. 解构赋值

    数组成员对变量赋值时，优先使用解构赋值
    ```javascript
      // 数组解构赋值
      const arr = [1, 2, 3, 4]
      // bad
      const first = arr[0]
      const second = arr[1]
    
      // good
      const [first, second] = arr
    ```
    函数的参数如果是对象的成员，优先使用解构赋值
    ```javascript
    // 对象解构赋值
      // bad
      function getFullName(user) {
        const firstName = user.firstName
        const lastName = user.lastName
      }
    
      // good
      function getFullName(obj) {
        const { firstName, lastName } = obj
      }
    
      // best
      function getFullName({ firstName, lastName }) {}
    
    ```
4. 拷贝数组
    
    使用扩展运算符（...）拷贝数组。
    ```javascript
    const items = [1, 2, 3, 4, 5]
    
      // bad
      const itemsCopy = items
    
      // good
      const itemsCopy = [...items]
    ```
5. 箭头函数

    需要使用函数表达式的场合，尽量用箭头函数代替。因为这样更简洁，而且绑定了 this
    ```javascript
    // bad
      const self = this;
      const boundMethod = function(...params) {
        return method.apply(self, params);
      }
    
      // acceptable
      const boundMethod = method.bind(this);
    
      // best
      const boundMethod = (...params) => method.apply(this, params);
    ```
6. 模块

    如果模块只有一个输出值，就使用 export default，如果模块有多个输出值，就不使用 export default，export default 与普通的 export 不要同时使用
    ```javascript
     // bad
      import * as myObject from './importModule'
    
      // good
      import myObject from './importModule'
    
    ```
     如果模块默认输出一个函数，函数名的首字母应该小写。
     ```javascript
      function makeStyleGuide() {
      }
    
      export default makeStyleGuide;
     ```

    如果模块默认输出一个对象，对象名的首字母应该大写。
    ```javascript
    const StyleGuide = {
        es6: {
        }
    };
    
    export default StyleGuide;
    ```
### 指令规范

1. 指令有缩写一律采用缩写形式
```html
 // bad
  v-bind:class="{'show-left'：true}"
  v-on:click="getListData"

  // good
  :class="{'show-left'：true}"
  @click="getListData"
```
2. v-for 循环必须加上 key 属性，在整个 for 循环中 key 需要唯一
```html
  <!-- good -->
  <ul>
    <li v-for="todo in todos" :key="todo.id">
      {{ todo.text }}
    </li>
  </ul>

  <!-- bad -->
  <ul>
    <li v-for="todo in todos">
      {{ todo.text }}
    </li>
  </ul>

```
3. 避免 v-if 和 v-for 同时用在一个元素上（性能问题）
以下为两种解决方案：

    * 将数据替换为一个计算属性，让其返回过滤后的列表

        ```html
            <!-- bad -->
            <ul>
                <li v-for="user in users" v-if="user.isActive" :key="user.id">
                  {{ user.name }}
                </li>
            </ul>
            
            <!-- good -->
            <ul>
                <li v-for="user in activeUsers" :key="user.id">
                  {{ user.name }}
                </li>
            </ul>
            
            <script>
            computed: {
                activeUsers: function () {
                  return this.users.filter(function (user) {
                    return user.isActive
                  })
                }
            }
            </script>
        ```
    * 将 v-if 移动至容器元素上 (比如 ul, ol)
        ```html
        <!-- bad -->
          <ul>
            <li v-for="user in users" v-if="shouldShowUsers" :key="user.id">
              {{ user.name }}
            </li>
          </ul>
        
          <!-- good -->
          <ul v-if="shouldShowUsers">
            <li v-for="user in users" :key="user.id">
              {{ user.name }}
            </li>
          </ul>
        ```
### Props规范
Props 定义应该尽量详细
```
// bad 这样做只有开发原型系统时可以接受
props: ['status']

// good
props: {
  status: {
    type: String,
    required: true,
    validator: function (value) {
      return [
        'syncing',
        'synced',
        'version-conflict',
        'error'
      ].indexOf(value) !== -1
    }
  }
}
```
## CSS规范
### 通用规范

1. 统一使用"-"连字符
2. 省略值为 0 时的单位
    ```
     // bad
      padding-bottom: 0px;
      margin: 0em;
    
     // good
      padding-bottom: 0;
      margin: 0;
    ```
3. 如果 CSS 可以做到，就不要使用 JS
4. 建议并适当缩写值，提高可读性，特殊情况除外
    “建议并适当”是因为缩写总是会包含一系列的值，而有时候我们并不希望设置某一值，反而造成了麻烦，那么这时候你可以不缩写，而是分开写。
    当然，在一切可以缩写的情况下，请务必缩写，它最大的好处就是节省了字节，便于维护，并使阅读更加一目了然。
    ```
     // bad
     .box{
       border-top-style: none;
       font-family: palatino, georgia, serif;
       font-size: 100%;
       line-height: 1.6;
       padding-bottom: 2em;
       padding-left: 1em;
       padding-right: 1em;
       padding-top: 0;
     }
   
     // good
     .box{
       border-top: 0;
       font: 100%/1.6 palatino, georgia, serif;
       padding: 0 1em 2em;
     }
    ```
5. 声明应该按照下表的顺序

    左到右，从上到下

    | 显示属性 | 自身属性 | 文本属性和其他修饰 |
    |:--------: |:-------:|:----------------:|
    | display | width | font |
    | visibility | height | text-align | 
    | position | margin | text-decoration | 
    | float | padding | vertical-align | 
    | clear | border | white-space | 
    | list-style | overflow | color | 
    | top | min-width | background | 
    ```
      // bad
      .box {
        font-family: 'Arial', sans-serif;
        border: 3px solid #ddd;
        left: 30%;
        position: absolute;
        text-transform: uppercase;
        background-color: #eee;
        right: 30%;
        isplay: block;
        font-size: 1.5rem;
        overflow: hidden;
        padding: 1em;
        margin: 1em;
      }
    
      // good
      .box {
        display: block;
        position: absolute;
        left: 30%;
        right: 30%;
        overflow: hidden;
        margin: 1em;
        padding: 1em;
        background-color: #eee;
        border: 3px solid #ddd;
        font-family: 'Arial', sans-serif;
        font-size: 1.5rem;
        text-transform: uppercase;
      }
    ```
6. 元素选择器应该避免在 scoped 中出现
    
    官方文档说明：在 scoped 样式中，类选择器比元素选择器更好，因为大量使用元素选择器是很慢的。

7. 统一语义理解和命名

|语义|命名|~~简写~~|
|---|---|---|
|文档|doc|doc|
|头部|header|header|
|主体|body|body|
|尾部|footer|footer|
|主栏|main|main|
|子|sub-|-|
|侧栏|side|-|
|盒容器|wrap/box|wrap/box|
|导航|nav|nav|
|面包屑|crumb|crm|
|菜单|menu|menu|
|选项卡|tab|tab|
|标题区|head/title|-|
|内容区|body/content|-|
|列表|list|-|
|表格|table|-|
|表单|form|-|
|热点|hot|hot|
|排行|top|top|
|登录|login|-|
|标志|logo|logo|
|广告|advertise|ad|
|搜索|search|-|
|幻灯|slide|-|
|提示|tips|tips|
|帮助|help|help|
|新闻|news|news|
|下载|download|-|
|注册|regist|-|
|投票|vote|vote|
|版权|copyright|-|
|结果|result|-|
|标题|title|-|
|按钮|button|btn|
|输入|input|-|
|浮动清除|-|cb|
|向左浮动|-|fl|
|向右浮动|-|fr|
|内联块级|inline-block|ib|
|文本居中|-|tc|
|文本居右|-|tr|
|文本居左|-|tl|
|溢出隐藏|overflow-hidden|oh|
|完全消失|display-none|dn|
|字体大小|font-size|fs|
|字体粗细|font-weight|fw|
|宽度|-|w|
|百分比宽度|-|w-100|
|字体颜色|fontcolor|fc|
|背景|background|bg|
|选中|selected|-|
|当前|current|-|
|显示|show|show|
|隐藏|hide|hide|
|打开|open|open|
|关闭|close|close|
|出错|error|err|
|不可用|disabled|-|
## Sass规范

当使用 Sass 的嵌套功能的时候，重要的是有一个明确的嵌套顺序，以下内容是一个 SCSS 块应具有的顺序。

1. 当前选择器的样式属性
1. 父级选择器的伪类选择器 (:first-letter, :hover, :active etc)
1. 伪类元素 (:before and :after)
1. 父级选择器的声明样式 (.selected, .active, .enlarged etc.)
1. 用 Sass 的上下文媒体查询
1. 子选择器作为最后的部分
    ```
    .product-teaser {
        // 1. Style attributes
        display: inline-block;
        padding: 1rem;
        background-color: whitesmoke;
        color: grey;
    
        // 2. Pseudo selectors with parent selector
        &:hover {
          color: black;
        }
    
        // 3. Pseudo elements with parent selector
        &:before {
          content: "";
          display: block;
          border-top: 1px solid grey;
        }
    
        &:after {
          content: "";
          display: block;
          border-top: 1px solid grey;
        }
    
        // 4. State classes with parent selector
        &.active {
          background-color: pink;
          color: red;
    
          // 4.2. Pseuso selector in state class selector
          &:hover {
            color: darkred;
          }
        }
    
        // 5. Contextual media queries
        @media screen and (max-width: 640px) {
          display: block;
          font-size: 2em;
        }
    
        // 6. Sub selectors
        > .content > .title {
          font-size: 1.2em;
    
          // 6.5. Contextual media queries in sub selector
          @media screen and (max-width: 640px) {
            letter-spacing: 0.2em;
            text-transform: uppercase;
          }
        }
      }
    ```
## 特殊规范

对用页面级组件样式，应该是有作用域的
对于公用组件或者全局组件库，我们应该更倾向于选用基于 class 的 BEM 策略
```
// bad
<style lang='scss'></style> 

// good
<!-- 使用 scoped 作用域 -->
<style lang='scss' scoped></style> 



<!-- 使用 BEM 约定 -->
// good
<style> 
.c-Button {
    border: none;
    border-radius: 2px;
}

.c-Button--close {
    background-color: red;
}
</style>
```
## 参考
    [史上最全的Vue开发规范](https://juejin.im/post/5b67e49551882508603d1431)
    
    [Vue风格指南](https://cn.vuejs.org/v2/style-guide/index.html#%E8%A7%84%E5%88%99%E5%BD%92%E7%B1%BB)
