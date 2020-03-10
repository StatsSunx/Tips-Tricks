### 一、CSS布局系列

[**1、CSS行等分布局的常用方法**]()

[**2、三栏布局的5种方法**]()



##### 1、行等分布局的常用方法

```css
/*案例通一使用以下html布局*/
<div class="box">
    <ul class="items">
        <li style="background-color: lightblue">1</li>
        <li style="background-color: lightgreen">2</li>
        <li style="background-color: lightsalmon">3</li>
        <li style="background-color: lightyellow">4</li>
        <li style="background-color: pink">5</li>
    </ul>
</div>

/*CSS*/
/* 1、float + padding + background-clip */
.items > li {
    float: left;
    width: calc(100% / 5);
    padding-right: 10px;
    box-sizing: border-box;
    background-clip: content-box;
}

/* 2、float + margin + calc() */
.items > li {
    float: left;
    width: calc((100% / 5) - 10px);
    margin-right: 10px;
}

/* 3、float + margin + 子元素嵌套 */
/* 其实就是宽度分离原则 */

/* 4、inline-block + padding + background-clip*/
.items {
    font-size: 0;
}
.items > li {
    display: inline-block;
    width: calc((100% / 5) - 10px);
    padding-right: 10px;
    /* box-sizing: border-box; */
    background-clip: content-box;
    font-size: 16px;
}

/* 5、inline-block + margin + calc */
.items > li {

    display: inline-block;

    width: calc((100% / 5) - 10px);

    margin-right: 10px;

    font-size: 16px;
}

/* 6、inline-block + margin 宽高分离原则 */

/* 7、table + padding */
.items {
    display: table;
    width: calc(100% + 10px);
    table-layout: fixed;
}
.items > li {
    display: table-cell;
    padding-right: 10px;
    background-clip: content-box;
}

/* 8、flex 弹性布局*/
.items {
    display: flex;
}
.items > li {
    flex: 1;
    margin-right: 10px;
}

/* 9、grid网格布局 */
.items {
    display: grid;
    grid-template-columns:repeat(5,calc((100% / 5) - 10px));
    grid-gap: 10px;
}
```

##### 2、三栏布局的5种方法

```css
/*前2种方法使用以下html结构*/
<div class="container">
    <div class="left" style="background-color: lightblue"></div>
    <div class="content" style="background-color: pink"></div>
    <div class="right" style="background-color: lightyellow"></div>
</div>
/*1、三栏布局-绝对定位法*/
.container1 {
    position: relative;
    height: 100px;
    text-align: center;
    line-height: 100px;
}
.left1, .right1 {
    position: absolute;
    width: 200px;
    height: 100%;
    top: 0;
}
.right1 {
    right: 0;
}
.content1 {
    height: 100%;
    margin: 0 210px;
}

/*2、利用flex布局*/
.container2 {
    display: flex;
    height: 100px;
    margin-top: 10px;
    text-align: center;
    line-height: 100px;
}
.left2, .right2 {
    flex: 0 0 200px;
}
.content2 {
    flex: 1;
    margin: 0 10px;
}

/*3、浮动定位布局*/
<div class="container3">
    <div class="left3" style="background-color: lightblue"></div>
    <div class="right3" style="background-color: lightyellow"></div>
    <!-- 中间栏必须放到最后渲染 -->
    <div class="content3" style="background-color: pink">浮动+BFC布局</div>
</div>
/*浮动CSS*/
.container3 {
    height: 100px;
    margin-top: 10px;
    overflow: hidden;
    text-align: center;
    line-height: 100px;
}
.left3 {
    float: left;
    width: 200px;
    height: 100%;
    margin-right: 10px;
}
.right3 {
    float: right;
    width: 200px;
    height: 100%;
    margin-left: 10px;
}
.content3 {
    height: 100%;
    overflow: hidden;
}

/*4、圣杯布局*/
<div class="container4">
    <!-- 中间栏必须放到最前渲染 -->
    <div class="content4" style="background-color: pink">圣杯布局</div>
    <div class="left4" style="background-color: lightblue"></div>
    <div class="right4" style="background-color: lightyellow"></div>
</div>
/* 圣杯CSS */
.container4 {
    height: 100px;
    padding: 0 210px;
    margin-top: 10px;
    text-align: center;
    line-height: 100px;
}
.left4, .right4 {
    float: left;
    width: 200px;
    height: 100%;
    position: relative;
}
.left4 {
    margin-left: -100%;
    left: -210px;
}
.content4 {
    float: left;
    width: 100%;
    height: 100%;
}
.right4 {
    margin-left: -200px;
    right: -210px;
}

/*5、双飞翼布局*/
<div class="container5">
    <div class="content5" >
        <!-- 增加一层结构 -->
        <div class="inner">双飞翼布局</div>
    </div>
    <div class="left5" style="background-color: lightblue"></div>
    <div class="right5" style="background-color: lightyellow"></div>
</div>
/*双飞翼CSS*/
.container5 {
    min-width: 600px;
    height: 100px;
    margin-top: 10px;
    text-align: center;
    line-height: 100px;
}
.left5, .right5 {
    float: left;
    height: 100%;
    width: 200px;
}
.content5 {
    float: left;
    width: 100%;
    height: 100%;
}
.left5 {
    margin-left: -100%;
}
.right5 {
    margin-left: -200px;
}
.content5 .inner {
    margin: 0 210px;
    height: 100%;
    background-color: pink;
}
```

