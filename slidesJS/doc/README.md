#SlidesJS说明文档

[官方网站](http://slidesjs.com/)

##Overview

SlidesJS is a responsive slideshow plug-in for jQuery (1.7.1+) with features like touch and CSS3 transitions. Give it a try above and check out the examples to help you get started adding SlidesJS to your project.

**Responsive**

Create dynamic slideshows that adapt to any screen.

**Touch**

Swipe support that tracks touch movements on supported devices.

**CSS3 transitions**

Animations that run smoothly on modern devices.

**Easy setup**

Get going fast with the easy-to-use examples.

####Want to contribute to SlidesJS? Check it out at [GitHub](https://github.com/nathansearles/Slides/tree/SlidesJS-3).


##Examples

[Standard slideshow](../code/examples/standard/index.html)

[Playing and stopping slideshow](../code/examples/playing/index.html)

[Multiple slideshows](../code/examples/multiple/index.html)

[Using callbacks](../code/examples/callbacks/index.html)

[Basic sliding slideshow (unstyled)](../code/examples/basic-slide/index.html)

[Basic fading slideshow (unstyled)](../code/examples/basic-fade/index.html)



##Docs

####Basic markup
```html
<!doctype html>
<head>
  <style>
    /* Prevents slides from flashing */
    #slides {
      display:none;
    }
  </style>

  <script src="http://code.jquery.com/jquery-latest.min.js"></script>
  <script src="jquery.slides.min.js"></script>

  <script>
    $(function(){
      $("#slides").slidesjs({
        width: 940,
        height: 528
      });
    });
  </script>
</head>
<body>
  <div id="slides">
    <img src="http://placehold.it/940x528">
    <img src="http://placehold.it/940x528">
    <img src="http://placehold.it/940x528">
    <img src="http://placehold.it/940x528">
    <img src="http://placehold.it/940x528">
  </div>
</body>
```

####Options

**width (number) & height (number)**

Set width and height of the slideshow.
```javascript
$(function(){
  $("#slides").slidesjs({
    width: 700,
    height: 393
  });
});
```

This must be defined.

**start (number)**

Set the first slide in the slideshow. 

```javascript
$(function(){
  $("#slides").slidesjs({
    start: 3
  });
});
```

Default value is 1.

**navigation (object)**

Next and previous button settings.
```javascript
$(function(){
  $("#slides").slidesjs({
    navigation: {
      active: true,
        // [boolean] Generates next and previous buttons.
        // You can set to false and use your own buttons.
        // User defined buttons must have the following:
        // previous button: class="slidesjs-previous slidesjs-navigation"
        // next button: class="slidesjs-next slidesjs-navigation"
      effect: "slide"
        // [string] Can be either "slide" or "fade".
    }
  });
});
```

**pagination (object)**

Pagination settings 

```javascript
$(function(){
  $("#slides").slidesjs({
    pagination: {
      active: true,
        // [boolean] Create pagination items.
        // You cannot use your own pagination. Sorry.
      effect: "slide"
        // [string] Can be either "slide" or "fade".
    }
  });
});

```

**play (object)**

Play and stop button setting.

```javascript
$(function(){
  $("#slides").slidesjs({
    play: {
      active: true,
        // [boolean] Generate the play and stop buttons.
        // You cannot use your own buttons. Sorry.
      effect: "slide",
        // [string] Can be either "slide" or "fade".
      interval: 5000,
        // [number] Time spent on each slide in milliseconds.
      auto: false,
        // [boolean] Start playing the slideshow on load.
      swap: true,
        // [boolean] show/hide stop and play buttons
      pauseOnHover: false,
        // [boolean] pause a playing slideshow on hover
      restartDelay: 2500
        // [number] restart delay on inactive slideshow
    }
  });
});

```

**effect (object)**

```javascript
$(function(){
  $("#slides").slidesjs({
    effect: {
      slide: {
        // Slide effect settings.
        speed: 200
          // [number] Speed in milliseconds of the slide animation.
      },
      fade: {
        speed: 300,
          // [number] Speed in milliseconds of the fade animation.
        crossfade: true
          // [boolean] Cross-fade the transition.
      }
    }
  });
});
```

**callback (function)**

SlidesJS callbacks.
```javascript
$(function(){
  $("#slides").slidesjs({
    callback: {
      loaded: function(number) {
        // Do something awesome!
        // Passes start slide number
      },
      start: function(number) {
        // Do something awesome!
        // Passes slide number at start of animation
      },
      complete: function(number) {
        // Do something awesome!
        // Passes slide number at end of animation
      }
    }
  });
});
```


