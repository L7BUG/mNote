# JavaScript
---

3. # 数据类型
    1. ## Map 和 Set
        用法和java一样
    2. ##   iterator(迭代器)
        1. for(let i of arr) 遍历值
        2. for(let i in arr) 遍历 下标
4. # 函数及面向对象
    `arguments` : 包含所有的参数 不管是定义的还是未定义
    1. # 函数定义及变量作用域
        1. ## var(全局变量)
        2. ## let(局部变量)
        3. ## const(常量)
    2. # 方法
        1. 函数放在对象里叫方法
        2. apply 指定函数里的 this (并调用)
    3. # 闭包(难点)
    4. # 箭头函数(新特性)
    5. # 创建对象
        1.  ## JSON
            1. `JSON.stringify()`将对象转换成json字符串
            2. `JSON.parse()`将JSON字符串转换成对象
        2. ## Ajax
            1. js网络请求 异步请求
            2. axios请求(可替代Ajax)
    6. # class 继承(新特性)
    7. # 原型链继承(难)
5. # 面向对象编程
    1. 原型继承(`__proto__`)
    2. class继承
        1. 通过 `class` 定义类
        2. `constructor` 构造函数
        3. 和java一样
6. # BOM(重点)
    >  浏览器对象模型
    1.  window
        >  window 代表浏览器窗口
    2.  Navigator
        >  封装了浏览器的信息(基本不用)
    3.  screen(计算机的屏幕)
    4.  location(重要)
        >代表当前页面的URL信息
        1. `assign()` 相当与重定向
        2. `reload()`刷新
    5. ## document(内容)
        > 代表当前页面
    6. ## history
        > 控制浏览器前进后退  
7. # DOM(重点)
    > 文档对象模型
    * ## 更新
        * innerText 改变文本
        * style CSS 属性
        * - 转换 驼峰命名
    * ## 遍历
    * ## 删除
        1. 获取父节点
        2. 用父删掉自己`removeChild()`
        > 注意： 删除的时候会父元素会变化尤其是在循环中
    * ## 添加
        * append
        * 
    * ## 操作表单
8. # jQuery
    1. 选择器
        > `$(selector).action()`
    2. [事件](https://www.runoob.com/jquery/jquery-events.html)
        > 鼠标， 键盘
    3. DOM
        1. css(JSON键值对)
        2. 