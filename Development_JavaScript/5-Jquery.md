#Jquery

Jquery is a fast and concise library that simplifies HTML document traversing, event handling, animating, and Ajax interactions for rapid web development


## On ready
The full library is loaded as one function that sits in the window object. In order to use jQuery we need the browser to load all the HTML & CSS first.
When the DOM is fully loaded and ready to be used it emits an event called onDOMReady.  JQuery then picks this up and fires your code.

```javascript
$(function(){
/* code goes here */
});
```

## The Two Phases of JQuery
### Phase 1: Select Element(s)

```javascript
$("h1");
Select By Class

$(".myClass");
$(".myClass p");
$(".myClass .myChildClass");
Select By ID

$("#myDiv");
```

## Phase 2: Manipulation

```javascript
$("#dropdown-menu").slideUp();
$(".my-icons").fadeOut();
```

## Event Bindings

```javascript 
var $redLightControl = $('#red-light-control');

$redLightControl.on('click.onOffToggle', function(){

var $redLights = $('.light.stop');
$redLights.toggleClass('on');
return false;
});
