# jQuery — Web Applications (A.Y. 2025/2026)

## Detailed Summary of: *16-webapp-2025-26-jquery.pdf*

**Course:** Web Applications  
**Degrees:** Master in Computer Engineering, Cybersecurity, ICT for Internet and Multimedia  
**Academic Year:** 2025/2026  
**Author:** Nicola Ferro — Intelligent Interactive Information Access (IIIA) Hub, Department of Information Engineering, University of Padua

---

## Table of Contents

1. [Introduction to jQuery](#1-introduction-to-jquery)
2. [jQuery Getters and Setters](#2-jquery-getters-and-setters)
3. [Altering the DOM Structure](#3-altering-the-dom-structure)
4. [Handling Events with jQuery](#4-handling-events-with-jquery)
5. [AJAX with jQuery](#5-ajax-with-jquery)

---

## 1. Introduction to jQuery

### 1.1 What is jQuery

jQuery is a **fast, small, and feature-rich JavaScript library** available at [jquery.com](http://jquery.com/). It offers a simple way to achieve a variety of common JavaScript tasks quickly and **consistently across all major browsers**, without any fallback code needed. The library was created to address the complexities and inconsistencies of cross-browser JavaScript development, and it has become one of the most widely used JavaScript libraries in the world.

jQuery allows developers to:

- **Select elements** in a simpler and more powerful way using CSS-style selectors, eliminating the need for verbose `getElementById()` or `getElementsByTagName()` calls.
- **Manipulate the DOM tree** with concise, chainable methods that operate on sets of elements simultaneously.
- **Attach event listeners** without any fallback code, handling cross-browser differences transparently.

### 1.2 Why jQuery?

jQuery is a lightweight, **"write less, do more"** JavaScript library. Its aim is to make it easier to use JavaScript on a website. It allows developers to perform many tasks that otherwise would have required many lines of JavaScript code in **single lines of code**. While there are many other JavaScript libraries available, jQuery is one of the most **popular and extensible**.

Some of jQuery's core features include:

- **HTML/DOM manipulation** — Selecting, creating, modifying, and removing elements
- **CSS manipulation** — Getting and setting styles and classes
- **HTML event methods** — Registering and managing event handlers
- **Effects and animations** — Showing, hiding, fading, and sliding elements
- **AJAX** — Making asynchronous HTTP requests to the server
- **Utilities** — Helper functions for common programming tasks

### 1.3 jQuery Basics

The jQuery library defines a single global function named **`jQuery()`**, with the symbol **`$`** as a shortcut for it. This is the entry point to all jQuery functionality:

```javascript
var divs = $("div");
```

The value returned by this function represents a **set of zero or more DOM elements** and is known as a **jQuery object**. jQuery objects define many methods for operating on the sets of elements they represent. One of the most powerful features of jQuery is **method chaining**, where multiple operations can be performed on a selection in a single statement:

```javascript
$("p.details").css("background-color", "yellow").show("fast");
```

This chained call selects all `<p>` elements with class "details", sets their background color to yellow, and then shows them with a fast animation — all in one concise line.

### 1.4 jQuery Objects

jQuery objects are **array-like** — they behave like arrays but are not true arrays. They have the following properties:

- **`length`** — The number of elements in the jQuery object.
- **`selector`** — The selector string (if any) that was used when the jQuery object was created.
- **`context`** — The context object that was passed as the second argument to `$()`, or the Document object otherwise.
- **`jquery`** — A property that identifies the object as a jQuery object. Testing for the existence of this property is a simple way to **distinguish jQuery objects** from other array-like objects.

### 1.5 Queries and Query Results

When you pass a CSS selector string to `$()`, it returns a jQuery object that represents the **set of matched elements**. jQuery objects are array-like: they have a `length` property, and you can access the contents using standard square-bracket array notation:

```javascript
$("body").length      // number of <body> elements
$("body")[0]          // the first (and only) <body> element
```

If you prefer not to use array notation with jQuery objects, you can use:

- **`size()`** method — Instead of the `length` property
- **`get()`** method — Instead of indexing with square brackets
- **`toArray()`** method — To convert a jQuery object to a true array

### 1.6 Creating DOM Elements

If a string is passed as the parameter to `$()`, jQuery examines the string to see if it looks like HTML (i.e., it starts with `<tag ...>`). If not, the string is interpreted as a **selector expression**. But if the string is an HTML snippet, jQuery attempts to **create new DOM elements**, and then a jQuery object is created and returned:

```javascript
var img = $("<img/>", {
  src: url,
  css: { borderWidth: 5 },
  click: handleClick
});
```

This powerful feature allows you to create new elements and immediately set their attributes, CSS styles, and event handlers in a single, expressive call.

### 1.7 The `each()` Method

If you want to loop over all elements in a jQuery object, you can call the **`each()`** method instead of writing a `for` loop. The `each()` method is similar to the `forEach()` array method. It expects a **callback function** as its sole argument, and it invokes that callback function once for each element in the jQuery object:

```javascript
$("div").each(function(index, element) {
  // operate on each div
});
```

Despite the power of the `each()` method, it is **not very commonly used**, since jQuery methods usually **iterate implicitly** over the set of matched elements and operate on them all. This implicit iteration is one of the key design principles that makes jQuery code so concise.

---

## 2. jQuery Getters and Setters

### 2.1 Overview

jQuery objects allow you to **get or set** the value of HTML attributes, CSS styles, or element content using a unified method interface. The key principles of jQuery getters and setters are:

- **Single method, dual role:** jQuery uses a single method as both getter and setter. If you pass a new value to the method, it **sets** that value; if you don't specify a value, it **returns** the current value.
- **Setters affect all elements:** When used as setters, these methods set values on **every element** in the jQuery object, and then return the jQuery object to allow **method chaining**.
- **Getters query only the first element:** When used as getters, these methods query only the **first element** of the set and return a single value. Therefore, getters can only appear at the **end** of a method chain.
- **Object arguments:** When used as setters, these methods often accept **object arguments**, where each property specifies a name and a value to be set.
- **Function values:** When used as setters, these methods often accept **functions as values**. In this case, the function is invoked to compute the value to be set.

### 2.2 Getting and Setting HTML Attributes

The **`attr()`** method acts as both a getter and a setter for HTML attributes:

**`attr()` as setter:**
```javascript
// Set a single attribute on all <a> elements
$("a").attr("href", "allMyHrefsAreTheSameNow.html");

// Set multiple attributes at once using an object
$("a").attr({
  title: "all titles are the same too!",
  href: "somethingNew.html"
});
```

**`attr()` as getter:**
```javascript
// Get the href attribute of the first <a> element
$("a").attr("href");
```

### 2.3 Getting and Setting CSS Attributes

The **`css()`** method is similar to the `attr()` method, but it works with the **CSS styles** of an element. When querying style values, `css()` returns the **current (or computed) style** of the element — the returned value may come from the `style` attribute or from a stylesheet.

**Setting CSS properties:**
```javascript
// Set a single CSS property
$("h1").css("fontSize", "100px");

// Set multiple CSS properties using an object
$("h1").css({
  fontSize: "100px",
  color: "red"
});
```

**Getting CSS properties:**
```javascript
$("h1").css("fontSize");    // returns computed font size
$("h1").css("font-size");   // same, using CSS property name
```

Note that jQuery accepts both CSS property names (`font-size`) and JavaScript camelCase names (`fontSize`) when getting and setting CSS properties.

### 2.4 Getting and Setting CSS Classes

jQuery defines dedicated methods for working with CSS classes, which is often more appropriate than directly manipulating the `class` attribute:

- **`addClass()`** — Adds one or more classes to the selected elements.
- **`removeClass()`** — Removes one or more classes from the selected elements.
- **`toggleClass()`** — Adds classes to elements that don't already have them and removes classes from those that do. This is particularly useful for creating toggle effects.
- **`hasClass()`** — Tests for the presence of a specified class, returning `true` or `false`.

```javascript
var h1 = $("h1");
h1.addClass("big");         // add class "big"
h1.removeClass("big");      // remove class "big"
h1.toggleClass("big");      // toggle class "big"

if (h1.hasClass("big")) {   // check if class "big" is present
  // ...
}
```

### 2.5 Getting and Setting HTML Form Values

The **`val()`** method is used for setting and querying the `value` attribute of HTML form elements. It also works for querying and setting the **selection state** of checkboxes, radio buttons, and `<select>` elements.

**Setting the input value:**
```javascript
$("input[type=text].tags").val(function(index, value) {
  return value.trim();
});
```

**Getting input values:**
```javascript
var singleValues = $("#single").val();
var multipleValues = $("#multiple").val();
```

The `val()` method is essential for form handling in jQuery, making it straightforward to read user input and programmatically set form values.

### 2.6 Getting and Setting Element Content

The **`text()`** and **`html()`** methods query and set the plain-text or HTML content of an element or elements:

- **`text()`** — When invoked with no arguments, returns the **plain-text content** of all descendant text nodes of all matched elements. When called with a string argument, it sets the plain-text content, replacing all existing content.
- **`html()`** — When invoked with no arguments, returns the **HTML content** of just the **first matched element**. When called with a string argument, it sets the HTML-formatted text content, replacing all existing content.

The key difference is that `text()` works with plain text (and thus is safe against XSS injection), while `html()` works with HTML markup and can insert formatted content. Also note that `text()` aggregates content from all matched elements, whereas `html()` only returns the content of the first element.

---

## 3. Altering the DOM Structure

### 3.1 Inserting and Replacing Elements

Each of jQuery's insertion and replacement methods takes an argument that specifies the content to be inserted into the document. This can be a string of **plain text or HTML** to specify new content, or it can be a **jQuery object** or an **Element or text Node**. The insertion is made into, before, after, or in place of (depending on the method) each of the selected elements.

Important behaviors:
- If the content to be inserted is an element that **already exists** in the document, it is **moved** from its current location.
- If it is to be inserted **more than once**, the element is **cloned** as necessary.
- These methods all **return the jQuery object** on which they are called, enabling method chaining.

jQuery provides two styles for insertion methods:

| Operation | `$(target).method(content)` | `$(content).method(target)` |
|-----------|----------------------------|----------------------------|
| Insert content at end of target | `append()` | `appendTo()` |
| Insert content at start of target | `prepend()` | `prependTo()` |
| Insert content after target | `after()` | `insertAfter()` |
| Insert content before target | `before()` | `insertBefore()` |
| Replace target with content | `replaceWith()` | `replaceAll()` |

The difference between the two columns is the **direction of the operation**: in the left column, you call the method on the target and pass the content; in the right column, you call the method on the content and pass the target.

**Examples:**
```javascript
// Target-method-content style
$("#log").append("<br/>" + message);
$("p").prepend("<b>Hello </b>");
$("h1").before("<hr/>");
$("h1").after("<hr/>");
$("hr").replaceWith("<br/>");

// Content-method-target style
$("<br/>" + message).appendTo("#log");
$(document.createTextNode("<b>Hello </b>")).prependTo("p");
$("<hr/>").insertBefore("h1");
$("<hr/>").insertAfter("h1");
$("<br/>").replaceAll("hr");
```

More examples are available at: [W3Schools jQuery HTML Reference](https://www.w3schools.com/jquery/jquery_ref_html.asp)

### 3.2 Copying Elements

If you insert elements that are already part of the document, those elements will simply be **moved** (not copied) to their new location. If you are inserting the elements in more than one place, jQuery will make copies as needed. However, if you want to explicitly copy elements to a new location instead of moving them, you must first make a copy with the **`clone()`** method.

`clone()` makes and returns a **copy (jQuery object)** of each selected element and of all of the **descendants** of those elements. This is a deep clone — it copies the entire subtree of elements.

**Example:**
```html
<div class="container">
  <div class="hello">Hello</div>
  <div class="goodbye">Goodbye</div>
</div>
```

```javascript
$(".hello").clone().appendTo(".goodbye");
```

**Result:**
```html
<div class="container">
  <div class="hello">Hello</div>
  <div class="goodbye">
    Goodbye
    <div class="hello">Hello</div>
  </div>
</div>
```

The original `.hello` element remains in place, while a cloned copy is appended to `.goodbye`.

### 3.3 Wrapping Elements

jQuery defines three wrapping functions that allow you to wrap elements with additional HTML structure:

- **`wrap()`** — Wraps **each** of the selected elements individually with the specified wrapper element.
- **`wrapInner()`** — Wraps the **contents** (inner content) of each selected element with the specified wrapper.
- **`wrapAll()`** — Wraps the selected elements **as a group** with a single wrapper element.

These methods are usually passed a newly created wrapper element or a string of HTML used to create a wrapper:

```javascript
$("h1").wrap(document.createElement("i"));               // wrap each h1 in an <i> element
$(".inner").wrapInner("<div class='new'></div>");         // wrap inner content of each .inner
$(".inner").wrapAll("<div class='new'></div>");            // wrap all .inner elements as a group
```

### 3.4 Deleting Elements

jQuery defines several methods for deleting elements from the DOM, each with different behaviors:

- **`empty()`** — Removes **all children** of each of the selected elements. The elements themselves remain in the document, but their content is cleared.
- **`remove()`** — Removes the selected elements (together with their **event handlers and data**) from the document entirely. If you pass an argument, that argument is treated as a selector, and only elements of the jQuery object that also match the selector are removed. This is useful for filtering which elements get removed.
- **`detach()`** — Works like `remove()` but **does not remove event handlers and data**. `detach()` may be more useful when you want to **temporarily remove** elements from the document for later reinsertion, preserving their behavior.
- **`unwrap()`** — Performs element removal in a way that is the **opposite** of the `wrap()` or `wrapAll()` method: it removes the **parent element** of each selected element without affecting the selected elements or their siblings. That is, for each selected element, it replaces the parent of that element with its children.

---

## 4. Handling Events with jQuery

### 4.1 Simple Event Handler Registration

jQuery defines simple event-registration methods for each of the commonly used and universally implemented browser events. To register an event handler for `click` events, for example, just call the **`click()`** method:

```javascript
$("p").click(function() {
  $(this).css("background-color", "gray");
});
```

In this example, only the `<p>` element being clicked is changed to gray (thanks to `$(this)` referring to the specific element that triggered the event). Calling a jQuery event-registration method registers your handler on **all of the selected elements** at once. This is typically much easier than one-at-a-time event handler registration with `addEventListener()`.

### 4.2 Event Handler Registration Methods

jQuery provides event-registration methods for all commonly used browser events:

| Method | Method | Method |
|--------|--------|--------|
| `blur()` | `mousedown()` | `keydown()` |
| `change()` | `mouseenter()` | `keypress()` |
| `click()` | `mouseleave()` | `keyup()` |
| `dblclick()` | `mousemove()` | `load()` |
| `focus()` | `mouseout()` | `resize()` |
| `focusin()` | `mouseover()` | `scroll()` |
| `focusout()` | `mouseup()` | `select()` |
| `error()` | | `submit()` |
| | | `unload()` |

Each of these methods can be called on a jQuery selection to register a handler for that event type on all matched elements.

### 4.3 The `bind()` Method

The **`bind()`** method binds a handler for a named event type to each of the elements in the jQuery object. Using `bind()` allows you to use more advanced event registration features than the simple event methods. `bind()` expects an **event type string** as its first argument and an **event handler function** as its second:

```javascript
// These two are equivalent:
$("p").click(f);
$("p").bind("click", f);
```

If the first argument is a **space-separated list of event types**, then the handler function will be registered for **each** of the named event types:

```javascript
// These two are equivalent:
$("a").hover(f);
$("a").bind("mouseenter mouseleave", f);
```

This ability to bind a single handler to multiple event types in one call makes `bind()` more flexible and concise than registering separate handlers for each event.

### 4.4 Deregistering Event Handlers

After registering an event handler with `bind()` (or with any of the simpler event registration methods), you can deregister it with **`unbind()`**. Important notes:

- `unbind()` only deregisters event handlers registered with `bind()` and related jQuery methods — **not** with `addEventListener()`.
- With **no arguments**, `unbind()` deregisters **all event handlers** (for each event, for each element):

  ```javascript
  $("*").unbind();
  ```

- With **string arguments**, all handlers for the named event type(s) are unbound from all elements in the jQuery object:

  ```javascript
  $("a").unbind("mouseover mouseout");
  ```

This provides a convenient way to clean up event handlers when they are no longer needed, which is important for preventing memory leaks in long-running web applications.

---

## 5. AJAX with jQuery

### 5.1 AJAX and jQuery

jQuery provides several methods for **AJAX functionality**. With these methods, it is possible to request text, HTML, XML, or JSON from remote servers using both HTTP **GET** and **POST** requests. Writing regular AJAX code can be tricky because different browsers have different syntax for AJAX implementation, which may necessitate writing extra code to test for different browsers. **jQuery takes care of this** by abstracting away the browser differences, providing a unified API that works consistently across all major browsers.

### 5.2 The `jQuery.ajax()` Function

The **`jQuery.ajax()`** function performs asynchronous HTTP requests. It underlies all Ajax requests sent by jQuery and is the most configurable option. It is often unnecessary to directly call this function, as several higher-level alternatives are available (such as `$.get()`, `$.post()`, `$.load()`, etc.).

`ajax()` accepts a single argument: an **options object** whose properties specify the details about how the AJAX request is to be performed. By default, data passed in to the `data` option as an object will be processed and transformed into a query string, fitting the default content-type `"application/x-www-form-urlencoded"`.

```javascript
$.ajax({
  method: "POST",
  url: "some.jsp",
  data: { name: "John", location: "Boston" }
})
.done(function(msg) {
  alert("Data Saved: " + msg);
});
```

The `.done()` method specifies a callback function that will be executed when the request succeeds, providing a clean and readable way to handle asynchronous responses.

### 5.3 `jQuery.get()`

**`jQuery.get()`** loads data from the server using an HTTP **GET** request. GET is basically used for getting data from a server and may also return cached data.

```javascript
$.get(URL, callback);
```

- The required **URL** parameter specifies the URL to request.
- The optional **callback** parameter is the name of a function to be executed if the request succeeds. The callback has two parameters: the **content** of the page requested, and the **status** of the request.

```javascript
$.get("test.jsp", { name: "John", time: "2pm" })
.done(function(data, status) {
  alert("Data Loaded: " + data + "\nStatus: " + status);
});
```

This is the simplest way to fetch data from a server when you don't need to send large amounts of data or when the request has no side effects on the server.

### 5.4 `jQuery.post()`

**`jQuery.post()`** loads data from the server using an HTTP **POST** request. POST is typically used when you need to send data to the server that modifies state or when the data payload is too large for a GET request.

```javascript
$.post(URL, data, callback);
```

- **URL** specifies the URL to request.
- The optional **data** parameter specifies some data to send along with the request.
- The optional **callback** parameter is the name of a function to be executed if the request succeeds.

```javascript
$.post("test.jsp", { name: "John", time: "2pm" })
.done(function(data) {
  alert("Data Loaded: " + data);
});
```

### 5.5 `jQuery.getScript()`

**`jQuery.getScript()`** loads a JavaScript file from the server using a GET HTTP request, then **executes it**. This is useful for dynamically loading scripts only when they are needed, rather than including them all in the initial page load.

```javascript
$.getScript("ajax/test.js", function(data, textStatus, jqxhr) {
  console.log(data);            // Data returned
  console.log(textStatus);      // Success
  console.log(jqxhr.status);    // 200
  console.log("Load was performed.");
});
```

The callback receives three arguments: the script content, the status text, and the jqXHR object, providing full information about the request result.

### 5.6 `jQuery.getJSON()`

**`jQuery.getJSON()`** loads JSON-encoded data from the server using a GET HTTP request. This is particularly useful for working with APIs that return JSON data, as jQuery automatically parses the JSON response into a JavaScript object.

```javascript
$.getJSON("ajax/test.json", function(data) {
  var items = [];
  $.each(data, function(key, val) {
    items.push("<li id='" + key + "'>" + val + "</li>");
  });
  $("<ul/>", {
    "class": "my-new-list",
    html: items.join("")
  }).appendTo("body");
});
```

In this example, the JSON data is iterated over using `$.each()`, list items are created from the data, and then a new `<ul>` element is constructed and appended to the body — all in a concise, readable manner.

### 5.7 The `load()` Method

**`load()`** is a simple but powerful AJAX method. It loads data from a server and **puts the returned content directly into the selected element(s)**. This makes it the most convenient method for simple AJAX operations where you want to update part of a page with server content.

```javascript
$(selector).load(URL, data, callback);
```

- **URL** — Specifies the URL you want to load.
- **selector** — Specifies the elements where the returned data will be loaded.
- **data** (optional) — A set of query-string key/value pairs to send along with the request.
- **callback** (optional) — A function to be executed after the `load()` method completes and the data are returned.

**Loading content into an element:**
```javascript
$("#result").load("ajax/test.html");
```

**Loading a fragment of a document** (only the content matching the selector is inserted):
```javascript
$("#result").load("ajax/test.html #container");
```

**Sending data with the request** (POST is used if data is provided as an object; otherwise, GET is assumed):
```javascript
$("#address").load("address.jsp", { zipcode: "02134", country: "IT" });
```

### 5.8 Load Examples: Loading Text into a Div

The lecture provides a step-by-step example of using the `load()` method:

**Step 1 — Basic load:** An anonymous function using the jQuery `load` method is attached as a callback of the `click` event on a button element. It loads the content of `demo_test.txt` into the element with id `div1`.

**Step 2 — Result after click:** After the click, the content of `div1` is replaced. In the example, it is HTML that is directly injected into the page.

**Step 3 — Loading a fragment:** It is possible to add a jQuery selector to the URL parameter to specify only the part of the document to insert. For example, only the text contained in the paragraph of id `p1` of the file `demo_test.txt` is inserted:
```javascript
$("#div1").load("demo_test.txt #p1");
```

**Step 4 — Using the callback:** The optional callback parameter specifies a function to run when the `load()` method is completed. This function can have different parameters:
- **`responseTxt`** — Contains the resulting content if the call succeeds.
- **`statusTxt`** — Contains the status of the call.
- **`xhr`** — Contains the `XMLHttpRequest` object.

**Step 5 — Complete flow:** User clicks the button → the callback function is invoked when the data returns → the information is loaded into the page.

These examples were taken from: [W3Schools jQuery AJAX Load](https://www.w3schools.com/jquery/jquery_ajax_load.asp)
