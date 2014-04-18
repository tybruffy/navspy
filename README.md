#NavSpy

This is a jQueryUI plugin similar to Bootstrap's Scrollspy.  It attempts to accomplish the same thing, while providing a few additional features.

##Basic Usage

This shows the minimum code needed to make navspy work.

```html
<script src="//ajax.googleapis.com/ajax/libs/jquery/1.11.0/jquery.min.js"></script>
<script src="//ajax.googleapis.com/ajax/libs/jqueryui/1.10.4/jquery-ui.min.js"></script>
<ul class="navspy-menu">
    <li class="menu-item" data-spy-on="#section1" id="menu-section1">
        <a href="#section1">Section 1</a>
    </li>
    <li class="menu-item" data-spy-on="#section2" id="menu-section2">
        <a href="#section2">Section 2</a>
    </li>
    <li class="menu-item" data-spy-on="#section3" id="menu-section3">
        <a href="#section3">Section 3</a>
    </li>
</ul>

<div id="section1">
    <!-- Content! -->
</div>
<div id="section2">
    <!-- Content! -->
</div>
<div id="section3">
    <!-- Content! -->
</div>
```

```js
$(".scrollspy-nav").navspy();
```

The minimum requirements here are:

1. A containing element to call `navspy()` on.
2. Within that container, items must have a `data-spy-on` attribute which points to the section it should link to.  This same element must also have aa unique ID attribute.  It doesn't matter what the ID is, so long as it has one.
3. Content with the ID listed in the `data-spy-on` attribute.

## Setting Page Offset

This example shows how to set an offset for the activation of menu items.  This is useful if you have a sticky nav at the top, and you want to activate an item when it reaches the bottom of the sticky nav, and not after it's already partially covered.  You can also set a `bottom` paramater to deactivate a menu item before you've scrolled to the bottom of it.

```js
$(".scrollspy-nav").navspy({
    top: 125    
})
```

##Events

NavSpy has a few events that you can hook into. Here's how to use them:

```js
$(".scrollspy-nav").bind("ns.activate", function(e, link) {
    // Your code here
});
```

Here is a list of the available events and the paramaters available to them.

- ns.activate - (e, menu item ID)
- ns.deactivate - (e, menu item ID)
- ns.enter - (e)
- ns.exit - (e)

Currently, the `link` variable points to the ID of the menu item that is activating or deactivating.  In the future this should be updated to return a jQuery object instead.

##Methods

There are four methods available outside the plugin, `pause` and `unpause`.

```js
$(".scrollspy-nav").navspy("pause");
$(".scrollspy-nav").navspy("unpause");
$(".scrollspy-nav").navspy("activate", $("#new-item"));
$(".scrollspy-nav").navspy("deactivate", $(".active"));
```

The pause method will stop any new items from being activated by scrolling until the unpause event is called.  When the unpause event is called it will check your scroll position and activate a new menu item if need be.

The element passed to activate and deactivate can be a jQuery object or any jQuery selector.  For deactivate, the element is what will be passed to the deactivate event.

##Other Features

Navspy will also update it's data when the window is resized.

##Todos
- Remove listener for document.resize, shouldn't be part of plugin.
- As part of the above, make the reset function "publicly" available.
- Fix the rest of this readme.

