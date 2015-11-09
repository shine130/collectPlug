#Fullpage帮助文档


##1、安装插件

如果你熟悉bower或者npm，您可以使用下面的命令安装Fullpage

```javascript
// With bower
bower install fullpage.js
 
// With npm
npm install fullpage.js
当然您也可以从 Fullpage 的Github地址下载得到源文件，这两种方法所获取到的Fullpage插件文件是一样的。
```

##2、引入插件文件

这个插件依赖于jQuery，所以你还需要下载jQuery，并且在Fullpage插件之前引入。
```javascript
<link rel="stylesheet" type="text/css" href="jquery.fullPage.css" />
<script src="jquery.min.js"></script>
<script type="text/javascript" src="jquery.fullPage.js"></script>
```

如果你需要自定义页面滚动的效果，你需要引入jquery.easings.min.js文件。
```javascript
<script src="jquery.easings.min.js"></script>

```

对于内容比较多的页面，可以设置右侧的滚动条，但是默认情况下无法滚动，你需要jquery.slimscroll.min.js文件来自定义滑条滚动效果。
```javascript
<script type="text/javascript" src="jquery.slimscroll.min.js"></script>

```

最后，如果你不想下载到项目中，您可以使用开源项目CDN服务，Fullpage在CDNJS的地址：https://cdnjs.com/libraries/fullPage.js

##3、编写HTML代码

默认情况下，每一屏幕的代码都需要有DIV包裹，并且设置DIV的类名为section，默认情况下，第一个setion将作为首页显示在页面上。
```html
<div id="fullpage">
<div class="section">Some section</div>
<div class="section">Some section</div>
<div class="section">Some section</div>
<div class="section">Some section</div>
</div>
```

假如你需要让某一个section作为首页的第一屏展示，你只需要给这个section添加一个active的类，Fullpage会自动优先展示这个屏幕，例如定义下面的代码：
```html
<div class="section active">Some section</div>
```

Fullpage自带左右滑动的幻灯片，只需要在section中添加DIV元素，并且给DIV元素添加slide类，FUllpage会自动生成幻灯片特效，例如下面的代码：
```html
<div class="section">
<div class="slide"> Slide 1 </div>
<div class="slide"> Slide 2 </div>
<div class="slide"> Slide 3 </div>
<div class="slide"> Slide 4 </div>
</div>
```

##4、初始化Fullpage

使用jQuery的文档加载完毕以后执行函数，初始化Fullpage插件。

```javascript
$(document).ready(function() {
$('#fullpage').fullpage();
});
```

所有的选项设置更复杂的初始化可能看起来像这样：
```javascript
$(document).ready(function() {
$('#fullpage').fullpage({
//Navigation
menu: false,
lockAnchors: false,
anchors:['firstPage', 'secondPage'],
navigation: false,
navigationPosition: 'right',
navigationTooltips: ['firstSlide', 'secondSlide'],
showActiveTooltip: false,
slidesNavigation: true,
slidesNavPosition: 'bottom',
 
//Scrolling
css3: true,
scrollingSpeed: 700,
autoScrolling: true,
fitToSection: true,
scrollBar: false,
easing: 'easeInOutCubic',
easingcss3: 'ease',
loopBottom: false,
loopTop: false,
loopHorizontal: true,
continuousVertical: false,
normalScrollElements: '#element1, .element2',
scrollOverflow: false,
touchSensitivity: 15,
normalScrollElementTouchThreshold: 5,
 
//Accessibility
keyboardScrolling: true,
animateAnchor: true,
recordHistory: true,
 
//Design
controlArrows: true,
verticalCentered: true,
resize : false,
sectionsColor : ['#ccc', '#fff'],
paddingTop: '3em',
paddingBottom: '10px',
fixedElements: '#header, .footer',
responsiveWidth: 0,
responsiveHeight: 0,
 
//Custom selectors
sectionSelector: '.section',
slideSelector: '.slide',
 
//events
onLeave: function(index, nextIndex, direction){},
afterLoad: function(anchorLink, index){},
afterRender: function(){},
afterResize: function(){},
afterSlideLoad: function(anchorLink, index, slideAnchor, slideIndex){},
onSlideLeave: function(anchorLink, index, slideIndex, direction, nextSlideIndex){}
});
});

```

#Fullpage初始化参数

###controlArrows

默认值：true，决定是否使用控制箭头向左或向右移动幻灯片。

###verticalCentered

默认值：true，决定是否初始化后，是否垂直居中网页的内容，如果你想自定义元素的位置，那么你可以设置为false，在插件初始化后调用afterrender回调函数加载其它的脚本库设置你网页的内容。

###resize

默认值：true，是否在窗口改变大小后，自动调整网页中字体的大小。

###scrollingSpeed

默认值：700，每个屏幕滚动动画执行的时间，时间的单位为毫秒（ms）。

###sectionsColor

默认值：none，定义每个section的CSS背景演示，例如下面的代码：
```javascript
$('#fullpage').fullpage({
  sectionsColor: ['#f2f2f2', '#4BBFC3', '#7BAABE', 'whitesmoke', '#000'],
});
```

如果设置的参数不对称，比如屏幕个数多余设置的颜色个数，那么多余的屏幕默认没有背景颜色，如果屏幕个数少于设置的颜色个数，那么多余的颜色将不显示。

###anchors

默认值：[]，定义导航的锚文本信息例如（#example），每个导航文本之前用英文逗号（,）分隔，快速导航的锚文本URL也是使用的这个文本，浏览器通过此锚文本链接可以支持前进和后退按钮功能。

此选项的设置还可以作为用户的书签，当用户打开带有锚文本的URL时，Fullpage可以自动跳转到对应的section屏幕或者slide幻灯片位置。

注意，如果你使用了此选项，那么网页中不能有相同的ID，一来Fullpage插件无法准确的定位到section屏幕或者slide幻灯片位置，二来这也有悖网页中CSS的编写规范。

###lockAnchors

默认值：false，确定是否在URL中的锚点将在插件有任何影响。你仍然可以使用锚内部自己的函数和回调，但他们不会有任何作用，在网站的滚动。如果你想把fullpage.js在URL使用锚其他插件。

注意，这样的设置有助于了解anchors选项在侧边栏菜单的对应关系，与类的元素的值。通过.section它在标记的位置。

###easing

默认值：easeInOutCubic，定义了用于垂直和水平滚动的过渡效果，它要求文件vendors/jquery.easings.min.js或者jQuery UI插件，具体的动画效果你可以参考 easings插件介绍 ，你也可以使用其它的动画插件库。

###easingcss3

默认值：ease，定义在滚动屏幕中使用css3:true设置的过度效果，你可以使用 CSS3 transition-timing-function 属性 自定义多个动画效果，例如：linear、ease-out、……，或者使用cubic-bezier方法创建自定义的动画效果，你可能想要使用 Matthew Lein CSS Easing Animation Tool 创建这个。

###loopTop

默认值：false，定义屏幕滚动到第一个后，是否循序滚动到最后一个。

###loopBottom

默认值：false，定义屏幕滚动到最后一个后，是否循环滚动到第一个。

###loopHorizontal

默认值：true，定义水平的幻灯片是否循环切换。

###css3

默认值：true，确定是否使用JavaScript和CSS3转换滚动在切片和幻灯片。加快平板电脑和移动设备的浏览器支持CSS3的运动有益。如果此选项设置为true，浏览器不支持CSS3，jQuery回调函数将被替代。

###autoScrolling

默认值：true，定义屏幕是否自动滚动，还是需要用户触发事件滚动，它也影响了部分适合在平板电脑和手机浏览器/设备窗口。

###fitToSection

默认值：true，设置是否自适应整个窗口的空间，以某个section的内容为分界线，设置为true时，某个的section将填充到整个页面，否者用户可以停留在网页的任何位置。

###scrollBar

默认值：false，定义是否使用浏览器默认的滚动条，如果使用浏览器默认的滚动条，autoScrolling配置任然生效，用户也可以自由滚动的网站与滚动条和fullpage.js将适合的部分在屏幕滚动时完成。

###paddingTop

默认值：0，定义每个section固定的头部留白，例如设置paddingBottom: ’10px’、 paddingBottom: ’10em’、……，在使用固定表头的情况下有用的。

###fixedElements

默认值：null，定义的某个元素是否在网页的固定位置，元素将被关闭的插件是必要的时候，使用CSS3的选项保持滚动结构固定。它需要对这些元素的jQuery选择器字符串。例如：fixedElements: ‘#element1, .element2’。

###normalScrollElements

默认值：null，如果你想避免自动滚动，滚动时的一些元素，这是你需要使用的选项。（有用的地图，滚动div等）需要对这些元素的jQuery选择器字符串。例如：normalScrollElements: ‘#element1, .element2’。

###normalScrollElementTouchThreshold

默认值：5，定义了一个数字，测试HTML标签树的机构，是否在在移动设备上支持触摸事件。

###keyboardScrolling

默认值：true，定义是否可以通过键盘箭头事件控制section的滚动。

###touchSensitivity

默认值：5，定义了浏览器窗口的宽度/高度的百分比，多远的触摸滑动可以跳转到下一个section / slide。

###continuousVertical

默认值：false，定义向下滚动到最后一节是否应该向下滚动到第一个，如果向上滚动的第一部分应该滚动到最后一个。不兼容loopTop和loopBottom选项。

###animateAnchor

默认值：true，定义当网页的URL中有锚文本的时候，是否帮用户定位到对应的section或者slide。

###recordHistory

默认值：true，定义是否将网页滚动的的状态纪录到浏览器的历史记录中。

当设置为true时，每一个section/slide滚动的状态将纪录到浏览器的历史纪录中，这样的设置有利于用户方便回退到刚才浏览的内容。
当设置为false时候，用户的浏览路径不会记录到浏览器的历史纪录中，如果要取消这个选项可以使用autoScrolling:false。

###menu

默认值：false，一个选择器可以用来指定要与滚动互动的导航菜单，有点类似与Bootstrap的滚动监听。这样到滚动到某个section时，对应的菜单会被自动添加active类。

注意，这个选项不会自动生成一个导航菜单，仅仅是给指定的菜单中当前菜单项添加一个active活动类。

为了让自定义导航菜单和屏幕section互动，需要给菜单添加一个HTML5的自定义属性（data-menuanchor），需要和锚文本设置相同的内容，例如下面的示例代码：
```html
<ul id="myMenu">
    <li data-menuanchor="firstPage" class="active"><a href="#firstPage">First section</a></li>
    <li data-menuanchor="secondPage"><a href="#secondPage">Second section</a></li>
    <li data-menuanchor="thirdPage"><a href="#thirdPage">Third section</a></li>
    <li data-menuanchor="fourthPage"><a href="#fourthPage">Fourth section</a></li>
</ul>
```
```javascript
$('#fullpage').fullpage({
    anchors: ['firstPage', 'secondPage', 'thirdPage', 'fourthPage', 'lastPage'],
    menu: '#myMenu'
});
```
注意：注意这个自定义的菜单代码应该放置到插件设置的内容外面，避免因为排版不兼容问题可以使用css3:true，否则将被附加到body的插件本身。

###navigation

默认值：false，如果设置为true，那他将会显示一个小圆圈组成的快速导航栏。

###navigationPosition

默认值：none，结合参数navigation一起使用，用于设置navigation定义的菜单显示的位置，可以设置为left/right。

###navigationTooltips

默认值：[]，定义当navigation设置为true的时候，鼠标移动到快速导航上面的提示文本，每个属性中间用英文半角逗号（,）隔开。

###showActiveTooltip

默认值：false，设置是否自动显示navigationTooltips中设置的工具提示文本。

###slidesNavigation

默认值：false，使用方法同navigation，不过这个参数设置的导航显示位置不同，而且这个是用户设置幻灯片的。

###slidesNavPosition

默认值：bottom，定义slidesNavigation中设置的导航菜单显示的位置，可选的设置值为top/bottom，你可能要修改CSS样式确定的距离从顶部或底部以及任何其他风格如颜色。

###scrollOverflow

默认值：false，设置当内容超过屏幕的高度的时候，是否裁切多余的内容。

当设置为true时，你的内容将会被自动裁切，可以考虑当afterRender回调函数调用的时候，处理你的内容的多少或者使用其它的插件库合理的处理多余的内容。
当设置为false时，插件不会自动裁切多余的内容，但是剩下没有显示的内容任然不能显示，此时，你可以使用 jquery.slimscroll.min插件来自定义滚动事件，如果要使用这个插件，应该在Fullpage插件之前引入，例如下面的代码：
```html
<script type="text/javascript" src="vendors/jquery.slimscroll.min.js"></script>
<script type="text/javascript" src="jquery.fullPage.js"></script>
```

###sectionSelector

默认值：.section，定义用于选择全屏滚动内容的jQuery选择器。它可能需要改变，有时为了避免与其他插件使用相同的选择器作为整版的问题。

###slideSelector

默认值：.slide，定义用于插件幻灯片jQuery选择器。它可能需要改变，有时为了避免与其他插件使用相同的选择器fullpage.js问题。

###responsiveWidth

默认值：0， A normal scroll (autoScrolling:false) will be used under the defined width in pixels. A class fp-responsive is added to the plugin&#8217;s container in case the user wants to use it for his own responsive CSS. For example, if set to 900, whenever the browser&#8217;s width is less than 900 the plugin will scroll like a normal site.

###responsiveHeight

默认值：0， A normal scroll (autoScrolling:false) will be used under the defined height in pixels. A class fp-responsive is added to the plugin&#8217;s container in case the user wants to use it for his own responsive CSS. For example, if set to 900, whenever the browser&#8217;s height is less than 900 the plugin will scroll like a normal site.

##Fullpage方法函数

###moveSectionUp()

设置section向上滚动
```javascript
$.fn.fullpage.moveSectionUp();
```

###moveSectionDown()

设置section向下滚动
```javascript
$.fn.fullpage.moveSectionDown();
```

###moveTo(section, slide)

设置屏幕滚动到某个section或者slide，两个参数都是某个内容块的索引值或者是锚文本，默认情况下slide的索引被设置为0。
```javascript
/*Scrolling to the section with the anchor link `firstSlide` and to the 2nd Slide */
$.fn.fullpage.moveTo('firstSlide', 2);
 
//Scrolling to the 3rd section in the site
$.fn.fullpage.moveTo(3, 0);
 
//Which is the same as
$.fn.fullpage.moveTo(3);
silentMoveTo(section, slide)
```

这个函数的用法和MoveTo方法完全一样，只是MoveTo在切换的时候有动画效果，而silentMoveTo方法在切换的时候没有动画效果，直接跳转到对应的section中。
```javascript
/*Scrolling to the section with the anchor link `firstSlide` and to the 2nd Slide */
$.fn.fullpage.silentMoveTo('firstSlide', 2);
```

###moveSlideRight()

设置幻灯片向右滑动，将下一个幻灯片显示在当前的屏幕中。
```javascript
$.fn.fullpage.moveSlideRight();
```

###moveSlideLeft()

设置幻灯片向左滑动，将上一个幻灯片显示在当前的屏幕中。
```javascript
$.fn.fullpage.moveSlideLeft();
setAutoScrolling(boolean)
```

可以实时的控制页面滚动的方式，可选的参数false/true。

如果参数被设置为true，所有的section将自动滚动。
如果参数被设置为false，所有的section将不会自动滚动，需要用户手动或者使用浏览器的滑条滚动网页。
注意，scrollOverflow参数如果设置为true，它可能很难滚动鼠标滚轮或触摸板当部分滚动。
```javascript
$.fn.fullpage.setAutoScrolling(false);
```

###setFitToSection(boolean)

该函数设置选项fitToSection确定是否自适应section在屏幕上。
```javascript
$.fn.fullpage.setFitToSection(false);
```

###setLockAnchors(boolean)

设置选项lockAnchors确定将锚文本锁定到URL中。
```javascript
$.fn.fullpage.setLockAnchors(false);
```

###setAllowScrolling(boolean, [directions])

添加或者禁止Fullpage自动绑定的鼠标滑轮和移动触摸事件，不过用户任然可以通过键盘和点击快速导航的方式切换section/slide。要取消键盘事件你应该使用setKeyboardScrolling方法。

directions，可选参数，可以设置的值：all, up, down, left, right或者设置组合的参数，例如down, right，他设置的两个方向上将禁止或者激活滚动。
```javascript
//disabling scrolling
$.fn.fullpage.setAllowScrolling(false);
 
//disabling scrolling down
$.fn.fullpage.setAllowScrolling(false, 'down');
 
//disabling scrolling down and right
$.fn.fullpage.setAllowScrolling(false, 'down, right');
```

###setKeyboardScrolling(boolean, [directions])

添加或者禁止键盘对section/slide的控制，这个事件是默认绑定的。

directions，可选参数，可以设置的值：all, up, down, left, right或者设置组合的参数，例如down, right，他设置的两个方向上将禁止或者激活键盘的滚动。
```javascript
//disabling all keyboard scrolling
$.fn.fullpage.setKeyboardScrolling(false);
 
//disabling keyboard scrolling down
$.fn.fullpage.setKeyboardScrolling(false, 'down');
 
//disabling keyboard scrolling down and right
$.fn.fullpage.setKeyboardScrolling(false, 'down, right');
```

###setRecordHistory(boolean)

定义是否为每个URL的变更纪录到浏览器中的历史记录中。
```javascript
$.fn.fullpage.setRecordHistory(false);
```

###setScrollingSpeed(milliseconds)

定义每个section/slide滚动的时间，默认的时间单位为毫秒（ms）。
```javascript
$.fn.fullpage.setScrollingSpeed(700);
```

###destroy(type)

移除Fullpage的事件和添加的HTML/CSS样式风格，理想的使用在使用Ajax加载内容。

type：可以被设置为空字符，或者all，如果一旦执行，通过Fullpage添加的HTML/CSS样式和代码都将会被移除，将显示没有使用Fullpage的样式，一个使用过任何插件进行修改。
```javascript
//destroy any plugin event (scrolls, hashchange in the URL...)
$.fn.fullpage.destroy();
 
//destroy any plugin event and any plugin modification done over your original HTML markup.
$.fn.fullpage.destroy('all');
```

###reBuild()

更新DOM结构以适应新的窗口大小或其内容。理想的使用与Ajax调用或外部网站的DOM结构的变化组合。
```javascript
$.fn.fullpage.reBuild();
```

###资源延时加载

fullpage.js提供了一种懒加载图像，视频和音频元素，所以他们不会放慢您的网站加载或不必要的浪费数据传输。使用延迟加载时，所有这些元素只会加载时进入视口。启用延迟加载，所有你需要做的是改变你的src属性的data-src如下图所示：
```html
<img data-src="image.png">
<video>
  <source data-src="video.webm" type="video/webm" />
  <source data-src="video.mp4" type="video/mp4" />
</video>
```

##Fullpage回调函数

###afterLoad (anchorLink, index)

滚动到某一屏后的回调函数，接收 anchorLink 和 index 两个参数。

anchorLink 是锚链接的名称
index 是section的索引，从1开始计算
在没有设置锚文本的情况下，只有使用唯一的index参数。
```javascript
$('#fullpage').fullpage({
    anchors: ['firstPage', 'secondPage', 'thirdPage', 'fourthPage', 'lastPage'],
    afterLoad: function(anchorLink, index){
        var loadedSection = $(this);
        //using index
        if(index == 3){
            alert("Section 3 ended loading");
        }
        //using anchorLink
        if(anchorLink == 'secondSlide'){
            alert("Section 2 ended loading");
        }
    }
});
```

###onLeave (index, nextIndex, direction)

滚动前的回调函数，接收 index、nextIndex 和 direction 3个参数

index 是离开的“页面”的序号，从1开始计算；
nextIndex 是滚动到的“页面”的序号，从1开始计算；
direction 判断往上滚动还是往下滚动，值是 up 或 down。
```javascript
$('#fullpage').fullpage({
    onLeave: function(index, nextIndex, direction){
        var leavingSection = $(this);
        //after leaving section 2
        if(index == 2 &amp;&amp; direction =='down'){
            alert("Going to section 3!");
        }
        else if(index == 2 &amp;&amp; direction == 'up'){
            alert("Going to section 1!");
        }
    }
});
```

取消section的滚动

你可以在onLeave 回调函数中返回false，那么将取消滚动。
```javascript
$('#fullpage').fullpage({
    onLeave: function(index, nextIndex, direction){
        //it won't scroll if the destination is the 3rd section
        if(nextIndex == 3){
            return false;
        }
    }
});
```

###afterRender()

这个回调函数只是在生成页面结构的时候调用。这是要用来初始化其他插件或删除任何需要的文件准备好代码的回调（这个插件修改DOM创建得到的结构）。
```javascript
$('#fullpage').fullpage({
    afterRender: function(){
        var pluginContainer = $(this);
        alert("The resulting DOM structure is ready");
    }
});
```

###afterResize()

这个回调函数在窗口发生大小改变的时候被调用，就在部分调整。
```javascript
$('#fullpage').fullpage({
    afterResize: function(){
        var pluginContainer = $(this);
        alert("The sections have finished resizing");
    }
});
```

###afterSlideLoad (anchorLink, index, slideAnchor, slideIndex)

滚动到某一水平滑块后的回调函数，与 afterLoad 类似，接收 anchorLink、index、slideIndex、direction 4个参数。

anchorLink: anchorLink corresponding to the section.
index: index of the section. Starting from 1.
slideAnchor: anchor corresponding to the slide (in case there is)
slideIndex: index of the slide. Starting from 1. (the default slide doesn&#8217;t count as slide, but as a section)
在没有anchorlinks的幻灯片或幻灯片SlideIndex参数是唯一使用定义的情况下。
```javascript
$('#fullpage').fullpage({
    anchors: ['firstPage', 'secondPage', 'thirdPage', 'fourthPage', 'lastPage'],
 
    afterSlideLoad: function( anchorLink, index, slideAnchor, slideIndex){
        var loadedSlide = $(this);
 
        //first slide of the second section
        if(anchorLink == 'secondPage' &amp;&amp; slideIndex == 1){
            alert("First slide loaded");
        }
 
        //second slide of the second section (supposing #secondSlide is the
        //anchor for the second slide
        if(index == 2 &amp;&amp; slideIndex == 'secondSlide'){
            alert("Second slide loaded");
        }
    }
});
```

###onSlideLeave (anchorLink, index, slideIndex, direction, nextSlideIndex)

某一水平滑块滚动前的回调函数，与 onLeave 类似，接收 anchorLink、index、slideIndex、direction 4个参数。

anchorLink: anchorLink corresponding to the section.
index: index of the section. Starting from 1.
slideIndex: index of the slide. Starting from 0.
direction: takes the values right or left depending on the scrolling direction.
nextSlideIndex: index of the destination slide. Starting from 0.
```javascript
$('#fullpage').fullpage({
    onSlideLeave: function( anchorLink, index, slideIndex, direction, nextSlideIndex){
        var leavingSlide = $(this);
 
        //leaving the first slide of the 2nd Section to the right
        if(index == 2 &amp;&amp; slideIndex == 0 &amp;&amp; direction == 'right'){
            alert("Leaving the fist slide!!");
        }
 
        //leaving the 3rd slide of the 2nd Section to the left
        if(index == 2 &amp;&amp; slideIndex == 2 &amp;&amp; direction == 'left'){
            alert("Going to slide 2! ");
        }
    }
});
```

取消slide滑动

你可以设置回调函数onSlideLeave 返回false，那么他将阻止此次的滑动事件，就像onLeave一样。