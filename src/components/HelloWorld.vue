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
      <article class="seriousError">
        我是文章外包围
        <section>子组合选择器和同层组合选择器</section>
        <dl>
          <dt>子组合选择器和同层组合选择器</dt>
          <dd>子组合选择器和同层组合选择器</dd>
        </dl>
        <h1 class="seriousError">我是H1标题</h1>
        <p>我是文章</p>
        <a href="">父选择器的标识符&;</a>
      </article>
      <article>子组合选择器和同层组合选择器</article>
      <article>子组合选择器和同层组合选择器</article>
    </div>
    <div class="fancybox seriousError"></div>
    <div class="blue-theme seriousError">
      <aside>
        我是嵌套导入的蓝色主题
      </aside>
    </div>
    <div class="notice seriousError">我是圆角混合器</div>
    <ul class="plain seriousError">
      <li>我是@mixin混合器的css规则1</li>
      <li>我是@mixin混合器的css规则2</li>
      <li>我是@mixin混合器的css规则3</li>
      <a href="" class="disabled">我是继承a标签的</a>
      <a href="">我是继承a标签的</a>
    </ul>
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
//默认变量值,使用sass的!default标签可以实现这个目的。它很像css属性中!important标签的对立面，
//不同的是!default用于变量，含义是：如果这个变量被声明赋值了，那就用它声明的值，否则就用这个默认值
$fancy-width:100px;
@import '../common/index';
.fancybox {
  width:$fancy-width;
}
// 嵌套导入
.blue-theme {
  @import "../common/_blue-theme"
}
// 这种注释类型为静默注释，不会被编译成css
/* 这种注释会出现生成的css文件中*/
/* 当然普通的注释如果出现在了不正确的地方，最终生成的css文件中也会去掉这段注释*/

// 混合器初步使用
@mixin rounded-corners {
  border-radius:5px;
}
.notice{
  background-color:green;
  border:2px solid #00aa00;
  @include rounded-corners;
}
// 混合器中不仅可以包含属性，可以包含CSS规则，包含选择器和选择器中的属性
@mixin no-bullets{
  list-style:none;
  li{
    list-style-image: none;
    list-style-type: none;
    margin-left:0px;
  }
}
ul.plain {
  margin-top:170px;
  color:#444;
  @include no-bullets;
}
// 给混合器传参数
@mixin link-colors($normal,$hover,$visited){
  color:$normal;
  &:hover{color:$hover;}
  &:visited{color:$visited;}
}
// a{
//   @include link-colors(black,red,blue);
// }
// 当你@include混合器时，有时候可能会很难区分每个参数是什么意思，参数之间是一个什么样的顺序。为了解决这个问题，sass允许通过语法$name: value的形式指定每个参数的值。这种形式的传参，参数顺序就不必再在乎了，只需要保证没有漏掉参数即可：
// a{
//   @include link-colors(
//     $hover:green,
//     $normal:red,
//     $visited:blue
//   )
// }
 // 默认参数值;
 @mixin link-colors(
  $normal,
  $hover:$normal,
  $visited:$normal
)
{
  color:$normal;
  &:hover{
    color:$hover;
  }
  &:visited{
    color:$visited;
  }
}
// a{
//   @include link-colors(red);
// }
// 使用选择器继承来精简CSS
.error{
  border:1px solid red;
  background-color: #fdd;
}
.seriousError{
  @extend .error;
  border-width:3px;
}
// .seriousError不仅会继承.error自身的所有样式，任何跟.error有关的组合选择器样式也会被.seriousError以组合选择器的形式继承，如下代码:
.error a {
  // color: red;
  font-weight:500;
}
h1.error{
  font-size:1.2rem;
}
// 大多数情况你可能只想对类使用继承,但是有些场合你可能想做的更多.最常用的一种高级用法是继承html样式
.disabled{
  color:gray;
  @extend a;
}
// 使用继承的最佳实践
</style>
