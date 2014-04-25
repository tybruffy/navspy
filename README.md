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
$(".navspy-menu").navspy();
```

The minimum requirements here are:

1. A containing element to call `navspy()` on.
2. Within that container, items must have a `data-spy-on` attribute which points to the section it should link to.  This same element must also have aa unique ID attribute.  It doesn't matter what the ID is, so long as it has one.
3. Content with the ID listed in the `data-spy-on` attribute.

## Options

This example shows how to set an offset for the activation of menu items.  This is useful if you have a sticky nav at the top, and you want to activate an item when it reaches the bottom of the sticky nav, and not after it's already partially covered.  You can also set a `bottom` paramater to deactivate a menu item before you've scrolled to the bottom of it.

| Option Name | Type    | Description   |
| ----------- | ------- | ------------- |
| top         | Integer | When scrolling down, spies will be activated when their tops are this number of pixels from the top of the browser. |
| bottom      | Integer | When scrolling up, spies will be activated when their botoms are this number of pixels from the top of the browser. |
| bottomOut   | Boolean | Use this to make the last item activate when the scroll position is at the bottom of the page. |

```js
$(".scrollspy-nav").navspy({
    top: 125    
})
```

##Events

NavSpy has a few events that you can hook into. They all fall within the `navspy:` namespace, so to use them you would do something like this:

```js
$(".scrollspy-nav").on("navspy:activate", function(e, link) {
    alert("The ID of the active target is: " + link);
});
```

Here is a list of the available events and the paramaters available to them.

| Event Name        | Data Passed           | Description   |
| ----------------- | --------------------- | ------------- |
| navspy:activate   | (event, menu item ID) | Called when a new nav target is activated. |
| navspy:deactivate | (event, menu item ID) | Called when the active nav target is deactivated. |
| navspy:enter      | (event)               | Called when scroll position comes inside the highest and lowest targets bounds after having been outside of those points. |
| navspy:exit       | (event)               | Called when scroll position leaves the highest and lowest targets bounds after having been inside of those points. |

Currently, the `link` variable points to the ID of the menu item that is activating or deactivating.  In the future this should be updated to return a jQuery object instead.

##Methods

To call a navspy method use code like this:

```js
$(".scrollspy-nav").navspy("pause");
```

| Method     | Paramaters    | Description   |
| ---------- | ------------- | ------------- |
| pause      |               | Call this to pause all execution on navspy. Prevents navspy from updating any of it's settings. |
| unpause    |               | Use this to unpause execution.  Navspy will immediately check it's scroll position, but it will not refresh it's settings in case of updated target sizes. |
| activate   | ID            | Pass an ID selector (`#target-name`) to this method to activate a new target.  **Note:** This does not deactivate the currently active target, if one exists.
| deactivate |               | Use this to deactivate the currently active target.  If you've used the `activate` method to activate more than one target, all targets will be deactivated. |
| refresh    |               | Use this to completely reset the list of targets and spies, as well as their top and bottom offsets.. |

The pause method will stop any new items from being activated by scrolling until the unpause event is called.  When the unpause event is called it will check your scroll position and activate a new menu item if need be.

The element passed to activate and deactivate can be a jQuery object or any jQuery selector.  For deactivate, the element is what will be passed to the deactivate event.

##Todos
- Add pause event
- Improve plugin event handling
- Fix the rest of this readme.

