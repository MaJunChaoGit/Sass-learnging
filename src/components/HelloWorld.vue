<template>
  <div class="container">
    <h1>群组选择器的嵌套</h1>
    <h2>群组选择器的嵌套</h2>
    <h3>群组选择器的嵌套</h3>
    <nav>
      变量声明
      <a href="">内嵌在群组选择器内的嵌 套规则</a>
    </nav>
    <article>子组合选择器和同层组合选择器</article>
    <div class="selected">
      变量引用
    </div>
    <a href="">变量名使用中划线和下划线可以相互兼容</a>
    <div id="content">
      我是最外层,展示嵌套CSS规则
      <aside>
        父选择器标识符还有另外一种用法，你可以在父选择器之前添加选择器
        <a href="">内嵌在群组选择器内的嵌 套规则</a>
      </aside>
      <article>
        我是文章外包围
        <section>子组合选择器和同层组合选择器</section>
        <dl>
          <dt>子组合选择器和同层组合选择器</dt>
          <dd>子组合选择器和同层组合选择器</dd>
        </dl>
        <h1>我是H1标题</h1>
        <p>我是文章</p>
        <a href="">父选择器的标识符&;</a>
      </article>
      <article>子组合选择器和同层组合选择器</article>
      <article>子组合选择器和同层组合选择器</article>
    </div>
    <div class="fancybox"></div>
  </div>
</template>

<script>
export default {
  name: 'HelloWorld',
  data () {
    return {
      msg: 'Welcome to Sass Learning'
    }
  }
}
</script>


<style lang="scss">
// 变量声明
$nav-color: red;
$nav-bgColor: green;
nav{
  $width: 400px;
  width: $width;
  background: $nav-bgColor;
  color:$nav-color;
}
// 变量引用
$highlight-color: #F90;
$highlight-border:1px solid $highlight-color;
.selected{
  border: $highlight-border;
}
// 变量名使用中划线和下划线可以相互兼容
$link-color:green;
a{
  color:$link_color;
}
// 嵌套CSS 规则
#content{
  border:1px solid red;
  width: 500px;
  height: 200px;
  aside{
    background-color: #EEE;
    float:left;
    width: 100px;
    height: 100%;
  }
  article{

    h1{
      color: red;
    }
    p{
      margin-bottom: 1.4em;
    }
  }
}
// 大多数情况下这种简单的嵌套都没问题，但是有些场景下不行，比如你想要在嵌套的选择器 里边立刻应用一个类似于：hover的伪类。为了解决这种以及其他情况，sass提供了一个特殊结 构&。
article a{
  color:blue;
  &:hover{
    color:red;
  }
}
// 父选择器标识符还有另外一种用法，你可以在父选择器之前添加选择器
#content aside{
  color:red;
  body.chrome & {color:blue;}
}
// 群组选择器的嵌套;
.container{
  h1,h2,h3{
    font-size:22px;
  }
}
// 对于内嵌在群组选择器内的嵌 套规则
nav,aside{
  a{
    color:orange;
  }
}
// 子组合选择器和同层组合选择器：>、+和~
article{
  ~ article{ border-top:1px dashed #ccc;}
  > section {background-color: #eee;}
  dl > {
    dt {color:#ccc}
    dd {color:#555}
  }
  nav + & {margin-top:20px}
}
// 嵌套属性
nav{
  border: 2px solid red {
    left: 0px;
    right: 0px;
  }
}
// 默认变量值,使用sass的!default标签可以实现这个目的。它很像css属性中!important标签的对立面，不同的是!default用于变量，含义是：如果这个变量被声明赋值了，那就用它声明的值，否则就用这个默认值
$fancy-width:100px;
@import '../common/index';
.fancybox {
  width:$fancy-width;
}
</style>
