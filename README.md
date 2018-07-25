# my-project

> A Vue.js project

## Build Setup

``` bash
# install dependencies
npm install

# serve with hot reload at localhost:8080
npm run dev

# build for production with minification
npm run build

# build for production and view the bundle analyzer report
npm run build --report
```

For a detailed explanation on how things work, check out the [guide](http://vuejs-templates.github.io/webpack/) and [docs for vue-loader](http://vuejs.github.io/vue-loader).


npm install vue -g;
npm install vue-cli -g;
npm instam cnpm -g;(一般建议这样安装 ，因为我会出现不必要的错误)
npm install <> --registry=https://registry.npm.taobao.org
他妈的网络弱爆了
npm install webpack --save-dev

<!-- 查看版本 -->
vue -V
cnpm -v
npm -v
webpack --version


<!-- 构建vue项目 -->
vue init webpack <my-project>
<!-- 这一步贼鸡巴慢啊 -->
cd <my-project>
npm install 
npm run dev 
<!-- 或者 -->
npm start

<!-- 用到Axios -->
npm install axios


解耦前端视图与数据
可以复用的组件
前端路由
状态管理
虚拟DOM


#项目目录
+ index.html 项目的根视图
+ build 这个是我们最终发布的时候会用到代码发布在这里，在开发阶段，我们基本不用管
+ config 配置目录，默认配置没有问题，所以我们也不用管
+ node_modules 这个目录是我们放置依赖文件的目录，我们也不用管
+ src 我们的开发目录 基本大多数工作就在这里开展
+ static 资源目录，我们可以放置一些图片，字体图标，一些依赖库jquery bootstrap
+ test 初始测试目录
+ .xxx文件 这是一些配置文件包括语法配置，git配置等。基本不用管，放着就是了
+ package.json 项目配置文件


#模板讲解
  + 注意 {{}} 必须为单行语句
  + 注意 template中只有一个根父级标签

#在组件中
  + 在<style scoped></style> 要加上scoped 表示在组件作用域中
  + 在<script> 
  	// export default 表示默认导出 可被外面访问
  	export default {
	  	// 数据要定义在
	  	// 注意的是 这里的不是一个对象
	  	// 而是一个函数方法
	  	// 不然是渲染不了的
	  	data(){
	  		// 里面
	  		// 函数里有一个返回值，是一个对象
	  		return {

	  		}
	  	}
  }</script>


#注意App.vue
  + 是整个组件的根组件
  + 其他在组件库（components）里的的所有分组件都引入到根组件
  + 最后统一在index.html根视图渲染 

  + index.js引入了HelloWorld组件

#事件绑定
  + 用v-on:事件名 = 
  + 用v-bind:事件名 = 
  + 事件必须写在 methods : {}对象中
  + methods:{
	  click(){},
	  <!-- 在事件中我们可以传入事件对象 event -->
	}

#属性绑定
  + v-html: 是指绑定到标签的内容上 就如document.getElementById('app').innerHTML = '';
  + v-text: 是指把标签显示为text文本显示

#数组更新视图
  + 变异方法 ： 引起视图更新 使原先数组发生

    * push()
	* pop()
	* shift()
	* unshift()
	* splice()
    * sort()
	* reverse()
  + 替换方法 ： 不会引起视图的更新 数组的本身没有变化 返回一个新数组

    * filter(),
    * concat()
    * slice()

#生命周期
  + created 实例创建完成后调用。此阶段完成了数据的观察，但是尚未挂载，$el还不能用
  + mounted el 挂载到实例上后调用
  + beforeDestroy 实例销毁之前调用

#插值与表达式

#指令与事件
  + v-if 当参数为false时，DOM不加载，
  + v-show 当参数false时，DOM加载但不显示 （通过样式设置不显示）
  + v-bind:href=''
  + v-bind:src=''
  + v-bind:id=''
  + v-bind:class=''
  + v-on:click=''
  + @click=''(个人比较喜欢这种方式)


+ v-html: 如果将用户产生的内容使用v-html输出后，有可能导致XSS攻击，所以要在 服务器端对用户提交的内容进行处理，一般可用尖括号<>转义

+ 如果想要显示{{}}模板而不进行替换，使用v-pre即可跳过这个元素和他的子元素的编译过程

{{
	<!-- 模板 -->
	计算
	三目运算
	数组操作
	<!-- 必须是单个表达式 -->

	<!-- 下面的离子就是不行de -->
	if(ok) return {}
	var book = 'Ken'
}}

#过滤器
  + 过滤器也可以串联 ，而且可以接受参数{{message | filterA | filterB}}
  + {{message | filterA('arg1','arg2')}}
filters:{
	<!-- 对象中书写过滤函数 -->
}

#特别注意
  + 引入App.vue的组件的名称不要用vue.js中自带一个关键字啊 比如说filter ,Filter(大写的都不行)
  + 如果在data函数对象中定义的数据 不要跟vue指令同名，不然会报错
  + v-bind:title='' v-html='title'这样会报错

#计算属性
  + 为什么要用到计算属性呢
  + 原因是如果要用到这个计算值多次的话
  + 就会重复使用那个属性

#计算属性 vs 方法
  + 我们可以将同一函数定义为一个方法而不是一个计算属性。两种方式的最终结果确实是完全相同的。然而，不同的是计算属性是基于它们的依赖进行缓存的。计算属性只有在它的相关依赖发生改变时才会重新求值。这就意味着只要 message 还没有发生改变，多次访问 reversedMessage 计算属性会立即返回之前的计算结果，而不必再次执行函数。

#数据检测属性
  + watch:{}

#每一个计算属性都包含一个getter和一个setter,我们上面的两个实例都是计算属性的默认
#只是利用了getter来读取。在你需要的时候，也可以提供一个setter函数，当手动修改计算属性
#就像修改一个普通数据那样时，就会出发setter函数，执行一些自定义的操作


# 既然有了方法为什么要用计算属性呢
  + 原因是计算属性是基于他的依赖缓存的，一个属性所依赖的数据变化时，它才会重新取值，所以text只要不变，计算属性也就不更新了

#绑定class的几种方式
  + :class={'active':inActive}
  + v-bind:class
  + :class可以跟普通的class共同存在
  + 数组的方式 :class="[activeCls,errorCls]"应用一个class列表
  + class还可以绑定一个计算属性

#vue.js提供的Key属性
  + 他可以让你决定是否复用元素
  + key的值必须是唯一的
  + 不复用输入框的值

#v-for
  + 可以索引数组
  + 可以索引对象
  + 可以用在内置标签template
  + 有两个可选参数 index key 
  + 还可以迭代整数

#注意的是
  + 通过索引直接设置项目，比如app.books[3] = {}
  + 修改数组的长度，比如app.books.length = 1;

#解决问题
  + 解决第一个问题可以有两种方法
  ```
      Vue.set(app.books,3,{
        name: '《CSS解密》',
        author: '[希] Lea Verou'
      })

  ```

  + 如果是在webpack中使用组件化的方式，默认没有导入vue，可以用$set
  ```
      this.$set(app.books,3,{
        name: '《CSS解密》',
        author: '[希] Lea Verou'    
      })
  ```

  +另一种方法就是
  ```
      app.books.splice(3,1,{
          name: '《CSS解密》',
          author: '[希] Lea Verou'
      })
  ```

  ```
      app.books.splice(1)
  ```

#过滤与排序
  + 当你不想改变原数组，想通过一个数组的副本来做过滤或者排序的显示时，可以使用计算属性
  + 来返回过滤或者排序的数组

#修饰符
  + .stop
  + .prevent
  + .capture
  + .self
  + .once
  + .enter
  + .tab
  + .delete
  + .esc
  + .space
  + .up
  + .down
  + .left
  + .right

  + .ctrl
  + .alt
  + .shift
  + .meta


#购物车的分析
  + 商品名称
  + 商品价格
  + 购买数量
  + 增加按钮
  + 减少按钮
  + 数据显示

#修饰符
  + .lazy 在输入框中，v-model默认是在input事件中同步输入框的数据
    使用修饰符.lazy 会转变为在change事件中同步
  + .number 可以将输入转换为Number类型，否则虽然你输入的是数字

#v-model
  + @input可以用来取代v-model
  + @input='一个方法'
  + 单选按钮单独使用时，不需要v-model 直接使用v-bind绑定一个布尔值，为真时选中
  + 使用组合来实现排斥选择的效果，就需要v-model配合绑定value来使用
  + .trim 可以自动过渡输入的首尾空格

#组件详解
  + 父组件与子组件之间的通信，
    -- 父组件通过props属性传递数据给子组件
    -- 子组件通过emit Events事件传递数据给父组件
    -- :自定义属性
    -- 数据传递的限制
    -- 数据是必须的加上require : true
  + 子组件向父组件之间的通信
    -- 子组件通过emit（发出）事件传递给父组件数据

#组件用法
  + 注册全局
    -- Vue.component('my-component',{
          <!-- 打开是空白的 -->
          template: '<div>这是组件的内容</div>'
          <!-- template的DOM结构必须被一个元素包含，如果直接写成'这是组件的内容' 不带
                <div></div>是无法渲染的
           -->
    -- })
    -- 现在就可以使用
    -- <div id="app">
          <my-component></my-component>
    -- </div>

  + 局部注册
    -- var Child = {
          template:'<div>这是组件的内容</div>',
    -- }

    -- var app = new Vue({
          el:'#app',
          components: {
              'my-component':Child,
          }
    -- })

    -- <div id="app">
          <my-component></my-component>
    -- </div>

    -- Vue组件的模板在某些情况下会受到HTML的限制，比如<table>内规定只允许是
       <td>,<tr>,<th>等这些表格，所以在<table>内直接使用组件是无效。这种情况
       可以使用is属性来挂载组件
       <div id="app">
         <table>
           <tbody is='my-component'></tbody>
         </table>
       </div>

       - Vue.component('my-component',{
            template: '<div>这一步贼鸡巴慢啊</div>'
       - })
       - var app = new Vue({
            el: '#app',
       - })


    -- Javascript对象是引用关系，所以如果return 出的对象引用了外部的一个对象
    -- 那就是对象就是共享的，任何 一方修改都会同步

    -- <div id="app">
          <my-component></my-component>
          <my-component></my-component>
          <my-component></my-component>
    -- </div>


    -- var data = {
          counter:0,
    -- }

    -- Vue.compoent('my-component',{
          template: '<button @click='counter++'>{{counter}}</button>',
          data:function(){
              return data;
          }
    -- })


    -- var app = new Vue({
          el:'#app',
    -- })

    -- 以上三个组件的点击事件同时进行，也就是说当点击按钮时，
    -- 如果改成以下的方式则组件的点击互不干扰
    -- Vue.compoent('my-component',{
          template: '<button @click='counter++'>{{counter}}</button>',
          data:function(){
              return {
                  counter:0
              }
          }
    -- })


#插槽
  + 单个插槽
    -- 
  + 多个插槽（具有名字的插槽name=''）

  + 作用域插槽 （数据由子组件传递给父组件）
    -- 父组件决定数据的显示方式
    -- 在2.5.0之前 只能作用于template 上

  + 动态组件（keep-alive）
    -- currentView:''(注意这里的当前组件必须是写在''里面)
    -- keep-alive 缓存数据，不再重新渲染

    -- 有时候，传递的数据并不是直接写死的，而是来自父级的动态数据，这时可以使用指令
       v-bind来绑定props的值，
       如果属性不用v-bind绑定的数据，（数字，布尔值，数组，对象）实际上仅仅是字符串而已
       <my-component message='[1,2,3]'></my-component>
       <my-component :message='[1,2,3]'></my-component>
    -- 一种是父组件传递过来初始值。子组件将初始值保存起来，在自己的作用域下可以随意的修改和使用
    -- 另一种情况就是prop作为需要被转换的原始值传入。这种情况就用计算属性就好 

#CSS动画
  + 把要执行动画的元素包裹在transition上
    这个transition这个标签上有个name属性
    v-enter:进入动画
    v-enter-active:执行过程中
    v-enter-to:结束动画

#组件通信
  + 父子组件通信
  + 兄弟组件通信
       --2.x推荐使用一个空的Vue实例来作为中央事件总线，也就是一个中介
  + 跨级组件通信
       --2.x推荐使用一个空的Vue实例来作为中央事件总线，也就是一个中介
  + 自定义事件 当子组件需要向父组件传递数据时，就要用到自定义事件。
    子组件通过$emit()来触发事件，父组件用$on()来监听子组件的事件
  + 使用v-model 2.x可以在组件使用v-model 这就相当于@input='handler'
  ===
      <!-- 父组件 -->
      <div id="app">
        <p>总数：{{total}}</p>
        <my-component v-model='total'></my-component>
      </div>
      <script>
        // 子组件
        Vue.component('my-component',{
          template: '<button @click='handleClick'>+1</button>',
          data(){
            return {
              counter:0,
            }
          },
          methods: {
            handleClick(){
              this.counter++;
              this.$emit('input',this.counter);
            }
          }
        });
        var app = new Vue({
          el:'#app',
          data:{
            total:0
          }
        })
      </script>
  ===

  + v-model可以用来创建自定义的表单输入组件，进行双向数据绑定
    -- 接受一个value的属性
    -- 在有新的value时出发input事件
    -- v-model会默认使用value和input事件

#自定义指令
  + directives:{
        focus:{
            inserted : function(e){
              e.focus();
            }
        }
    }
  + 钩子函数
    --bind：只调用一次，指令第一次绑定到元素时调用。在这里可以进行一次性的初始化设置。

    -- inserted：被绑定元素插入父节点时调用 (仅保证父节点存在，但不一定已被插入文档中)

    -- update：所在组件的 VNode 更新时调用，但是可能发生在其子 VNode 更新之前。指令的值可能发生了改变，也可能没有。但是你可以通过比较更新前后的值来忽略不必要的模板更新 (详细的钩子函数参数见下)。

    -- componentUpdated：指令所在组件的 VNode 及其子 VNode 全部更新后调用。

    -- unbind：只调用一次，指令与元素解绑时调用。


#Axios网络请求
  + npm install axios
  + 引入axios
  + get请求
    -- Axios(url).then((response)=>{}).catch((error)=>{})
    -- Axios(url,{param}).then((response)=>{}).catch((error)=>{})
    -- // Want to use async/await? Add the `async` keyword to your outer function/method.
      async function getUser() {
        try {
          const response = await axios.get('/user?ID=12345');
          console.log(response);
        } catch (error) {
          console.error(error);
        }
      }

  + post请求
  数据格式
    form-data:?name=''&age=20
    x-www-form-urlencode:"{"name":"Ken","age":"20"}"
    -- 注意axios接受的参数是from-data格式
    this.$axios.post('http://www.wwtliu.com/sxtstu/blueberrypai/login.php',qs.stringify({
        user_id:'iwen@qq.com',
        password:'iwen123',
        verification_code:'crvfw'
      })).then((response)=>{
        console.log(response);
      }).catch((error)=>{
        console.log(error);
      })

    qs第三方插件是用来解析x-www-form-urlencode转换为form-data格式

   全局默认配置
    axios.defaults.baseURL = 'https://api.example.com';
    axios.defaults.headers.common['Authorization'] = AUTH_TOKEN;
    axios.defaults.headers.post['Content-Type'] = 'application/x-www-form-urlencoded';
   拦截器
     // Add a request interceptor
    axios.interceptors.request.use(function (config) {
        // Do something before request is sent
        return config;
      }, function (error) {
        // Do something with request error
        return Promise.reject(error);
      });

    // Add a response interceptor
    axios.interceptors.response.use(function (response) {
        // Do something with response data
        return response;
      }, function (error) {
        // Do something with response error
        return Promise.reject(error);
      });


#安装npm install express --save-dev
     npm install mysql --save-dev
#更新npm
    npm install -g npm
    npm cache verify
    npm cache clean
    npm cache clean --force

#解决跨域问题 
  + 打开config/index.js,在proxyTable中添写如下代码：
    -- proxyTable: { 
          '/api': {  //使用"/api"来代替"http://f.apiplus.c" 
            target: 'http://f.apiplus.cn', //源地址 
            changeOrigin: true, //改变源 
            pathRewrite: { 
              '^/api': 'http://f.apiplus.cn' //路径重写 
              } 
          } 
        }

#post数据请求方式
  + 协议规定 POST 提交的数据必须放在消息主体（entity-body）中，但协议并没有规定数据必须使用什么编码方式。实际上，开发者完全可以自己决定消息主体的格式，只要最后发送的 HTTP 请求满足上面的格式就可以。

但是，数据发送出去，还要服务端解析成功才有意义。一般服务端语言如 php、python 等，以及它们的 framework，都内置了自动解析常见数据格式的功能。服务端通常是根据请求头（headers）中的 Content-Type 字段来获知请求中的消息主体是用何种方式编码，再对主体进行解析。所以说到 POST 提交数据方案，包含了 Content-Type 和消息主体编码方式两部分

HTTP/1.1 协议规定的 HTTP 请求方法有 OPTIONS、GET、HEAD、POST、PUT、DELETE、TRACE、CONNECT 这几种。其中 POST 一般用来向服务端提交数据，本文主要讨论 POST 提交数据的几种方式。

我们知道，HTTP 协议是以 ASCII 码传输，建立在 TCP/IP 协议之上的应用层规范。规范把 HTTP 请求分为三个部分：状态行、请求头、消息主体。类似于下面这样：


<method> <request-URL> <version>
<headers>
协议规定 POST 提交的数据必须放在消息主体（entity-body）中，但协议并没有规定数据必须使用什么编码方式。实际上，开发者完全可以自己决定消息主体的格式，只要最后发送的 HTTP 请求满足上面的格式就可以。
<entity-body>


1. application/x-www-form-urlencoded
这应该是最常见的 POST 提交数据的方式了。浏览器的原生 表单，如果不设置 enctype 属性，那么最终就会以 application/x-www-form-urlencoded方式提交数据。请求类似于下面这样（无关的请求头在本文中都省略掉了）：

POST http://www.example.com HTTP/1.1
Content-Type: application/x-www-form-urlencoded;charset=utf-8

title=test&sub%5B%5D=1&sub%5B%5D=2&sub%5B%5D=3
很多时候，我们用 Ajax 提交数据时，也是使用这种方式。例如 JQuery 和 QWrap 的 Ajax，Content-Type 默认值都是「application/x-www-form-urlencoded;charset=utf-8」。 

我这里用soupui调用选的xml格式Media Type为 application/xml ,这里是不对的。我改成 application/x-www-form-urlencoded这种格式后，xml报文也改成key=value形式：

requestMessage=<?xml version=...><itxEnvelope>...</itxEnvelope>


2. multipart/form-data
这又是一个常见的 POST 数据提交的方式。我们使用表单上传文件时，必须让 表单的 enctype 等于 multipart/form-data。直接来看一个请求示例：
POST http://www.example.com HTTP/1.1
Content-Type:multipart/form-data; boundary=----WebKitFormBoundaryrGKCBY7qhFd3TrwA

------WebKitFormBoundaryrGKCBY7qhFd3TrwA
Content-Disposition: form-data; name="text"

title
------WebKitFormBoundaryrGKCBY7qhFd3TrwA
Content-Disposition: form-data; name="file"; filename="chrome.png"
Content-Type: image/png

PNG ... content of chrome.png ...
------WebKitFormBoundaryrGKCBY7qhFd3TrwA--


3. application/json
application/json 这个 Content-Type 作为响应头大家肯定不陌生。实际上，现在越来越多的人把它作为请求头，用来告诉服务端消息主体是序列化后的 JSON 字符串。由于 JSON 规范的流行，除了低版本 IE 之外的各大浏览器都原生支持 JSON.stringify，服务端语言也都有处理 JSON 的函数，使用 JSON 不会遇上什么麻烦。 


JSON 格式支持比键值对复杂得多的结构化数据，这一点也很有用。记得我几年前做一个项目时，需要提交的数据层次非常深，我就是把数据 JSON 序列化之后来提交的。不过当时我是把 JSON 字符串作为 val，仍然放在键值对里，以 x-www-form-urlencoded 方式提交。 
Google 的 AngularJS 中的 Ajax 功能，默认就是提交 JSON 字符串。例如下面这段代码：
var data = {'title':'test', 'sub' : [1,2,3]};
$http.post(url, data).success(function(result) {
    ...
});

POST http://www.example.com HTTP/1.1 
Content-Type: application/json;charset=utf-8

{"title":"test","sub":[1,2,3]}
这种方案，可以方便的提交复杂的结构化数据，特别适合 RESTful 的接口。各大抓包工具如 Chrome 自带的开发者工具、Firebug、Fiddler，都会以树形结构展示 JSON 数据，非常友好。但也有些服务端语言还没有支持这种方式，例如 php 就无法通过 $_POST 对象从上面的请求中获得内容。这时候，需要自己动手处理下：在请求头中 Content-Type 为 application/json 时，从 php://input 里获得原始输入流，再 json_decode 成对象。一些 php 框架已经开始这么做了。 



4. text/xml
我的博客之前提到过 XML-RPC（XML Remote Procedure Call）。它是一种使用 HTTP 作为传输协议，XML 作为编码方式的远程调用规范。典型的 XML-RPC 请求是这样的：
POST http://www.example.com HTTP/1.1 
Content-Type: text/xml

<?xml version="1.0"?>
<methodCall>
    <methodName>examples.getStateName</methodName>
    <params>
        <param>
            <value><i4>41</i4></value>
        </param>
    </params>
</methodCall>

XML-RPC 协议简单、功能够用，各种语言的实现都有。它的使用也很广泛，如 WordPress 的 XML-RPC Api，搜索引擎的 ping 服务等等。JavaScript 中，也有现成的库支持以这种方式进行数据交互，能很好的支持已有的 XML-RPC 服务。不过，我个人觉得 XML 结构还是过于臃肿，一般场景用 JSON 会更灵活方便。


#mock数据模拟
   只能模拟get请求
   项目集成服务器、
   数据模拟工具mockjs.com
   npm install mockjs

#总线bus方式实现组件跨级传递数据
  + 推荐使用以空的Vue实例作为中央事件总线bus

#vue-router
  + 安装npm install vue-router
  + 如果在一个模块化工程中使用它，必须要通过 Vue.use() 明确地安装路由功能：
    -- import Vue from 'vue'
       import VueRouter from 'vue-router'
       Vue.use(VueRouter)
  + 构建开发板
    -- git clone https://github.com/vuejs/vue-router.git node_modules/vue-router
       cd node_modules/vue-router
       npm install
       npm run build
  +
    用 Vue.js + Vue Router 创建单页应用，是非常简单的。使用 Vue.js ，我们已经可以通过组合组件来组成应用程序，当你要把 Vue Router 添加进来，我们需要做的是，将组件 (components) 映射到路由 (routes)，然后告诉 Vue Router 在哪里渲染它们

  + router这个文件主要是路由文件
    Vue.use(Router)

    export default new Router({
      routes: [
        {
          path: '/hello',//配置路径
          name: 'HelloWorld',
          component: HelloWorld
        }
      ]
    })

    new Vue({
      el: '#app',
      router,
      
      components: { App },
      template: '<App/>'
    })

  + 视图加载的位置
    在App.vue中使用标签<router-view></router-view>
    这是视图显示的位置
    <!-- 使用 router-link 组件来导航. -->
    <!-- 通过传入 `to` 属性指定链接. -->
    <!-- <router-link> 默认会被渲染成一个 `<a>` 标签 -->
    <router-link to="/foo">Go to Foo</router-link>
    <router-link to="/bar">Go to Bar</router-link>
    <!-- 路由出口 -->
    <!-- 路由匹配到的组件将渲染在这里 -->
    <router-view></router-view>

  + 跳转
    -- <li>
        <router-link to="/">Go To Root</router-link>
      </li>
      <li>
        <router-link to="/hello">Go To HelloWorld</router-link>
      </li>
      <li>
        <router-link to="/helloRouter">Go To HelloRouter</router-link>
      </li>
      <router-link> 比起写死的 <a href="..."> 会好一些，理由如下：

      无论是 HTML5 history 模式还是 hash 模式，它的表现行为一致，所以，当你要切换路由模式，或者在 IE9 降级使用 hash 模式，无须作任何变动。

      在 HTML5 history 模式下，router-link 会守卫点击事件，让浏览器不再重新加载页面。

      当你在 HTML5 history 模式下使用 base 选项之后，所有的 to 属性都不需要写 (基路径) 了。

      <li>
        <!-- <router-link to="/">Go To Root</router-link> -->
          <router-link :to="DataUrl.root">Go To Root</router-link>
        <!-- <a href="#/" title='root'>Go To Root</a> -->
      </li>
      <li>
        <!-- <router-link to="/hello">Go To HelloWorld</router-link> -->
        <router-link :to="DataUrl.hello">Go To HelloWorld</router-link>
        <!-- <a href="#/hello" title="hello">Go To HelloWorld</a> -->
      </li>
      <li>
        <!-- <router-link to="/helloRouter">Go To HelloRouter</router-link> -->
        <router-link :to="DataUrl.helloRouter">Go To HelloRouter</router-link>
        <!-- <a href="#/helloRouter" title="helloRouter">Go To HelloRouter</a> -->
      </li>


      <li>
        <!-- <router-link to="/">Go To Root</router-link> -->
        <!-- <router-link :to="DataUrl.root">Go To Root</router-link> -->
        <router-link :to="{path:'/'}">Go To Root</router-link>
        <!-- <a href="#/" title='root'>Go To Root</a> -->
      </li>
      <li>
        <!-- <router-link to="/hello">Go To HelloWorld</router-link> -->
        <!-- <router-link :to="DataUrl.hello">Go To HelloWorld</router-link> -->
        <router-link :to="{path:'/hello'}">Go To HelloWorld</router-link>

        <!-- <a href="#/hello" title="hello">Go To HelloWorld</a> -->
      </li>
      <li>
        <!-- <router-link to="/helloRouter">Go To HelloRouter</router-link> -->
        <!-- <router-link :to="DataUrl.helloRouter">Go To HelloRouter</router-link> -->
        <router-link :to="{path:'/helloRouter'}">Go To HelloRouter</router-link>
        <!-- <a href="#/helloRouter" title="helloRouter">Go To HelloRouter</a> -->
      </li>

  + 路由的嵌套
    -- 要在嵌套的出口中渲染组件，需要在 VueRouter 的参数中使用 children 配置：
       const router = new VueRouter({
        routes: [
          { path: '/user/:id', component: User,
            children: [
              {
                // 当 /user/:id/profile 匹配成功，
                // UserProfile 会被渲染在 User 的 <router-view> 中
                path: 'profile',
                component: UserProfile
              },
              {
                // 当 /user/:id/posts 匹配成功
                // UserPosts 会被渲染在 User 的 <router-view> 中
                path: 'posts',
                component: UserPosts
              }
            ]
          }
        ]
      })

  -- 默认显示
     -- 重定向
            重定向也是通过 routes 配置来完成，下面例子是从 /a 重定向到 /b
            const router = new VueRouter({
              routes: [
                { path: '/a', redirect: '/b' }
              ]
            })
            重定向的目标也可以是一个命名的路由：
            const router = new VueRouter({
              routes: [
                { path: '/a', redirect: { name: 'foo' }}
              ]
            })
+ 路由组件传参
  取代与 $route 的耦合
    const User = {
      template: '<div>User {{ $route.params.id }}</div>'
    }
    const router = new VueRouter({
      routes: [
        { path: '/user/:id', component: User }
      ]
    })
  通过 props 解耦
    const User = {
      props: ['id'],
      template: '<div>User {{ id }}</div>'
    }
    const router = new VueRouter({
      routes: [
        { path: '/user/:id', component: User, props: true },

        // 对于包含命名视图的路由，你必须分别为每个命名视图添加 `props` 选项：
        {
          path: '/user/:id',
          components: { default: User, sidebar: Sidebar },
          props: { default: true, sidebar: false }
        }
      ]
    })


    <li>
      <!-- <router-link to="/master">专家</router-link> -->
      <!-- <router-link :to="{name: 'master', params: {count: 100}}">专家</router-link> -->
      <!-- 带参数查询 -->
      <!-- <router-link :to="{name: 'master', query: {count: 100}}">专家</router-link> -->
      <router-link :to="{name: 'master', params: {count: 100, type: obj}}">专家</router-link>
      <!-- <router-link to="/master/120/{name:'Ken'}">专家</router-link> -->
    </li>

  + 路由高亮效果
    -- exact
    类型: boolean

    默认值: false

    "是否激活" 默认类名的依据是 inclusive match (全包含匹配)。 举个例子，如果当前的路径是 /a 开头的，那么 <router-link to="/a"> 也会被设置 CSS 类名。

    按照这个规则，每个路由都会激活<router-link to="/">！想要链接使用 "exact 匹配模式"，则使用 exact 属性：

    <!-- 这个链接只会在地址为 / 的时候被激活 -->
    <router-link to="/" exact>


    -- active-class
        类型: string

        默认值: "router-link-active"

        设置 链接激活时使用的 CSS 类名。默认值可以通过路由的构造选项 linkActiveClass 来全局配置
        export default new Router({
            linkActiveClass: 'active',
            routes: [

              // {
              //  path: '/',
              //  name: 'Root',
              //  component: Root,
              // },
             //  {
             //    path: '/hello',//配置路径
             //    name: 'HelloWorld',
             //    component: HelloWorld
             //  },
             //  {
             //   path: '/helloRouter',
             //   name: 'HelloRouter',
             //   component: HelloRouter
             //  }
              {
                path: '/',
                name: 'index',
                component: Index
              },
              {
                path: '/course',
                name: 'course',
                component: Course,
                // 指定默认路由
                redirect: '/course/web',
                children:[
                  {
                    path: 'web',
                    component: Web,
                  },
                  {
                    path: 'java',
                    component: Java,
                  },
                  {
                    path: 'andriod',
                    component: Andriod
                  }
                ]
              },
              {
                // 传递参数
                path: '/master/:count/:type',
                name: 'master',
                component: Master
              }
            ]
          })

  + mode
    类型: string

    默认值: "hash" (浏览器环境) | "abstract" (Node.js 环境)

    可选值: "hash" | "history" | "abstract"

    配置路由模式:

    hash: 使用 URL hash 值来作路由。支持所有浏览器，包括不支持 HTML5 History Api 的浏览器。

    history: 依赖 HTML5 History API 和服务器配置。查看 HTML5 History 模式。

    abstract: 支持所有 JavaScript 运行环境，如 Node.js 服务器端。如果发现没有浏览器的 API，路由会自动强制进入这个模式。


  + exact-active-class
      类型: string

      默认值: "router-link-exact-active"

      配置当链接被精确匹配的时候应该激活的 class。注意默认值也是可以通过路由构造函数选项 linkExactActiveClass 进行全局配置的

#element-ui
   安装 npm i element-ui -S
   按需引入
      借助 babel-plugin-component，我们可以只引入需要的组件，以达到减小项目体积的目的。

      首先，安装 babel-plugin-component：

      npm install babel-plugin-component -D
      然后，将 .babelrc 修改为：

      {
        "presets": [["es2015", { "modules": false }]],
        "plugins": [
          [
            "component",
            {
              "libraryName": "element-ui",
              "styleLibraryName": "theme-chalk"
            }
          ]
        ]
      }

  import Vue from 'vue';
  import { Button, Select } from 'element-ui';
  import App from './App.vue';

  Vue.component(Button.name, Button);
  Vue.component(Select.name, Select);
  /* 或写为
   * Vue.use(Button)
   * Vue.use(Select)
   */
 + 走马灯
 结合使用el-carousel和el-carousel-item标签就得到了一个走马灯。幻灯片的内容是任意的，需要放在el-carousel-item标签中。默认情况下，在鼠标 hover 底部的指示器时就会触发切换。通过设置trigger属性为click，可以达到点击触发的效果。
 <template>
  <div class="block">
    <span class="demonstration">默认 Hover 指示器触发</span>
    <el-carousel height="150px">
      <el-carousel-item v-for="item in 4" :key="item">
        <h3>{{ item }}</h3>
      </el-carousel-item>
    </el-carousel>
  </div>
  <div class="block">
    <span class="demonstration">Click 指示器触发</span>
    <el-carousel trigger="click" height="150px">
      <el-carousel-item v-for="item in 4" :key="item">
        <h3>{{ item }}</h3>
      </el-carousel-item>
    </el-carousel>
  </div>
</template>

<style>
  .el-carousel__item h3 {
    color: #475669;
    font-size: 14px;
    opacity: 0.75;
    line-height: 150px;
    margin: 0;
  }

  .el-carousel__item:nth-child(2n) {
     background-color: #99a9bf;
  }
  
  .el-carousel__item:nth-child(2n+1) {
     background-color: #d3dce6;
  }
</style>

#vue-awesome-swiper
  + npm install vue-awesome-swiper --save
    mount with global
      import Vue from 'vue'
      import VueAwesomeSwiper from 'vue-awesome-swiper'
       
      // require styles
      import 'swiper/dist/css/swiper.css'
       
      Vue.use(VueAwesomeSwiper, /* { default global options } */)
    
    mount with component
      // require styles
      import 'swiper/dist/css/swiper.css'
       
      import { swiper, swiperSlide } from 'vue-awesome-swiper'
       
      export default {
        components: {
          swiper,
          swiperSlide
        }
      }


#npm install vue-lazyload -D
import Vue from 'vue'
import App from './App.vue'
import VueLazyload from 'vue-lazyload'
 
Vue.use(VueLazyload)
 
// or with options
Vue.use(VueLazyload, {
  preLoad: 1.3,
  error: 'dist/error.png',
  loading: 'dist/loading.gif',
  attempt: 1
})
 
new Vue({
  el: 'body',
  components: {
    App
  }
})


vue-lazyload will set this img element's src with imgUrl string

<script>
export default {
  data () {
    return {
      imgObj: {
        src: 'http://xx.com/logo.png',
        error: 'http://xx.com/error.png',
        loading: 'http://xx.com/loading-spin.svg'
      },
      imgUrl: 'http://xx.com/logo.png' // String
    }
  }
}
</script> 
 
<template>
  <div ref="container">
     <img v-lazy="imgUrl"/>
     <div v-lazy:background-image="imgUrl"></div>
 
     <!-- with customer error and loading -->
     <img v-lazy="imgObj"/>
     <div v-lazy:background-image="imgObj"></div>
 
     <!-- Customer scrollable element -->
     <img v-lazy.container ="imgUrl"/>
     <div v-lazy:background-image.container="img"></div>
 
    <!-- srcset -->
    <img v-lazy="'img.400px.jpg'" data-srcset="img.400px.jpg 400w, img.800px.jpg 800w, img.1200px.jpg 1200w">
    <img v-lazy="imgUrl" :data-srcset="imgUrl' + '?size=400 400w, ' + imgUrl + ' ?size=800 800w, ' + imgUrl +'/1200.jpg 1200w'" />
  </div>
</template>
CSS state
There are three states while img loading

loading loaded error

<img src="imgUrl" lazy="loading">
<img src="imgUrl" lazy="loaded">
<img src="imgUrl" lazy="error">
<style>
  img[lazy=loading] {
    /*your style here*/
  }
  img[lazy=error] {
    /*your style here*/
  }
  img[lazy=loaded] {
    /*your style here*/
  }
  /*
  or background-image
  */
  .yourclass[lazy=loading] {
    /*your style here*/
  }
  .yourclass[lazy=error] {
    /*your style here*/
  }
  .yourclass[lazy=loaded] {
    /*your style here*/
  }
</style> 

#rem
  安装 npm install --save-dev less less-loader
  修改配置文件 webpack.base.conf.js添加配置
  {
        test: /\.less$/,
        use:[
          'style-loader',
          'css-loader',
          'less-loader'
        ],
      }

#Vuex
  安装npm install vuex --save-dev
  引入
  import Vuex from 'vuex'
  Vue.use(Vuex)

  构建自己的vuex库
  git clone https://github.com/vuejs/vuex.git node_modules/vuex
  cd node_modules/vuex
  npm install
  npm run build

  每一个 Vuex 应用的核心就是 store（仓库）。“store”基本上就是一个容器，它包含着你的应用中大部分的状态 (state)。Vuex 和单纯的全局对象有以下两点不同：

  Vuex 的状态存储是响应式的。当 Vue 组件从 store 中读取状态的时候，若 store 中的状态发生变化，那么相应的组件也会相应地得到高效更新。

  你不能直接改变 store 中的状态。改变 store 中的状态的唯一途径就是显式地提交 (commit) mutation。这样使得我们可以方便地跟踪每一个状态的变化，从而让我们能够实现一些工具帮助我们更好地了解我们的应用。

  Vuex 是一个专为 Vue.js 应用程序开发的状态管理模式。它采用集中式存储管理应用的所有组件的状态，并以相应的规则保证状态以一种可预测的方式发生变化。Vuex 也集成到 Vue 的官方调试工具 devtools extension，提供了诸如零配置的 time-travel 调试、状态快照导入导出等高级调试功能

  state，驱动应用的数据源；
  view，以声明方式将 state 映射到视图；
  actions，响应在 view 上的用户输入导致的状态变化。

  什么情况下我应该使用 Vuex？
    虽然 Vuex 可以帮助我们管理共享状态，但也附带了更多的概念和框架。这需要对短期和长期效益进行权衡。

    如果您不打算开发大型单页应用，使用 Vuex 可能是繁琐冗余的。确实是如此——如果您的应用够简单，您最好不要使用 Vuex。一个简单的 global event bus 就足够您所需了。但是，如果您需要构建一个中大型单页应用，您很可能会考虑如何更好地在组件外部管理状态，Vuex 将会成为自然而然的选择。引用 Redux 的作者 Dan Abramov 的话说就是：

    Flux 架构就像眼镜：您自会知道什么时候需要它。

    起始这个状态管理器有点像父组件向子组件传递数据的props属性
    你可以理解成vuex就是把这个props


    通过在根实例中注册 store 选项，该 store 实例会注入到根组件下的所有子组件中，且子组件能通过 this.$store 访问到。让我们更新下 Counter 的实现：
      const Counter = {
      template: `<div>{{ count }}</div>`,
      computed: {
        count () {
          return this.$store.state.count
        }
      }
    }

# Getter 其实就是一个依赖，他依赖于state的属性
  如果有多个组件需要用到此属性，我们要么复制这个函数，或者抽取到一个共享函数然后在多处导入它——无论哪种方式都不是很理想。

  Vuex 允许我们在 store 中定义“getter”（可以认为是 store 的计算属性）。就像计算属性一样，getter 的返回值会根据它的依赖被缓存起来，且只有当它的依赖值发生了改变才会被重新计算。
  const store = new Vuex.Store({
  state: {
    todos: [
      { id: 1, text: '...', done: true },
      { id: 2, text: '...', done: false }
    ]
  },
  getters: {
    doneTodos: state => {
      return state.todos.filter(todo => todo.done)
    }
  }
})

# mutations 不允许出现异步操作的
# actions 可以包含任何异步操作 setTimeout(function(){},1000);

#我们会把store这个仓库不直接写在main.js,而是单独写在一个文件里面
一般我们在src新建一个store文件夹

#npm 发布组件
     官网注册账号

#父链
  在子组件中，使用this.$parent可以直接访问该组件的父实例或者组件
  父组件也可以通过this.$children访问他的所有子组件，而且可以递归向上或者
  递归向下无限访问，直接到跟实例或者最内层的组件

  不过一般不会使用这种方式

#子组件索引
  当子组件比较多时，通过this.$children来--遍历出我们需要的一个组件 实例
  是比较困难的，尤其组件动态渲染时，他们的序列是不固定的。Vue提供了
  通过this.$refs来访问
  <template>
    <div class="pa">
      <p>
        父亲
        <button @click='hanldeRef'>通过ref来访问子组件的实例</button>
        <c ref="comA"/>
        {{msg}}
      </p>
    </div>
  </template>

  <script type="text/javascript">
    import c from './c';
    export default{
      name: 'pa',
      data(){
        return {
          msg:'',
        }
      },
      methods: {
        hanldeRef(){
          console.log(this.$refs)
          this.msg = this.$refs.comA.mseg
        }
      },
      components: {
        c,
      }
    }
  </script>
  $refs只在组件渲染完成后才能填充，并且它是非响应式的，
  它仅仅作为一个直接 访问子组件的应急方案 应当避免使用

#<style type="text/css" scoped lang="less">这个地方的lang="less"一定要是双引号
如果是lang='less'无效

#slot插槽
 编译的作用域 比如父组件中有如下模板
 <child-compoent>
    {{message}}
 </child-compoent>
 这里的message就是slot 但是他绑定的是父组件的数据而不是子组件的数据
 父组件的模板的内容在父组件里编译，子组件的内容在子组件的作用域里编译
 这感觉好像有点向局部函数和全局函数一样
 父组件有自己的数据，子组件也有自己的数据
 单slot、
 子组件内部使用特殊的slot标签可以为这个子组件开启一个slot插槽
 在父组件模板里，插入在子组件标签的所有内容将替代子组件的slot标签及他的内容
<div id='app'>
    <child>
      <p>分别的心无法晚会</p>
    </child>
</div>
<script>
    Vue.component('child',{
        template: '\
        <div>\
          <slot>\
            <p>如果父组件没有内容，我将作为默认出现</p>\
          </slot>\
        </div>'
    })
</script>
<template>
  <div class='detail'>
    详情页
    <!-- <div class="detail-left">
      <div class='product-broad'>
        <img :src="getUrl" alt="">
        <ul>
          <router-link active-class="active" tag="li" :key="index" :to="{path:'/detail/'+detail.tag}" v-for="(detail, index) in detailsNav">
            {{detail.title}}
          </router-link>
        </ul>
        详情页
      </div>
    </div>
    <div class="detail-right">
      {{ getUrl}}
      <router-view/>
      
    </div> -->
  </div>
</template>

<script type="text/javascript">
  export default{
    name: 'detail',
    data(){
      return{
        // detailsNav:[
        //  {
        //    title: '开放产品',
        //    tag: 'earth',
        //  },
        //  {
        //    title: '品牌营销',
        //    tag: 'loud',
        //  },
        //  {
        //    title: '使命必达',
        //    tag: 'car',
        //  },
        //  {
        //    title: '勇攀高峰',
        //    tag: 'hill'
        //  }
        // ]
      }
    },
    // imgUrl:{
   //        "/details/earth":require("../../assets/images/1.png"),
   //        "/details/loud":require("../../assets/images/2.png"),
   //        "/details/car":require("../../assets/images/3.png"),
   //        "/details/hill":require("../../assets/images/4.png")
   //    },
    // computed:{
    //     getUrl(){
    //       return this.imgUrl[this.$route.path];
    //       console.log(this.$route.path)
    //     }
    // }  
  }
</script>

<!-- <style type="text/css" scoped lang="less">
.detail{
  width: 1200px;
    margin: 0 auto;
    height:auto;
    overflow: hidden;
    padding-top: 20px;

  .detail-left{
    float: left;
      width: 200px;
      text-align: center;

      .product-broad{
        background: #fff;
        padding: 20px 0;


        ul{
          margin-top: 20px;

          li{
            text-align: left;
            padding: 10px 15px;
            cursor: pointer;
            transition: background,color 0.8s ease-in-out;

            a{
               display: block;
            }
          }

          li.active,li:hover{
          background: #4fc08d;
            color: #fff;
          }
        }
      }
  }

  .detail-right{
    float: left;
      width: 980px;
      margin-left: 20px;
  }

}
.sales-board {
  background: #fff;
}
.sales-board-form {

}
.sales-board-intro h2 {font-size: 20px;
  padding: 20px;
}
.sales-board-intro p {
  background: #f7fcff;
  padding: 10px 20px;
  color: #999;
  line-height: 1.8;
}
.sales-board-form {
  padding: 30px 20px;
  font-size: 14px;
}
.sales-board-line {
  clear: both;
  padding-bottom: 20px;
}
.sales-board-line-left {
    display: inline-block;
    width: 100px;
}
.sales-board-line-right {
    display: inline-block;
    width: 75%;
}
.sales-board-des {
  border-top: 20px solid #f0f2f5;
  padding: 15px 20px;
}
.sales-board-des p {
  line-height: 1.6;
}
.sales-board-des h2 {
  font-size: 20px;
  padding-bottom: 15px;
}
.sales-board-des h3 {
  font-size: 18px;
  font-weight: bold;
  padding: 20px 0 10px 0;
}
.sales-board-des li {
  padding: 5px 0;
}
.sales-board-table {
  width: 100%;
  margin-top: 20px;
}
.sales-board-table th {
  background: #4fc08d;
  color: #fff;
}
.sales-board-table td {
    border: 1px solid #f0f2f5;
    padding: 15px;
}
</style> -->

{
      path:'/detail',
      name: 'detail',
      ccomponent: Detail,
      // redirect:"/detail/earth",
      // children:[
      //     {
      //       name: 'earth',
      //       path: 'earth',
      //       component: Earth,
      //     },
      //     {
      //       name: 'loud',
      //       path: 'loud',
      //       component: Loud,
      //     },
      //     {
      //       name: 'car',
      //       path: 'car',
      //       component: Car,
      //     },
      //     {
      //       name: 'hill',
      //       path: 'hill',
      //       component: Hill
      //     }
      // ]
    }


#最后打包的时候注意把build文件夹下面的index.js
assetsPublicPath: '/',改成assetsPublicPath: './',

