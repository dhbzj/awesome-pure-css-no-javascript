# Flexbox 样式

让我们来看看如何使用 CSS3 的弹性布局写出 10 种常见的 UI 组件。

翻译自 [Flexbox Patterns](http://www.flexboxpatterns.com/)

### 目录

* [步进计数器](#stepper-input)
* [标签页](#tabs)
* [站点头部](#site-header)
* [表单底部](#form-footer)
* [侧边栏](#sidebar)
* [居中提示](#centered-propmt)
* [居中图标](#centered-icon)
* [功能列表](#feature-list)
* [卡片](#card)
* [卡片组](#card-group)

### 从 "display: flex" 属性开始

Flexbox CSS 的基础属性就是 `display: flex`，只需要给一个元素添加这个属性，你就用上了弹性布局了。就这么简单！

你也许会问，这个属性起了什么作用？默认情况下，它指定了元素中的项目沿主轴（main axis）排列，主轴默认是水平方向的。

接下来，我们会用两个实例来介绍这个属性是如何用在我们的 UI 组件的。


<a name="stepper-input"></a>
### 步进计数器 [Demo](http://www.flexboxpatterns.com/stepper-input)

![image](http://www.flexboxpatterns.com/images/thumbs/stepperInput.png)

我们要介绍的第一个例子是步进输入框组件。当绑定 JavaScript 代码之后，点击 + / - 号，输入框中的值将会对应变化。

_译注：此处计数器的实现也可以使用 [CSS Counters](http://caniuse.com/#search=CSS%20Counters) 来代替 JavaScript，具体例子可以参考 [使用 CSS 的 counter-increment 做的游戏](http://www.w3cplus.com/css3/pure-css-games-with-counter-increment.html)。_

按照以往的正常思路，你可能会选择用 `display: inline-block` 或者 `float: left` 来实现这种内联样式。然而，这样做的话，你还需要给这些元素添加特定的选择器。来使用弹性盒子吧，只需要往容器添加 `display: flex` 属性，就可以实现相同的效果了。

当你添加这个属性时，相当于对元素说：“嘿伙计，你就负责按照 flexbox 的规则排列你的子元素就好了！”。在最基本的形式下，元素沿主轴（main axis）排列，默认就是 x 轴，从左到右。

CSS 代码
```CSS
.stepperInput {
  /**
   * Setting display to flex makes this container lay
   * out its children using flexbox. By default, it 
   * orders items horizontally, top-aligned.
   * This has a similar effect to setting the children
   * to have display: inline-block.
   */
  display: flex;
}

.stepperInput__input {
  border-left: 0;
  border-right: 0;
  width: 60px;
  text-align: center;
}

.button {
  cursor: pointer;
  padding: 5px 15px;
  color: #FFFFFF;
  background-color: #4EBBE4;
  font-size: 12px;
  border: 1px solid #16A2D7;
  border-radius: 4px;
}

.button--addOnLeft {
  border-top-right-radius: 0;
  border-bottom-right-radius: 0;
}

.button--addOnRight {
  border-top-left-radius: 0;
  border-bottom-left-radius: 0;
}

.input {
  border: 1px solid #D7DBDD;
  padding: 0 10px;
  border-radius: 0;
  box-shadow: none;
}
```

HTML 代码
```HTML
<div class="stepperInput">
  <button class="button button--addOnLeft">-</button>
  <input type="text" placeholder="Age" value="32" class="input stepperInput__input"/>
  <button class="button button--addOnRight">+</button>
</div>
```

<a name="tabs"></a>
### 标签页 [Demo](http://www.flexboxpatterns.com/tabs)

![image](http://www.flexboxpatterns.com/images/thumbs/tabs.png)

同理，使用 `display: flex` 也可以实现这种标签页效果。

CSS 代码
```CSS
.tabs {
  /**
   * Setting display to flex makes this container lay
   * out its children using flexbox, the exact same
   * as in the above "Stepper input" example.
   */
  display: flex;

  border-bottom: 1px solid #D7DBDD;
}

.tab {
  cursor: pointer;
  padding: 5px 30px;
  color: #16A2D7;
  font-size: 12px;
  border-bottom: 2px solid transparent;
}

.tab.is-tab-selected {
  border-bottom-color: #4EBBE4;
}
```

HTML 代码
```HTML
<div class="tabs">
  <div class="tab is-tab-selected">Tab 1</div>
  <div class="tab">Tab 2</div>
  <div class="tab">Tab 3</div>
  <div class="tab">Tab 4</div>
</div>
```

_译注：tab 的切换效果可以通过纯 CSS 实现，可以参考 [CSS trick for tabs without javascript demo](http://poppinlp.com/demos/tabs-without-javascript.html)_


<a name="site-header"></a>
### 站点头部 [Demo](http://www.flexboxpatterns.com/site-header)

![image](http://www.flexboxpatterns.com/images/thumbs/siteHeader.png)

你可以把这种组件作为网站或者 webapp 的顶部。

要构建这种组件，典型方法是把 logo 和导航按钮包裹在一个容器，设置按钮放在另一个容器中。然后，使用 `float` 把两个容器方别推向两边。紧接着，你要对整个顶部元素清楚浮动。对于一个简单布局而言，这也太复杂了。

如果使用弹性盒子，你依然需要容器元素，但是你不需要为容器添加特定的样式了，因为 flexbox 已经让父元素来负责布局了。

除开 `display: flex` 属性外，我们还需要另外两个属性来调整布局：

* `justify-content: space-between` 让容器左右分开成为了可能。这个属性把 logo 和导航按钮推向了左边，把设置推向了右边。
* `align-items: center` 讲主轴上的元素垂直居中对齐。这个属性很重要，因为 logo 和导航按钮高度不同，如果不设置该属性，它们默认会对齐上边沿。

```CSS
.siteHeader {
  /**
   * Lay out the children of this container with
   * flexbox, which is horizontal by default.
   */
  display: flex;

  /**
   * Make the container put as much space as possible
   * between its children, with the children at either
   * end laying flush against the container's edges.
   */
  justify-content: space-between;

  padding: 10px;
  background-color: #56727C;
}

.siteHeader__section {
  /**
   * Lay out the children of this container with
   * flexbox.
   */
  display: flex;
  
  /**
   * Align the children in the center, along
   * the main axis. By default the children will
   * align along their top edges.
   */
  align-items: center;
}

.siteHeader__item {
  padding: 5px 15px;
  font-size: 12px;
}

.siteHeader__item + .siteHeader__item {
  margin-left: 5px;
}

.siteHeader__item.is-site-header-item-selected {
  color: #FFFFFF;
  background-color: #415F69;
  border-radius: 4px;
}

.siteHeaderLogo {
  font-size: 20px;
  line-height: 0;
  color: white;
}

.siteHeaderButton {
  cursor: pointer;
  color: #D9E9EF;
}
```

```HTML
<div class="siteHeader">
  <!-- This section gets pushed to the left side-->
  <div class="siteHeader__section">
    <div class="siteHeader__item siteHeaderLogo">
      <div class="fa fa-inbox"></div>
    </div>
    <div class="siteHeader__item siteHeaderButton is-site-header-item-selected">Inbox</div>
    <div class="siteHeader__item siteHeaderButton">Sent</div>
    <div class="siteHeader__item siteHeaderButton">Trash</div>
  </div>
  <!-- This section gets pushed to the right side-->
  <div class="siteHeader__section">
    <div class="siteHeader__item siteHeaderButton">Settings</div>
  </div>
</div>
```

<a name="form-footer"></a>
### 表单底部 [Demo](http://www.flexboxpatterns.com/form-footer)

![image](http://www.flexboxpatterns.com/images/thumbs/formFooter.png)

你也许需要在表单底部放一些进度菊花或者验证反馈。和上面的例子类似，使用弹性盒子可以将这些内容和表单提交按钮分隔开来。

CSS 代码
```CSS
.formFooter {
  /**
   * Lay out the children of this container with
   * flexbox, which is horizontal by default.
   */
  display: flex;

  /**
   * Align the children in the center, along
   * the main axis, which is horizontal in this case.
   */
  align-items: center;

   /**
   * Make the container put as much space as possible
   * between its children, with the children at either
   * end laying flush against the container's edges.
   */
  justify-content: space-between;

  border-top: 1px solid #D7DBDD;
  padding: 10px;
}

.formFooter__section {
  /**
   * This container orders items horizontally.
   */
  display: flex;

  /**
   * It aligns them vertically in the center.
   */
  align-items: center;
}

.formFooter__item + .formFooter__item {
  margin-left: 5px;
}

.formFooterFeedback {
  color: #86969C;
  font-size: 12px;
  line-height: 0;
}

.formFooterSpinner {
  animation: formFooterSpinner 1s infinite steps(8, end);
}

@keyframes formFooterSpinner {
  0%   { transform: rotate(0deg); }
  100% { transform: rotate(360deg); }
}

.button--clear {
  color: #16A2D7;
  background-color: #FFFFFF;
  border: 1px solid #FFFFFF;
}
```

HTML 代码
```HTML
<div class="formFooter">
  <!-- This section gets pushed to the left side-->
  <div class="formFooter__section">
    <div class="formFooter__item formFooterFeedback">
      <div class="fa fa-spinner formFooterSpinner"></div>&nbsp;Saving...
    </div>
  </div>
  <!-- This section gets pushed to the right side-->
  <div class="formFooter__section">
    <div class="formFooter__item button button--clear">Reset</div>
    <div class="formFooter__item button">Save</div>
  </div>
</div>
```


<a name="sidebar"></a>
### 侧边栏 [Demo](http://www.flexboxpatterns.com/side-bar)

![image](http://www.flexboxpatterns.com/images/thumbs/sideBar.png)

这也是一个相当经典的组件。你甚至不需要 flexbox 来构造它，div 就足够了…… 如果产品经理告诉你，要把其中一个按钮单独拿到下面，你可以用 `position: absolute` 来处理，当然也可以用 flexbox。

除了 `display: flex` 和 `justify-content: space-between`，我们还需要另一个属性：

* `flex-direction: column` 会将主轴 (main axis) 从水平方向改为垂直方向。正如你所猜测的那样，现在子元素将会垂直排列了。

CSS 代码
```CSS
.sideBar {
  /**
   * This container orders items according to flexbox
   * rules. By default, this would arrange its children
   * horizontally. However, the next property...
   */
  display: flex;

  /**
   * ...sets the main axis to be vertical instead of
   * horizontal, so now the children are laid out
   * vertically, from top to bottom.
   */
  flex-direction: column;

  /**
   * It will also put as much space as possible
   * between its children, with the children at either end
   * laying flush against the container's edges.
   */
  justify-content: space-between;

  height: 300px;
  width: 150px;
  border-right: 1px solid #D7DBDD;
  background-color: #FCFDFD;
  padding: 10px;
}

.sideBar__item {
  cursor: pointer;
  padding: 5px 10px;
  color: #16A2D7;
  font-size: 12px;
}

.sideBar__item.is-side-bar-item-selected {
  background-color: #EEF3F5;
  border-radius: 4px;
}
```

HTML 代码
```HTML
<div class="sideBar">
  <!-- This section gets pushed to the top-->
  <div class="sideBar__section">
    <div class="sideBar__item is-side-bar-item-selected">Inbox</div>
    <div class="sideBar__item">Contacts</div>
    <div class="sideBar__item">Account</div>
  </div>
  <!-- This section gets pushed to the bottom-->
  <div class="sideBar__section">
    <div class="sideBar__item">Legal</div>
  </div>
</div>
```


<a name="centered-propmt"></a>
### 居中提示 [Demo](http://www.flexboxpatterns.com/centered-prompt)

![image](http://www.flexboxpatterns.com/images/thumbs/centeredPropmt.png)

不使用 flexbox 的居中布局通常需要一些 Hack 技巧，比如使用绝对布局然后通过 2D transform 平移。使用 flexbox，你只需要在容器元素设置 4 个属性：

* `display: flex`
* `flex-direction: column`
* `align-items: center` 设置或检索弹性盒子元素在侧轴（纵轴）方向上的对齐方式。在这里和设置 `text-align: center` 的效果有点类似。
* `justify-content: center` 子元素向主轴中心紧挨靠拢。

CSS 代码
```CSS
.centeredPrompt {
  /**
   * Lay out the children of this container with
   * flexbox.
   */
  display: flex;

  /**
   * Rotate the main axis so that the children
   * are laid out vertically, the same as in the
   * above "Side bar" example.
   */
  flex-direction: column;

  /**
   * Align the children in the center, along
   * the main axis. Because the direction is
   * "column" this has a similar effect as setting
   * text-align: center.
   */
  align-items: center;

  /**
   * Instead of pushing the children apart, as in
   * previous examples, we will group them together
   * in the center of their container.
   */
  justify-content: center;

  min-height: 300px;
  padding: 10px;
}

.centeredPrompt__item + .centeredPrompt__item {
  margin-top: 5px;
}

.centeredPromptIcon {
  font-size: 60px;
  line-height: 0;
}

.centeredPromptLabel {
  color: #86969C;
  font-size: 30px;
  font-weight: 700;
  text-align: center;
}

.centeredPromptDetails {
  color: #86969C;
  font-size: 16px;
  margin-bottom: 10px;
  text-align: center;
}

.icon {
  color: #BCD2DA;
}
```

HTML 代码
```HTML
<div class="centeredPrompt">
  <div class="centeredPrompt__item centeredPromptIcon">
    <div class="icon fa fa-smile-o"></div>
  </div>
  <div class="centeredPrompt__item centeredPromptLabel">Welcome to the app!</div>
  <div class="centeredPrompt__item centeredPromptDetails">Thanks for signing up. Let&rsquo;s take a look around.</div>
  <div class="centeredPrompt__item button">Begin tour</div>
</div>
```

<a name="centered-icon"></a>
### 居中图标 [Demo](http://www.flexboxpatterns.com/centered-icon)

![image](http://www.flexboxpatterns.com/images/thumbs/centeredIcon.png)

使用同样的方法，我们还可以居中更多东西，比如图标。

CSS 代码
```CSS
.centeredIcon {
  /**
   * Lay out the children of this container with
   * flexbox.
   */
  display: flex;

  /**
   * As in the above "Centered prmopt" example,
   * we'll rotate the main axis so that the children
   * are ordered vertically.
   */
  flex-direction: column;

  /**
   * And just like in that example, align the children
   * in the center, along the main axis.
   */
  align-items: center;

  /**
   * Same thing here as before: group the children
   * together in the center of their container.
   */
  justify-content: center;

  border: 1px solid #D7DBDD;
  font-size: 40px;
  width: 90px;
  height: 90px;
  border-radius: 100%;
  box-shadow:
    0 2px 1px rgba(0, 0, 0, 0.05),
    0 2px 3px rgba(0, 0, 0, 0.05),
    0 4px 8px rgba(0, 0, 0, 0.05);
}
```

HTML 代码
```HTML
<div class="centeredIcon">
  <div class="icon fa fa-phone"></div>
</div>
```


<a name="feature-list"></a>
### 功能列表 [Demo](http://www.flexboxpatterns.com/feature-list)

![image](http://www.flexboxpatterns.com/images/thumbs/featureList.png)

在这个列表中，其中一行是反向排列的，实现方法很简单，只需要添加一个 flexbox 属性：

`flex-direction: row-reverse` 把容器中的子元素按照 HTML 中的顺序反向排列。

CSS 代码
```CSS
.featureListItem {
  /**
   * Lay out the children of this container with
   * flexbox, which is horizontal by default.
   */
  display: flex;

  /**
   * Align the children in the center, along
   * the main axis, which is horizontal in this case.
   */
  align-items: center;

  max-width: 400px;
  padding: 10px;
}

.featureListItem + .featureListItem {
  border-top: 1px solid #D7DBDD;
}

.featureListItem--reverse {
  /**
   * We can specify the flex-direction so that
   * the children elements are displayed in the
   * reverse order of how they appear in the
   * markup.
   */
  flex-direction: row-reverse;
}

.featureListItem__icon,
.featureListItem__description {
  padding: 5px 15px;
}

.featureListItem__icon {
  font-size: 50px;
  line-height: 0;
}

.featureListItem__description {
  color: #86969C;
  font-size: 12px;
}
```

HTML 代码
```HTML
<div class="featureListItem">
  <div class="featureListItem__icon">
    <div class="icon fa fa-calendar"></div>
  </div>
  <div class="featureListItem__description">The calendar feature makes scheduling a snap.</div>
</div>
<div class="featureListItem featureListItem--reverse">
  <div class="featureListItem__icon">
    <div class="icon fa fa-dashboard"></div>
  </div>
  <div class="featureListItem__description">Our dashboard gives you a bird&rsquo;s-eye-view-at-a-glance-on-the-go.</div>
</div>
<div class="featureListItem">
  <div class="featureListItem__icon">
    <div class="icon fa fa-envelope"></div>
  </div>
  <div class="featureListItem__description">You can get notified by email or SMS.</div>
</div>
```


<a name="card"></a>
### 卡片 [Demo](http://www.flexboxpatterns.com/card)

![image](http://www.flexboxpatterns.com/images/thumbs/card.png)

接下来复习一下，这个卡片的组件用到了此前提到的属性。

* display: flex
* flex-direction: column
* align-items: center
* justify-content: center

这里没什么新的知识点，但是为我们接下来要介绍的卡片组做了铺垫。

CSS 代码
```CSS
.card {
  /**
   * Lay out the children of this container with
   * flexbox, which is horizontal by default.
   */
  display: flex;

  /**
   * Rotate the main axis so that the children
   * are laid out vertically.
   */
  flex-direction: column;

  border: 1px solid #CAD0D2;
  border-radius: 4px;
  overflow: hidden;
}

.card__description {
  /**
   * Lay out the children of this container with
   * flexbox.
   */
  display: flex;

  /**
   * We're going to lay out this element's children
   * just like in the "Centered prompt" example.
   * First we'll rotate the main axis so that the 
   * children are laid out vertically.
   */
  flex-direction: column;

  /**
   * Just like in the "Centered prompt" example,
   * we'll align the children in the center, along
   * the main axis.
   */
  align-items: center;

  /**
   * And just like in the "Centered prompt", we'll
   * group the children in the center of their
   * container.
   */
  justify-content: center;

  padding: 15px;
}

.card__descriptionIcon {
  font-size: 32px;
  margin-bottom: 10px;
}

.card__descriptionText {
  color: #57727C;
  font-size: 12px;
  text-align: center;
}

.card__price {
  text-align: center;
  color: #57727C;
  font-size: 12px;
  font-weight: 700;
  padding: 5px 15px;
  border-top: 1px solid #D7DBDD;
  background-color: #EEF3F5;
}

.card--fixedWidth {
  max-width: 120px;
}
```

HTML 代码
```HTML
<div class="card card--fixedWidth">
  <div class="card__description">
    <div class="icon fa fa-flask card__descriptionIcon"></div>
    <div class="card__descriptionText">Science potion</div>
  </div>
  <div class="card__price">Costs $5</div>
</div>
```


<a name="card-group"></a>
### 卡片组 [Demo](http://www.flexboxpatterns.com/card-group)

![image](http://www.flexboxpatterns.com/images/thumbs/cardGroup.png)

现在我们来学习最后一个 “卡片组” 组件。我们需要考虑两个麻烦的地方：

1. 我们想要每个卡片的宽度相等，但是里面包含的内容多少可能各不相同。
2. 我们想要所有的卡片注释高度相等，同样，每张卡片的注释长度也不相等。

不适用 flexbox，你可能会想到使用 `table` 元素来实现这些需求，或者对所有元素使用绝对布局，并组合使用百分比、像素和 calc() 来实现。这样也太复杂了。

使用弹性盒子，整个问题的解决方案就变得优雅多了。这里我们引入一个新的属性，但是和之前我们提到的属性不同，这个属性应用在 **子元素** 而不是容器。

我们为每张卡片设置 `flex: 1 1 0`，使得每张卡片的宽度相等。这个属性是以下三个属性的简写方法：

* `flex-grow: 1` 设置或检索弹性盒的扩展比率。默认值为 0，我们设置为 1，此时卡片会尽可能扩展以填充容器。
* `flex-shrink: 1` 设置或检索弹性盒的收缩比率。默认值为 1。我们设置为 1，此时卡片会尽可能收缩以适应容器。
* `flex-basis: 0` 设置或检索弹性盒伸缩基准值。设置为 0 的时候，其大小仅由容器的大小所决定。

这些属性满足了第一点要求。对于我们的第二个要求，我们可以对 flex 属性稍作调整，改成 `flex: 1 1 auto`。

* `flex-basis: auto` 导致卡片注释的高度自适应，意思就是最长的注释框拥有最大的高度。由于注释同时拥有 `flex-grow: 1` 属性，因此较短注释的卡片会自动伸长来适配容器高度。

```CSS
.cardGroup {
  /**
   * Lay out the children of this container with
   * flexbox, which is horizontal by default.
   */
  display: flex;

  border: 1px solid #CAD0D2;
  border-radius: 4px;
  overflow: hidden;
}

.cardGroup__card {
  /**
   * The flex property is a short-hand for setting
   * the flex-shrink, flex-grow, and flex-basis
   * properties. These properties control how the
   * element resizes to fill its container.
   *
   * We'll also set flex-grow to 1 so that it
   * will expand to fill its container. (The
   * default value is 0.)
   *
   * We'll set flex-shrink to 1 so that the element
   * will shrink as its container gets smaller.
   * (The default value is 1.)
   *
   * Last, we set flex-basis to 0 so that its
   * size is solely determined by the size of
   * the container. (The default value
   * is auto, which would cause the content's
   * size to also be a factor in this calculation.)
   *
   * The net result of these properties is that the
   * element is a fluid size, and will expand and
   * shrink with its container and siblings, but
   * they will all have the same size, even if they
   * have different amounts of content.
   */
  flex: 1 1 0;

  border: none;
  border-radius: 0;
}

.cardGroup__card + .cardGroup__card {
  border-left: 1px solid #D7DBDD;
}

.cardGroup__cardDescription {
  /**
   * We're doing almost the exact same thing here as
   * we did above. The difference is that its
   * flex-basis is auto, so now the size of its content
   * will affect how large it is.
   */
  flex: 1 1 auto;
}
```

```HTML
<div class="cardGroup">
  <div class="card cardGroup__card">
    <div class="card__description cardGroup__cardDescription">
      <div class="icon fa fa-thumbs-o-up card__descriptionIcon"></div>
      <div class="card__descriptionText">Trial</div>
    </div>
    <div class="card__price">Free!</div>
  </div>
  <div class="card cardGroup__card">
    <div class="card__description cardGroup__cardDescription">
      <div class="icon fa fa-trophy card__descriptionIcon"></div>
      <div class="card__descriptionText">Basic tier<br/>(most popular)</div>
    </div>
    <div class="card__price">$10.00</div>
  </div>
  <div class="card cardGroup__card">
    <div class="card__description cardGroup__cardDescription">
      <div class="icon fa fa-bolt card__descriptionIcon"></div>
      <div class="card__descriptionText">Advanced tier<br/>(only for enterprise-level professionals)</div>
    </div>
    <div class="card__price">$6,000.00</div>
  </div>
</div>
```


