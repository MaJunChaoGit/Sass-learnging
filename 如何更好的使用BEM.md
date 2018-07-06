# 如何更好的使用BEM

[BEM](https://en.bem.info/)是由Yandex团队提出的一种CSS Class 命名方法，旨在更好的创建CSS/Sass模块。他需要遵循一些特殊规定，有些人认为这些规定很冗余，但是我发现他们对于理解DOM有着很大的帮助。你可以去查看我[之前的文章](https://garrettlevinesite.wordpress.com/2016/01/23/bem-helps-beginners-learn-htmlcss/)去了解为什么BEM如此伟大。或者你可以去查看这几篇中文文章来了解BEM([《BEM的定义》](http://www.w3cplus.com/css/bem-definitions.html)[《为什么我们需要BEM》](http://blog.lxjwlt.com/front-end/2015/10/08/why-bem.html))。今天这篇文章，是我在假设你对BEM和Sass已经有所了解甚至熟悉的基础上完成的。

### BEM又丑又傻?

许多人认为BEM是一种[多余的，丑陋的长命名](https://permanenttourist.ch/2015/06/why-using-bem-for-your-css-is-a-bad-idea/)。我完全能够理解当你在使用一种臃肿的和过度描述的命名方式时会发出这样的抱怨。这种情况下你会发现Sass编译后的CSS会非常的冗余和丑陋，尤其是当你在很长的BEM命名内又嵌套了更长的BEM命名时。这简直是非常糟糕和令人沮丧的一件事。

```scss
.aboutSection {
  background-color: tomato;
}
.aboutSection__wrapp {
  max-width: 108rem;
  padding: 3rem 0;
}
.aboutSection__headingContainer {
  background-color: steelblue;
  .aboutSection__header {
  	font-size: 2.4rem;
  	font-weight: 700;
  }
  .aboutSection__subHeader {
    font-size: 1.8rem;
    color: green;
  }
}
```

可能很多刚开始使用BEM的程序员会写出像上面一样的CSS/Scss代码。虽然手指已经很酸痛了但是还是每次都兢兢业业地输入完整的类名。我完全能够理解这时你会感觉BEM是一种很傻很多余的命名规则。我们在不断的重复自己来为不同的类名设置不同的样式，而且不具有可重复性。

### 在Sass中使用BEM

#### 灵活的`&__`

通过使用一组便利的选择器和运算符，我们可以使得BEM出类拔萃。其中最重要的是新加入Sass中的[`&`选择器](http://thesassway.com/intermediate/referencing-parent-selectors-using-ampersand).在声明内`&`选择器会直接引用他的父选择器。当嵌套使用'&'时，它会直接抓取父选择器的类名。因为我们的类名遵循真正可靠的模式，所以我们可以把它作为我们的优势来打造真正可读的代码。

```scss
.aboutSection {
    &__wrapper {
        max-width 108rem;
        padding: 3rem 0;
    }
    &__headingContainer {
        background-color: steelblue;
    }
    &__header {
        font-size: 2.4rem;
        font-weight: 700;
    }
    &__subHeader {
        font-size: 1.8rem;
        color: green;
    }
}
```

以上这段代码就是一个利用`&`选择器的BEM创建的Sass模块，这个模块看上去像是嵌套但并不会带来嵌套所造成的权重差异等问题。这将有效帮助你避免CSS文件中组件样式的冲突。同时采用Sass的嵌套选择器也使我们的代码更加直观可读。

### 强大的`@extend`

我们可以进一步使用`@extend`来改进我们的BEM。BEM允许我们在类的最后添加一个修饰符，当以纯CSS编写样式时，就需要你给同一个元素两个类的标记，比如：

```html
<nav class="nav">
    <ul class="nav__container">
        <li class="nav__item"></li>
        <li class="nav__item"></li>
        <li class="nav__item"></li>
        <li class="nav__item nav__item--active"></li>
    </ul>
</nav>
```

以上这种情况是令人很沮丧的，为什么我们需要添加一个又长又绕的类来说明这个元素是`active`的？为什么我们不能仅仅增加一个名为`active`的类？通过使用`@extend`指令，我们就可以很好地消除这种冗余。

```
.nav {
  background-color: steelblue;
  &__container {
    display: flex;
    justify-content: space-between;
  }
  &__item {
    color: white;
    &--active {
      @extend .nav__item;
      border-bottom: 1px solid red;
    }
  }
}
```

`@extend`指令能让我们确保所选择的项目也具有`nav_item`类中的所有样式，从而清除HTML中的`nav_item`标记。使用这种方法，我们能够随心所欲地改变活动状态的颜色，而无需重写我们之前创建的样式。在我看来，一个元素应该只有一个类，我们应该活用Sass来达到我们想要的结果。

### 结束语

我希望这篇文章能够使你相信尽管BEM的好处远远超过它的那点瑕疵。也许有人会告诉你相反的结果，也许在一开始你会觉得它很冗余，但是通过BEM，我们CSS文件中所有选择器都保持相似的特异性水平。当我们使用'&'选择器时我们可以在保持有很好的组织性和可读性的同时避免嵌套带来的样式冲突。通过使用`@extend`指令，我们不仅可以消除BEM命名的冗余，而且可以修剪下来你的标记。

>本文根据[@Garrett Levine](https://medium.com/@GarrettLevine)的[《Getting Sass-y with BEM》](https://medium.com/@GarrettLevine/getting-sass-y-with-bem-ccaf93c3ad55#.96qo9brxw)所译，整个译文带有我们自己的理解与思想，如果译得不好或有不对之处还请同行朋友指点。如需转载此译文，需注明英文出处:<https://medium.com/@GarrettLevine/getting-sass-y-with-bem-ccaf93c3ad55#.96qo9brxw>。

出处：<http://www.w3cplus.com/preprocessor/getting-sass-y-with-bem.html>