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

