#NavSpy

This is a jQueryUI plugin similar to Bootstrap's Scrollspy.  It attempts to accomplish the same thing, while providing a few additional methods/events/options for you to hook into.  Throughout this introduction the terms "spy" and "target" will be used to identify certain elements.  Spy will refer to the element which recieves the active class, while target will refer to the element whose position is being checked.

##Basic Usage

Here is the minimum code needed to get started:

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
2. Within that element, a group of items with the `data-spy-on` attribute pointing to the section it should spy on.  This same element must also have a unique ID attribute.  It doesn't matter what the ID is, so long as it has one.
3. Content with the ID listed in the `data-spy-on` attribute.

## Options

This example shows how to set an offset for the activation of menu items.  This is useful if you have a sticky nav at the top, and you want to activate an item when it reaches the bottom of the sticky nav, and not after it's already partially covered.  You can also set a `bottom` paramater to deactivate a menu item before you've scrolled to the bottom of it.

| Option Name | Type    | Default | Description   |
| ----------- | ------- | ------- | ------------- |
| top         | Number  | 0       | When scrolling down, spies will be activated when their tops are this number of pixels from the top of the browser. |
| bottom      | Number  | 10      | When scrolling up, spies will be activated when their botoms are this number of pixels from the top of the browser.  This means that when scrolling up, at least this many pixels must be visible of the new target to initiate a switch. |
| bottomOut   | Boolean | True    | Use this to make the last item activate when the scroll position is at the bottom of the page. |

```js
$(".scrollspy-nav").navspy({
    top: 125    
})
```

##Events

NavSpy has a few events that you can hook into. They all use the `navspy:` namespace, so to use them you would do something like this:

```js
$(".scrollspy-nav").on("navspy:activate", function(e, id) {
    alert("The ID of the active spy is: " + id);
});
```

**All events pass an event object as the first parameter, some events pass aditional data as well.**

| Event Name        | Data Passed | Description   |
| ----------------- | ----------- | ------------- |
| navspy:activate   | Spy ID      | Called when a new nav target is activated. |
| navspy:deactivate | Spy ID      | Called when the active nav target is deactivated. |
| navspy:enter      |             | Called when scroll position comes inside the highest and lowest targets bounds after having been outside of those points. |
| navspy:exit       |             | Called when scroll position leaves the highest and lowest targets bounds after having been inside of those points. |

Currently, the `link` variable points to the ID of the menu item that is activating or deactivating.  In the future this should be updated to return a jQuery object instead.

##Methods

To call a navspy method use code like this:

```js
$(".scrollspy-nav").navspy("pause");
```

| Method     | Paramaters    | Description   |
| ---------- | ------------- | ------------- |
| pause      |               | Call this to pause all execution on navspy. Prevents navspy from updating active target. |
| unpause    |               | Use this to unpause execution.  Navspy will immediately check it's scroll position, and update the active target. |
| activate   | ID            | Pass an ID selector (`#target-name`) to this method to activate a new target.  The ID passed can *technically* be any selector or jQuery object, but it *should* be the ID of the spy you want to activate.  **Note:** This does not deactivate the currently active target, if one exists. |
| deactivate |               | Use this to deactivate the currently active target.  If you've used the `activate` method to activate more than one target, all targets will be deactivated. |
| refresh    |               | Use this to completely reset the list of targets and spies, as well as their top and bottom offsets. |

##Todos
- Improve plugin event triggering.
- Use uniqueID() to create an ID on the spy if none exists.
- Allow custom class name.
