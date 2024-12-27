> javascript输入输出

* prompt() 显示对话框提示用户输入信息
* alert()、prompt()会跳过页面渲染先被执行

> 变量注意事项

* let 不允许多次定义一个变量
* const 声明的变量称为"常量"，（声明时必须赋值，且不允许重新赋值）

> 模板字符串

使用``来拼接字符串与变脸，变量使用${}进行包裹

> undefined

一般声明变量，但是没有给变量进行赋值，变量的类型就是undefined



> DOM树

* 一个页面就是一个文档，使用document表示
* 每一个标签都是一个元素，使用element表示
* 所有的内容都是节点，使用node表示（标签、属性、文本、注释等）



##### 1.	JS执行机制

> javascript语言特点就是单线程，所以区分同步与异步
>
> 同步：同步任务都在一个主线程上，形成一个执行栈
>
> 异步：JS的异步是通过回调函数实现的，一般而言，异步任务有三种类型
>
> 1、普通事件：click、resize
>
> 2、资源加载：load、error
>
> 3、定时器：setInterval、setTimeout

###### 	1.1	执行机制

​	先执行执行栈中的同步任务

​	异步任务放在任务队列中

​	执行栈中同步任务完成后，从任务队列中获取异步任务并在执行栈中执行，主线程重复获取、执行任务的机制称为事件循环（event loop）

##### 2.	location对象

> location的数据类型是对象，它拆分并保存了URL的信息

###### 2.1	常用属性和方法

> href：获取完整URL地址，对其赋值时用于地址跳转
>
> search：获取地址中携带的参数，一般是？后的部分
>
> hash：获取地址中的哈希值，#符号后的部分
>
> reload：方法用来刷新当前页面，传入参数为true时强制刷新，location.reload(true)

##### 3.	正则表达式

###### 3.1	test()与exec()区别

> test()方法,判断匹配字符是否存在,返回布尔值
>
> exec()方法,检索查找符合规范的字符串,找到返回数组,否则为null

###### 3.2	预定义:常见模式的简写方式

> \d	匹配0-9任意数字,[0-9]
>
> \D	0-9以外的数字
>
> \w	匹配任意字母,数字,下划线 [0-9a-zA-Z_]
>
> \W	字母,数字,下划线以外的字符
>
> \s	匹配空格(换行符,制表符,空格)	[\t\r\n\v\f]
>
> \S	匹配非空格的字符

##### 4.	闭包

###### 4.1	概念

​	一个函数对周围状态的引用捆绑在一起,内层函数中访问到其外层函的作用域

> 简单来说就是,一个内部函数能够访问外部变量,即使外部函数已经执行完毕

###### 4.2	闭包优势

> 1.数据私有性

##### 5.	箭头函数

> 事件回调函数使用箭头函数时,this指的是window,因此DOM事件回调函数为了简便,不推荐使用箭头函数

##### 6.	遍历数组forEach()方法

> forEach()方法用于调用数组的每一个元素,并将元素传给回调函数

```js
goodsList.forEach(item => {
    const {name, price, pricture} = item
    str += `
    	<div class='item'>
    		<img src=${picture} alt="">
    		<p class="name">${name}</p>
    		<p class="price">${price}</p>
    	<div>
    `
})
document.querySelecter('.list').innerHTML = str
```

##### 7.	筛选数组filter()方法

> 筛选符合条件的数组元素,并返回这些元素组成的新数组

```js
if (dataset.index === '1'){
    arr = goodsList.filter(item => itrm.price > 0 && item.price <= 100)
}
```

##### 8.	创建对象的3种方式

> 字面量\new Object\构造函数

```js
 const o = {
                name: ''
            }

 const obj = new Object({
                uname: 'Thranduil'
            })

 function Person(name){
                this.name = name
            }

 const person = new Person("thranduil")

 console.log(o)
 console.log(obj)
 console.log(person)
```

##### 9.	原型

> 每个构造函数都有prototype属性,该属性指向原型对象,那些不变的方法prototype对象上,所有实例对象都能共享这些方法,构造函数和原型对象的this都是指向实例对象的

###### 9.1	constructor属性

> 每个原型对象都有constructor属性,该属性指向原型对象的构造函数

###### 9.2	对象原型

​	对象都有一属性proto属性,指向构造函数的prototype原型对象,对象之所以能够使用原型对象的属性和方法,就是因为proto属性的存在

> 注意:	proto属性是JS非标准属性
>
> [[prototype]]和proto意义相同
>
> proto对象原型里面也有一个constructor属性,指向该实例对象的构造函数

###### 9.3	原型总结

> prototype 是原型对象\构造函数都自动有原型
>
> constructor属性在哪里:	原型对象prototype和对象原型proto属性中都有,均指向构造函数
>
> proto属性在哪里:	在实例对象中,指向原型对象prptotype

###### 9.4	原型继承

> 封装:抽取公共部分
>
> 继承:	其他构造函数继承公共属性和方法

```js
function Person(){
    this.eyes = 2
    this.head = 1
}

function Woman(){}
//	修改构造函数的原型对象
Woman.prototype = new Person()
//	原型对象构造器指向原来构造函数
Woman.prototype.constructor = Woman
//	添加一个方法
Woman.prototype.baby = function () {
    console.log('baby')
}
//	实例化对象
const red = new Woman
console.log(red)
```

> instanceof 方法检测构造函数的prototype是否出现在其原型链上

```js
        // 模拟框的构造函数
        function Modal(title = '', message = ''){
            // 创建modal模拟框盒子
            this.modalBox = document.createElement('div')
            // 给div标签添加类名modal
            this.modalBox.className = 'modal'
            // modal盒子内部填充2个div标签并修改文字内容
            this.modalBox.innerHTML = `
                <div class='header'>${title}<i>x</i></div>
                <div class='body'>${message}</div>
            `
        }
        
        // 给构造函数原型对象挂载open方法
        Modal.prototype.open = function () {
            //  先判断页面是否有modal盒子，有先删除，否则添加
            const box = document.querySelector('.modal')
            box && box.remove()

            //  注意这个方法不要用箭头函数
            //  把刚才创建的modalBox显示到页面body中
            document.body.append(this.modalBox) 

            //  等盒子显示出来就可以绑定点击事件了
            this.modalBox.querySelector('i').addEventListener('click', ()=>{
                //  此处使用箭头函数
                //  this指向实例对象
                this.close()
            })
        }

        // 关闭方法，挂载到拟态框的构造函数原型上
        Modal.prototype.close = function () {
            this.modalBox.remove()
        }

        // 按钮点击
        document.querySelector('#delete').addEventListener('click', () => {
            const m = new Modal('温馨提示', '您没有权限删除')
            // 调用 打开方法
            m.open()
        })
```

##### 10.	深浅拷贝

> 浅拷贝:	拷贝地址,基本数据类型拷贝数值,引用数据类型拷贝地址,数据共享
>
> 深拷贝:	拷贝对象,实现数据完全隔离

##### 11.	异常处理

###### 11.1	throw抛异常

> throw 抛出异常信息,程序会终止运行
>
> throw后面跟的是错误信息
>
> Error对象配合throw使用,能够设置更详细的报错信息

```js
        function counter(x, y) {
            if (!x || !y){
                throw new Error('参数不能为空')
            }
            return x + y
        }
```

###### 11.2	try/catch 捕获错误信息

```js
        function fn() {
            try {
                const p = document.querySelector('.p')
                p.style.color = 'red'
            } catch (err) {
                //  拦截错误，提示浏览器提供的错误信息，但是不中断程序执行
                console.log(err.message)
                throw new Error('you can see,the chooser is wrong')
                //需要加return，中断程序
                return
            } finally {
                alert('this is finally excuter')
            }
            console.log(11)
        }
```

##### 12.	this指向

> 函数内部步存在this,沿用上一级的,向外层一层一层的查找this,直到找到
>
> 不适用:	构造函数, 原型函数, dom事件函数等
>
> 适用:	需要使用上层this的地方

###### 12.1	call改变this的指向

> call apply bind总结：
>
> call和apply会调用函数，并且改变函数内部this的指向
>
> 

#### Ⅱ	vue

##### 1.	vue引用方式

> 离线引用：下载vue的js文件，添加到项目中
>
> CDN引用：<script src="https://cdn.jsdelivr.net/npm/vue@2.5.16/dist/vue.js"></script>

##### 2.	对象类型数据

> 支持ognl语法 （object graph navigation language）对象图导航语言

```js
    <div id="app-2">
        姓名：{{person.name}} <br />
        年龄：{{person.age}} <br />
        性别：{{person.gender}} <br />
        爱好：{{person.hobby}}
    </div>

    <script>
        const vm = new Vue({
            el: '#app-2',
            data: {
                person: {
                    name: 'Thranduil',
                    age: 25,
                    gender: 'M',
                    hobby: 'trip'
                }
            }
        })
    </script>
```

##### 3.	条件v-if

> v-if:	控制切换元素是否显示（底层控制DOM元素，操作DOM）

```js
<div id="app-3">
        姓名：{{person.name}} <br />
        年龄：{{person.age}} <br />
        性别：
        <label v-if="person.gender == 'M'">男</label>
        <label v-if="person.gender == 'F'">女</label> <br />
        爱好：{{person.hobby}}
    </div>

    <script>
        const vm = new Vue({
            el: '#app-3',
            data: {
                person: {
                    name: 'Thranduil',
                    age: 25,
                    gender: 'M',
                    hobby: 'trip'
                }
            }
        })
    </script>
```

##### 4.	循环v-for

> v-for: 访问所有父作用域的property

```js
    <div id="app-4">
        <table border="1" cellspacing="0" width="400">
            <tr>
                <th>序号</th>
                <th>序号</th>
                <th>姓名</th>
                <th>性别</th>
                <th>年龄</th>
            </tr>

            <tr v-for="(stu, index) in stus">
                <td>{{index + 1}}</td>
                <td>{{stu.stuNum}}</td>
                <td>{{stu.stuName}}</td>
                <td>
                    <lable v-if="stu.stuGender == 'M'">男</lable>
                    <lable v-if="stu.stuGender == 'F'">女</lable>
                </td>
                <td>{{stu.stuAge}}</td>
            </tr>
        </table>
    </div>

    <script>
        const vm = new Vue({
            el: '#app-4',
            data: {
                stus: [
                    {
                        stuNum: '10001',
                        stuName: 'Thranduil',
                        stuGender: 'M',
                        stuAge: 25
                    },
                    {
                        stuNum: '10002',
                        stuName: 'Monica',
                        stuGender: 'F',
                        stuAge: 25
                    },
                    {
                        stuNum: '10003',
                        stuName: 'Elessar',
                        stuGender: 'M',
                        stuAge: 25
                    }
                ]
            }
        })
    </script>
```

##### 5.	绑定标签属性 v-bind

> 两种格式：v-bind: 属性名
>
> 或是简写为   ：属性名

```js
    <div id="app-5">
        <input type="text" v-bind:value="message">
    </div>

    <script>
        const vm = new Vue({
            el: '#app-5',
            data: {
                message: 'take a note'
            }
        })
    </script>
```

##### 6.	表单标签的双向绑定 v-model

> 只能使用在表单输入标签上
>
> v-model:value 可以简写为 v-model
>
> 简单理解为v-model与数据实现与视图层和模型层数据的绑定，视图层数据发生变化影响模型层数据，反之亦然

```js
    <div id="app-6">
        <input type="text" v-model="message">
        <hr><br>
        双向绑定：{{message}}
    </div>

    <script>
        const vm = new Vue({
            el: '#app-6',
            data: {
                message: 'proferssion'
            }
        })
    </script>	
```

##### 7.	vue实例

> 每一个使用vue进行数据渲染的网页文档都需要创建一个vue实例--ViewModel

###### 7.1	vue实例的生命周期

> 创建vue实例（初始化data,加载el）
>
> 数据挂载（将vue实例data中数据渲染到网页HTML标签）
>
> 重新渲染（当vue的data数据发生变化时，会渲染HTML
>
> 销毁实例

创建对象-属性初始化-获取属性值-GC回收

###### 7.2	钩子函数

> 为方便开发者在vue实例生命周期的不同阶段进行特定的操作,vue在生命周期的4个阶段前后分别提供了一个函数,这个函数无须开发者调用,当vue实例到达生命周期的指定阶段会自动调用对应的函数

```js
 <div id="app-7">
        <label v-once>{{message}}</label><br>
        <label>{{message}}</label><br>
        <input type="text" v-model="message">
     </div>

     <script>
        const vm = new Vue({
            el: '#app-7',
            data: {
                message: 'thranduil'
            },

            beforeCreate: function () {
                //  1.data 初始化之前执行，不能操作data
            },

            create: function () {
                //  2.data初始化之后执行，模板加载之前，可以修改/获取data的值
                console.log(this.message)
                //  this.message = thranduil create()
            },

            beforeMount: function () {
                //  3.模板加载以后，数据初始渲染之前，可以修改 / 获取data的值
                // this.message = 'thranduil beforeMount'
            },

            mounted: function () {
                //  4.数据初始渲染之前，可以对data中变量进行修改，但是不会影响v-once的渲染
                //  this.meaasge = 'thranduil mounted'
            },

            beforeUpdate: function () {
                //  5.数据渲染之后，当data中数据发生变化时触发重新渲染，渲染之前执行该函数
                console.log('---' + this.message);
                this.message = 'thranduil beforeUpdate'
            },

            update: function () {
                //  6.data数据修改之后，重新渲染到页面之后
                //  this.message = 'thranduil update'
            },

            beforeDestroy: function () {
                //  7.实例销毁之前调用
            },

            destroy: function () {
                //  8.实例销毁以后调用
            }
        })
     </script>
```

##### 8.	计算属性和侦听器

> data中属性可以通过声明获取,也可以通过computed计算属性的getter获取
>
> 特性:	计算属性所依赖的属性值发生变化会影响计算属性的值

```js
     <div id="app-8">
        <input type="text" v-model="message1"><br>
        <input type="text" v-model="message2"><br>
        {{message3}}
     </div>

     <script>
        const vm = new Vue({
            el: '#app-8',
            data: {
                message1: 'thranduil',
                message2: 'leglas'
            },
            computed: {
                message3: function () {
                    return this.message1 + this.message2;
                }
            }
        })
     </script>
```

> 当数据变化时执行异步操作,或者开销较大时,使用侦听器wctch

```js
     <div id="app-9">
        <input type="text" v-model="message1"><br>
        <input type="text" v-model="message2"><br>
        {{message3}}
     </div>

     <script>
        const vm = new Vue({
            el: '#app-9',
            data: {
                message1: 'thranduil',
                message2: 'leglas',
                message3: 'thranduil leglas'
            },
            watch: {
                message1: function (){
                    this.message3 = this.message1 + this.message2;
                },
                message2: function (){
                    this.message3 = this.message1 + this.message2;
                }
            }
        })
     </script>
```

##### 9.	class绑定

```js
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
    <style>
        .my-style1 {
            width: 200px;
            height: 100px;
            background-color: orange;
        }
        .my-style2 {
            border-radius: 10px
        }
        .my-style3 {
            width: 200px;
            height: 100px;
            background-color: black;
        }
    </style>
    <script src="https://cdn.jsdelivr.net/npm/vue@2.5.16/dist/vue.js"></script>
</head>
<body>
    <div id="app-10">
         <!-- message1 为true加载my-style1, message2 为true加载my-style2 -->
        <div :class="{'my-style1': message1, 'my-style2': message2}"></div>
        <hr>
        <!-- 为class 属性加载多个样式名 -->
        <div :class="[booleanValue1, booleanValue2]"></div>
        <hr>
        <!-- 如果message3 为true ，则class='my-style3',否则class='my-style1'
         如果在三元运算中使用样式名需要加单引号，不加单引号则表示从data 变量中获取样式名 -->
        <div :class="[message3 ? 'my-style3' : 'my-style1']"></div>
        <div :class="[message1 ? booleanValue1 : booleanValue2]"></div>
    </div>

    <script>
        const vm = new Vue({
            el: '#app-10',
            data: {
                message1: true,
                message2: true,
                message3: true,
                booleanValue1: "my-style1",
                booleanValue2: "my-style2",
                booleanValue3: "my-style3",
            }
        })
    </script>
</body>
```

##### 10.	style绑定

> 使用v-bind绑定内联样式时:
>
> 使用{}定义样式,才能获取data的值,{}要遵循JSON格式
>
> {} 中不在使用style的属性名,而是转换为JSON格式的属性名

```js
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
    <script src="https://cdn.jsdelivr.net/npm/vue@2.5.16/dist/vue.js"></script>
</head>
<body>
    <div id="app-11">
        <div v-bind:style="{color: colorName, fontSize: fontsize + px}">
            thranduil
        </div>
        <!-- 直接绑定data中定义好的样式字符串 -->
        <div v-bind:style="myStyle1">thranduil</div>
        <!-- 直接绑定data中定义好的样式对象 -->
        <div v-bind:style="myStyle2">thranduil</div>
        <!-- 可以通过数组形式引用多个样式对象 -->
        <div v-bind:style="[myStyle2, myStyle3]">thranduil</div>
    </div>

    <script>
        const vm = new Vue({
            el: '#app-11',
            data: {
                colorName: 'yellow',
                fontsize: '40',
                myStyle1: "color: orange; font-size: 50px",
                myStyle2: {
                    color: 'blue',
                    fontSize: '60px'                
                },
                myStyle3: {
                    textShadow: 'orange 3px 3px 5px'
                }
            }
        })
    </script>
</body>
```

##### 11.	条件与列表渲染

###### 11.1	条件渲染

> v-if 	v-else-if 	v-else

```js
    <div id="app-12">
        <h3 v-if="code == 1">thranduil can see</h3>
        <h3 v-if="flag">leglas can see</h3>
		<h3 v-else>hello can see</h3>
    </div>

    <script>
        const vm = new Vue({
            el: '#app-12',
            data: {
                code: 1,
                flag: false
            }
        })
    </script>
```

> v-else指令表示v-if的else块
>
> v-else-if
>
> v-if与v-show效果相同只是渲染过程不一样

```js
    <div id="app-13">
        分数： {{code}}
        等级： 
        <h3 v-if="code >= 90">优秀</h3>
        <h3 v-else-if="code >= 80">良好</h3>
        <h3 v-else-if="code >= 90">中等</h3>
        <h3 v-else-if="code >= 90">及格</h3>
        <h3 v-else>挂科</h3>
    </div>
    <script>
        const vm = new Vue({
            el: '#app-13',
            data: {
                code: 85
            }
        })
    </script>
```

##### 12.	事件处理

> v-on:click 点击事件可以简写为@click
>
> 使用js函数传值
>
> 使用dataset对象传值

```html
	<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
    <script src="https://cdn.staticfile.org/jquery/1.10.2/jquery.min.js"></script>
    <!-- 最新版本的 Bootstrap 核心 CSS 文件 -->
    <link rel="stylesheet" href="https://stackpath.bootstrapcdn.com/bootstrap/3.4.1/css/bootstrap.min.css" integrity="sha384-HSMxcRTRxnN+Bdg0JdbxYKrThecOKuH5zCYotlSAcp1+c8xmyTe9GYg1l9a69psu" crossorigin="anonymous">
    <!-- 最新的 Bootstrap 核心 JavaScript 文件 -->
    <script src="https://stackpath.bootstrapcdn.com/bootstrap/3.4.1/js/bootstrap.min.js" integrity="sha384-aJ21OjlMXNL5UyIl/XNwTMqvzeRMZH2w8c5cRVpzpU8Y5bApTppSuUkhZXN0VxHd" crossorigin="anonymous"></script>

    <script src="https://cdn.jsdelivr.net/npm/vue@2.5.16/dist/vue.js"></script>
</head>
<body>
    <div id="app-15">
       <ul>
           <li v-for="c in categories">
               <a :href="'query?cid=' + c.cid">{{c.cname}}</a>
           </li>
       </ul>

        <table class="table table-bordered">
            <tr>
                <th>学号</th>
                <th>照片</th>
                <th>姓名</th>
                <th>性别</th>
                <th>年龄</th>
                <th>操作</th>
            </tr>
            <template v-for="(s, index) in stu">
                <tr :id="'tr' + s.stuNum">
                    <td>{{s.stuNum}}</td>
                    <td>
                        <img height="30" :src="s.stuImg" />
                    </td>
                    <td>{{s.stuName}}</td>
                    <td>
                        <!-- {{s.stuGender == 'M' ? '男' : '女'}} -->
                        <img v-if="s.stuGender == 'M'" src="img/m.bmp">
                        <img v-else src="img/f.bmp">
                    </td>
                    <td>{{s.stuAge}}</td>
                    <td>
                        <button class="btn btn-danger" v-on:click="doDelete(s.stuNum,s.stuName)">删除</button>
                        <button class="btn btn-success" @click="doUpdate" :data-snum="s.stuNum"
                                :data-sname="s.stuName" :data-simg="s.stuImg">修改</button>
                    </td>
                </tr>
            </template>

        </table>
    </div>

    <script type="text/javascript">
        var vm = new Vue({
            el: '#app-15',
            data: {
                categories:[
                    {
                        cid: 1,
                        cname: "华为"
                    },
                    {
                        cid: 2,
                        cname: "小米"
                    },
                    {
                        cid: 3,
                        cname: "OPPO"
                    },
                    {
                        cid: 4,
                        cname: "VIVO"
                    }
                ],
                stu: [
                    {
                        stuNum: "10010",
                        stuImg: "img/1.jpg",
                        stuName: "Tom",
                        stuGender: "M",
                        stuAge: 20
                    },
                    {
                        stuNum: "10011",
                        stuImg: "img/2.jpg",
                        stuName: "Joker",
                        stuGender: "M",
                        stuAge: 21
                    },
                    {
                        stuNum: "10012",
                        stuImg: "img/3.jpg",
                        stuName: "Ling",
                        stuGender: "F",
                        stuAge: 20
                    },
                    {
                        stuNum: "10013",
                        stuImg: "img/1.jpg",
                        stuName: "Jack",
                        stuGender: "F",
                        stuAge: 18
                    },
                ]
            },
            methods: {
                doDelete: function (sNum, sName) {
                    alert("---delete:" + sNum + " " + sName)
                },
                doUpdate: function (event) {
                    // 如果 v-on 绑定的 js 函数没有参数，调用的时候可以省略 (), 同时可以给 js 函数一个 event 参数（事件对象）
                    // 1. event 表示触发当前函数的事件
                    // 2. event.srcElement 表示发生事件的元素 --- 修改按钮
                    // 3. event.srcElement.dataset 表示按钮上绑定的数据集 （data-开头的属性）
                    alert("---update:");
                    let stu = event.srcElement.dataset;
                }
            }
        })
    </script>
</body>
```

##### 13.	表单输入绑定

> 表单输入绑定，即双向绑定：就是能够将 vue 实例的 data 数据渲染到表单输入视图 （input\textarea\select）,
>
> 也能够将输入视图的数据同步到 vue 实例的 data中。

```html
<div id="app-18">
    <!-- 文本输入框 密码输入框 -->
    <input type="text" v-model="name" /><br />
    <input type="password" v-model="password" />
    <hr />
    <!-- 单选按钮 -->
    <input type="radio" v-model="radioTest" value="A" /> A
    <input type="radio" v-model="radioTest" value="B" /> B
    <input type="radio" v-model="radioTest" value="C" /> C
    <input type="radio" v-model="radioTest" value="D" /> D
    <hr />

    <!-- 复选框，绑定的是一个数组 -->
    <input type="checkbox" v-model="checkBox" value="篮球" /> 篮球 <br />
    <input type="checkbox" v-model="checkBox" value="足球" /> 足球 <br />
    <input type="checkbox" v-model="checkBox" value="羽毛球" /> 羽毛球 <br />
    <input type="checkbox" v-model="checkBox" value="乒乓球" /> 乒乓球 <br />

    <!-- 下拉菜单 select：绑定一个字符串 -->
    <select v-model="city">
        <option value="BJ">北京</option>
        <option value="SH">上海</option>
        <option value="SZ">深圳</option>
        <option value="GZ">广州</option>
    </select>
    <hr />

    <!-- 下拉菜单 select：加上了 multiple ，表示可多选，需要绑定一个数组 -->
    <select v-model="cities" multiple>
        <option value="BJ">北京</option>
        <option value="SH">上海</option>
        <option value="SZ">深圳</option>
        <option value="GZ">广州</option>
    </select>

    <button type="button" @click="test">测试</button>
</div>

<script type="text/javascript">

    var vm = new Vue({
        el: '#app-18',
        data: {
            name: "admin",
            password: "123456",
            radioTest: "C",
            checkBox: [],
            city: "",
            cities: []
        },
        methods: {
            test: function () {
                alert(vm.cities)
            }
        }

    })
</script>
```

##### 14.	组件

> 将通用的HTML模块进行封装--可复用的vue实例

###### 14.1	组件注册

> 将通用的HTML模板封装注册到Vue中
>
> 自定义组件my-components.js

```js
Vue.component('header-button',{
	template:`<div style="width: 100%; height: 80px; background: salmon">
                <table width="100%">
                    <tr>
                        <td width="200" align="right" valign="middle">
                            <img src="img/1.jpg" height="80" />
                        </td>
                        <td>
                            <label style="color: deepskyblue; font-size: 32px; font-family: 'Adobe 楷体 Std R'; margin-left: 30px">
                                登录
                            </label>
                        </td>
                    </tr>
                </table>
            </div>`
});
```

###### 14.2	组件引用

> 定义组件需要依赖vue.js,在引用自定义组件js文件要先引用vue.js
>
> 组件的引用必须在vue实例el指定的容器中,即要在Vue实例范围之内

```html
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
    <!-- 先引用vue.js -->
    <script src="js/vue.js"></script>
</head>
<body>
    <div id="app-16">
        <header-button></header-button>
        <hr />
        <header-button></header-button>
    </div>
    <!-- 在Vue实例范围内引用组件 -->
    <script src="js/my-component.js"></script>
    <script>
        const vm = new Vue({
            el: '#app-16',
            data: {
                
            }
        })
    </script>
</body>
```

###### 14.3	自定义组件的结构

> Vue.component() 注册组件
>
> data 定义组件模板渲染的数据
>
> template 组件的HTML模板(HTML标签\CSS样式)
>
> methods 定义组件中的标签事件绑定的JS函数

```js
Vue.component('header-button', {
    data: function () {
        // 组件中 data 是通过函数返回的对象
        return {
            name: "貂蝉"
        };
    },
    template: `<div style="width: 100%; height: 80px; background: salmon">
                <table width="100%">
                    <tr>
                        <td width="200" align="right" valign="middle">
                            <img src="img/1.jpg" height="80" />
                        </td>
                        <td>
                            <label style="color: deepskyblue; font-size: 32px; font-family: 'Adobe 楷体 Std R'; margin-left: 30px">
                                登录人： {{name}}
                            </label>
                        </td>
                        <td>
                            <button @click="test">组件按钮</button>
                        </td>
                    </tr>
                </table>
            </div>`,
    methods: {
        test: function () {
            alert("组件中 header-button 定义的函数事件")
        }
    }
});
```

###### 14.4	组件封装/复用

> 将模板中的css样式提取出来,单独封装到css文件存储在css目录
>
> 图片存储在img目录
>
> 将定义的组件js文件和vue文件存放在js目录中

###### 14.5	组件通信

> vue实例本身就是一个组件
>
> 在vue实例指定的el容器中引用的组件称为子组件,当前vue实例就是父组件
>
> 父组件通过属性将数据传递给子组件

###### 14.6	父子组件通信

> 父组件通信子组件:
>
> - `props`: 子组件通过props获取定义父组件传递的自定义属性
>
> - `this.$refs`： 引用子组件
>
> - `this.$children`： 父组件childrens属性，存储着所有的子组件.
>
> 子组件通信父组件（或根组件）
>
> - `this.$emit`： 子组件通过`$emit`访问父组件传递的自定义事件
> - `this.$parent`： 访问父组件
> - `this.$root`: 访问根组件。根组件root就是`new Vue({el: "#app"}); `中的el元素