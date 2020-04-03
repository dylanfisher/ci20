---
title:            jQuery in-class exercises
lecture_date:     2020-04-03 00:00:00 -0500
section:          Lab
---

### Instructions

1. Remix the [Glitch ci20-jquery project](https://glitch.com/~ci20-jquery).
1. Try to complete each task using as short and simple code as possible. Try to replicate the look of the CSS and HTML exactly, including color, font size, etc.
1. The Glitch project has 6 different sets of HTML, CSS, and JavaScript files that correspond to each question.

---

### 1. Toggle Text

Use jQuery to bind a click event to the "Toggle the text" button that shows and hides the paragraph of
text each time the button is clicked.

[https://api.jquery.com/click/](https://api.jquery.com/click/)

<a href="/assets/workshops/lab/html-css-jquery-in-class-exercises/5-desk-1.jpg" target="_blank">
  <img src="/assets/workshops/lab/html-css-jquery-in-class-exercises/5-desk-1.jpg">
</a>

<a href="/assets/workshops/lab/html-css-jquery-in-class-exercises/5-desk-2.jpg" target="_blank">
  <img src="/assets/workshops/lab/html-css-jquery-in-class-exercises/5-desk-2.jpg">
</a>

---

### 2. Animate Image

Using [this image](/assets/workshops/lab/html-css-jquery-in-class-exercises/seagull.jpg), create an
interaction where when you click the seagull it moves it's position across the screen.

You might choose to do this with [animate](http://api.jquery.com/animate/) or with [addClass](https://api.jquery.com/addclass/) and doing the animation in CSS.

<a href="/assets/workshops/lab/html-css-jquery-in-class-exercises/6-desk-1.jpg" target="_blank">
  <img src="/assets/workshops/lab/html-css-jquery-in-class-exercises/6-desk-1.jpg">
</a>

<a href="/assets/workshops/lab/html-css-jquery-in-class-exercises/6-desk-2.jpg" target="_blank">
  <img src="/assets/workshops/lab/html-css-jquery-in-class-exercises/6-desk-2.jpg">
</a>

---

### 3. Random Boxes

Create an interaction so that when you click the "Select a random box" button, one of the outlined
boxes is randomly chosen and becomes filled in.

All of the boxes should start out not filled in.

<a href="/assets/workshops/lab/html-css-jquery-in-class-exercises/7-desk-1.jpg" target="_blank">
  <img src="/assets/workshops/lab/html-css-jquery-in-class-exercises/7-desk-1.jpg">
</a>

<a href="/assets/workshops/lab/html-css-jquery-in-class-exercises/7-desk-2.jpg" target="_blank">
  <img src="/assets/workshops/lab/html-css-jquery-in-class-exercises/7-desk-2.jpg">
</a>

---

### 4. Keyboard events

Use the `keypress` event listener to do something fun when the user presses a key on their keyboard. Try modifying the examples below
or do something totally original using the `keypress` event.

For example, you might want to define a series of "stamps" that map to a particular key on the keyboard.

```javascript
$(document).on('keypress', function(e) {
  var key = e.key;
  var img;
  var text;

  console.log('keypress:', key);

  if ( key == 'a' ) {
    img = 'https://upload.wikimedia.org/wikipedia/commons/8/84/Apple_Computer_Logo_rainbow.svg';
  } else if ( key == 'b' ) {
    img = 'https://upload.wikimedia.org/wikipedia/commons/f/f7/Bananas.svg';
  } else if ( key == 'c' ) {
    img = 'http://www.alsointocats.com/wp-content/uploads/2013/01/lordmeowington-828x1024.png';
  }  else if ( key == 'd' ) {
    img = 'https://images.petsmartassets.com/is/image/PetSmart/SV0401_CATEGORY_HERO-Dog-Dog-20160818?$SV0401$';
  }

  // etc.

  if ( img ) {
    $('body').append('<img src="' + img + '" style="position: fixed; top: '+ Math.random() * 100 + '%; left: ' + Math.random() * 100 + '%; transform: translate(-50%, -50%); max-width: 300px;">');
  } else {
    $('body').append('<h2 style="position: fixed; top: '+ Math.random() * 100 + '%; left: ' + Math.random() * 100 + '%; transform: translate(-50%, -50%); font-size: ' + Math.random() * 200 + 'px;">' + key + '</h2>');
  }
});
```

You could also map the keys to play audio files instead of images, and create a musical instrument in your browser. This examples uses [tone.js](https://github.com/Tonejs/Tone.js) to generate the sound in JavaScript.

```javascript
// Include tone.js in the head of your index file, before jQuery
// <script src="https://unpkg.com/tone@13.4.9/build/Tone.js"></script>
// or, load it via jQuery for the sake of testing this demo in dev tools. -->
$.getScript('https://unpkg.com/tone@13.4.9/build/Tone.js', function() {
  console.log('tone.js is loaded');
});

$(document).on('keypress', function(e) {
  var key = e.key;
  var synth = new Tone.Synth().toMaster();

  console.log('keypress:', key);

  if ( key > 0 && key < 10 ) {
    synth.triggerAttackRelease(('C' + key), '8n');
  }

  // etc.
});
```

---

### 5. Scrolling events

Using the snippets below as examples of what's possible, create a unique behavior when the `scroll` event is fired. Don't copy these
snippets exactly.

Here's a snippet of code that will move you back to the top of the page if you reach the bottom.

```javascript
var documentHeight = $(document).height();
var windowHeight = $(window).height();

$(window).on('scroll', function() {
  var scrollTop = $(this).scrollTop();

  if ( scrollTop + windowHeight >= documentHeight ) {
    $(window).scrollTop(0);
  }
});
```

Here's a snippet of code that will display a progress bar that indicates what percentage of the page you've scrolled.

```javascript
var documentHeight = $(document).height();
var windowHeight = $(window).height();

$('body').append('<div id="percentage" style="position: fixed; top: 0; left: 0; height: 30px; background-color: black;"></div>');

var $percentageIndicator = $('#percentage');

$(window).on('scroll', function() {
  var scrollTop = $(this).scrollTop();
  var percentage = scrollTop / (documentHeight - windowHeight) * 100;

  console.log(percentage + '%');

  $percentageIndicator.css({ width: percentage + '%' });
});
```

Here's a snippet of code that will resize the items on the page by a factor of how much you have scrolled down the page.

```javascript
var documentHeight = $(document).height();
var $elements = $('.sidebar > *, .page-content > *');

$(window).on('scroll', function() {
  var scrollTop = $(this).scrollTop();
  var scaleFactor = ((scrollTop / documentHeight * 4) % 1.5) + 0.2;

  console.log('scaleFactor', scaleFactor);

  $elements.css({ transform: 'scale(' + scaleFactor + ')' });
});

```

---

### 6. Click events

Use the `click` event to do something to the document whenever a user clicks on it. The examples below give you an idea of what's possible,
but for your click events please do something totally different.

Here's a snippet of code that will remove any items on the page when you click them.

```javascript
$(document).on('click', function(event) {
  // All javascript event handlers give you information about the event type in the event argument.
  console.log(event);

  // event.preventDefault() will prevent the default click event from happening in the browser.
  // This makes it so that clicking a link doesn't actually go to that link.
  event.preventDefault();

  // You can refer to items on the event object, such as the target, which represents
  // the individual DOM element you clicked.
  var $clickTarget = $(event.target);

  $clickTarget.remove();
});
```

This snippet of code is similar, but it will scale the element you click randomly each time you click it.

```javascript
$(document).on('click', function(event) {
  event.preventDefault();

  var $clickTarget = $(event.target);

  $clickTarget.css({ transform: 'scale(' + randomNumber(0.5, 1.5) + ')' });

  function randomNumber(min, max) {
    return Math.random() * (max - min) + min;
  }
});
```
