# Form Validation and AJAX — Detailed Summary

> **Course:** Web Applications — Master Degree in Computer Engineering, Cybersecurity, and ICT for Internet and Multimedia
> **Academic Year:** 2025/2026
> **Author:** Nicola Ferro — University of Padua

---

## 1. Form Validation

### 1.1 Introduction to Form Validation

Form validation is the process by which a web application checks the data entered by a user before that data is submitted to the server. When the data is correct, the application allows it to be sent to the server and typically stored in a database; when the data is incorrect, the application displays an error message explaining what corrections need to be made. Form validation is a critical aspect of web development because it ensures data integrity, improves user experience, and protects both the user and the application from various risks.

There are three main reasons to validate forms:

1. **To get the right data, in the right format:** Web applications will not function properly if user data is stored in the wrong format, if users enter incorrect information, or if they omit required information altogether. For example, a phone number field that accepts free-form text may end up containing alphabetic characters, rendering the data useless for automated calling or SMS systems.

2. **To protect users' accounts:** By forcing users to choose secure passwords — combining uppercase and lowercase letters, numbers, and special characters — applications reduce the risk of accounts being compromised through brute-force or dictionary attacks.

3. **To protect the application itself:** Unprotected forms can be exploited by malicious users to damage the application through techniques such as SQL injection, cross-site scripting (XSS), or other injection attacks. Validation acts as a first line of defense against these threats.

### 1.2 Different Types of Form Validation

There are two fundamentally different types of form validation, each serving a distinct role in the data submission pipeline:

#### Client-Side Validation

Client-side validation occurs in the browser, before the data has been submitted to the server. This approach is more user-friendly because it provides instant feedback to the user without the round-trip delay of a server request. Client-side validation can be further subdivided into two categories:

- **JavaScript validation:** This is coded using JavaScript and is completely customizable. Developers can define their own validation logic, create custom error messages, and apply any rules they deem necessary. The downside is that it requires more development effort and may be bypassed if the user disables JavaScript in their browser.

- **Built-in form validation (HTML5):** HTML5 introduced native form validation features through validation attributes on form elements. This approach has better performance because it leverages the browser's built-in functionality and does not require any JavaScript code. However, it is not as customizable as JavaScript validation; the error messages and styling options are limited to what the browser provides.

#### Server-Side Validation

Server-side validation occurs on the server after the data has been submitted. It is used to validate the data before it is saved into the database. If the data fails validation, a response is sent back to the client informing the user what corrections need to be made. Server-side validation is not as user-friendly as client-side validation because it does not provide errors until the entire form has been submitted and the page reloads (or a new response is rendered). However, server-side validation is the application's last line of defense against incorrect or malicious data. Even if client-side validation is bypassed (e.g., by disabling JavaScript or by crafting a custom HTTP request), the server must still validate all incoming data.

In practice, developers use a **combination** of both client-side and server-side validation. Client-side validation provides immediate, user-friendly feedback, while server-side validation ensures data integrity and security regardless of what happens on the client.

### 1.3 HTML5 Form Validation

One of the key features of HTML5 is the ability to validate most user data without relying on scripts. This is achieved by using **validation attributes** on form elements, which allow developers to specify rules for each form input. If the entered data follows all the specified rules, it is considered **valid**; if not, it is considered **invalid**.

When an element is valid:
- The element matches the `:valid` CSS pseudo-class, which allows developers to apply a specific visual style to valid elements (e.g., a green border).
- If the user tries to submit the data, the browser will submit the form, provided there is nothing else preventing it from doing so (e.g., JavaScript calling `preventDefault()`).

When an element is invalid:
- The element matches the `:invalid` CSS pseudo-class, which allows developers to apply a specific visual style to invalid elements (e.g., a red dashed border).
- If the user tries to submit the data, the browser will **block** the form submission and display an error message.

Common HTML5 validation attributes include `required`, `pattern`, `min`, `max`, `minlength`, `maxlength`, and `type` (e.g., `type="email"` or `type="url"`). These attributes declaratively define the constraints that the input must satisfy.

### 1.4 Basic HTML5 Form Validation Example

The following example demonstrates a simple form using HTML5 validation. A text input requires the user to enter either "Informatics", "ICT", or "Cybersecurity", enforced through the `required` and `pattern` attributes:

```html
<!DOCTYPE html>
<html>
<head>
  <meta charset="utf-8">
  <title>Form Example</title>
  <link rel="stylesheet" type="text/css" href="css/basic-html5-validation.css">
</head>
<body>
  <form>
    <label for="choose">In which course are you enrolled? Informatics or ICT?</label>
    <input id="choose" name="course" required pattern="Informatics|ICT|Cybersecurity">
    <button>Submit</button>
  </form>
</body>
</html>
```

The accompanying CSS uses the `:invalid` and `:valid` pseudo-classes to provide visual feedback:

```css
input:invalid {
  border: 2px dashed red;
}
input:valid {
  border: 2px solid black;
}
```

When the input is empty or does not match the pattern, the border turns red and dashed; when the input matches one of the allowed values, the border becomes solid black.

### 1.5 Customized Error Messages

HTML5 provides the **Constraint Validation API** to check and customize the state of a form element. Among its features, it is possible to change the text of the error message using the `setCustomValidity()` method. This is useful when the default browser error messages are too generic or when developers want to provide more specific guidance to the user.

Example:

```javascript
var email = document.getElementById("provide_email");
email.addEventListener("input", function (event) {
  if (email.validity.typeMismatch) {
    email.setCustomValidity("Please insert an email address!");
  } else {
    email.setCustomValidity("");
  }
});
```

In this code, the `input` event listener checks whether the email field has a `typeMismatch` validity state (i.e., the entered value does not conform to the expected email format). If there is a mismatch, a custom error message is set; otherwise, the custom validity is cleared by passing an empty string.

### 1.6 Validating Forms without a Built-in API

When HTML5 built-in validation is not sufficient or not available, developers must implement custom validation logic using JavaScript. To validate a form without a built-in API, several questions need to be addressed:

1. **What kind of validation should I perform?** Developers must determine how to validate the data: string operations, type conversion, regular expressions, etc. It is important to remember that form data is always text and is always provided to scripts as strings, even if the input type is `number` or `date`.

2. **What should I do if the form does not validate?** Developers need to decide how the form will behave when validation fails: should the fields in error be highlighted? Should error messages be displayed? Should the form scroll to the first error? These decisions significantly impact user experience.

3. **How can I help the user to correct invalid data?** To reduce user frustration, it is crucial to provide as much helpful information as possible to guide users in correcting their inputs. This includes offering up-front suggestions so users know what is expected (e.g., placeholder text, format hints), as well as clear, specific error messages when something goes wrong.

### 1.7 Validating Forms with Plain JavaScript

The following example demonstrates how to validate an email field using plain JavaScript with a regular expression. The HTML structure includes a label, an input, and a span element for displaying errors:

```html
<div>
  <label for="provide_email">What is your e-mail?</label>
  <input type="text" id="provide_email" name="email">
  <span class="error"></span>
</div>
```

The JavaScript code first retrieves references to the relevant DOM elements and defines a regular expression for validating email addresses:

```javascript
var form = document.getElementsByTagName("form")[0];
var email = document.getElementById("provide_email");
var error = email.nextElementSibling;
var emailRegExp = /^[a-zA-Z0-9.!#$%&'*+/=?^_`{|}~-]+@[a-zA-Z0-9-]+(?:\.[a-zA-Z0-9-]+)*$/;
```

The `input` event listener provides real-time feedback as the user types:

```javascript
email.addEventListener("input", function () {
  var test = email.value.length === 0 || emailRegExp.test(email.value);
  if (test) {
    email.className = "valid";
    error.innerHTML = "";
  } else {
    email.className = "invalid";
    error.innerHTML = "Please insert an e-mail address";
    error.className = "error";
  }
});
```

The `submit` event listener performs the final validation before the form is submitted. If validation fails, `event.preventDefault()` is called to block the form submission:

```javascript
form.addEventListener("submit", function (event) {
  var test = email.value.length === 0 || emailRegExp.test(email.value);
  if (test) {
    email.className = "valid";
    error.innerHTML = "";
  } else {
    email.className = "invalid";
    error.innerHTML = "I expect an e-mail!";
    error.className = "error active";
    event.preventDefault();
  }
});
```

This approach provides both real-time feedback (on `input`) and a final check (on `submit`), ensuring that invalid data never reaches the server.

---

## 2. AJAX — Scripted HTTP

### 2.1 Introduction to AJAX

Historically, **AJAX** stands for **Asynchronous JavaScript And XML**, an acronym reflecting the technologies used at the time of its inception (JavaScript and XML). Today, AJAX refers to a broader group of technologies that offer asynchronous functionality in the browser. The key feature of an AJAX application is that it uses **scripted HTTP** to initiate data exchange with a web server **without causing pages to reload**.

AJAX uses the `XMLHttpRequest` object to communicate with servers. It can send and receive information in various formats, including JSON, XML, HTML, and plain text files. The most appealing characteristic of AJAX is its **asynchronous** nature, meaning it can communicate with the server, exchange data, and update the page without having to refresh the entire page. This ability to avoid page reloads results in **responsive web applications** that feel more like desktop applications.

A web application might use AJAX technologies to log user interaction data to the server silently, or to improve its start-up time by displaying only a simple page at first and then downloading additional data and page components on an as-needed basis.

### 2.2 AJAX Examples

AJAX is used extensively across the modern web, often without users even realizing it. Some common examples include:

- **Live search (autocomplete):** When you type into the search bar of a website, results often appear before you have finished typing. Google's search suggestions are a classic example — as you type each character, AJAX requests are sent to the server to retrieve matching search terms.

- **Social media integrations:** Websites with user-generated content (Twitter, Facebook, etc.) allow you to display information (e.g., the latest photograph) on your own page. This involves collecting data from their servers via AJAX without reloading your page.

- **Shopping carts:** When you are shopping online and add items to your cart, the cart is updated without you leaving the page, and the site may display a confirmation message. The server is notified of the change via an AJAX request.

- **Username availability check:** When you are registering on a website, a script may check whether your chosen username is already taken before you have completed the rest of the form, providing instant feedback.

### 2.3 Synchronous vs Asynchronous Processing

Understanding the difference between synchronous and asynchronous processing is fundamental to grasping the value of AJAX:

- **Synchronous processing:** When a browser encounters a `<script>` tag, it typically stops processing the rest of the page until it has loaded and processed the script. This is the traditional synchronous processing model. This can cause significant delays, especially if the script requires data from the server — the user must then wait for the server to respond before anything else can happen.

- **Asynchronous processing (AJAX):** AJAX uses an asynchronous (non-blocking) processing model. The user can continue interacting with the page while the browser is waiting for data to load. When the server responds with the data, an event is fired, which calls a function that processes the data. This function can update only a specific element of the page instead of requiring the entire page to reload. This results in a much faster, more responsive user experience.

### 2.4 Using XMLHttpRequest

Browsers define their HTTP API on the `XMLHttpRequest` class. Each instance of this class represents a single request/response pair, and the properties and methods of the object allow you to specify request details and extract response data.

```javascript
var request = new XMLHttpRequest();
```

An HTTP request consists of **four parts**:
1. The HTTP request method (e.g., GET, POST, PUT, DELETE).
2. The URL being requested.
3. An optional set of request headers, which may include authentication information.
4. An optional request body (used with POST and PUT requests).

The HTTP response sent by a server has **three parts**:
1. A numeric and textual status code that indicates the success or failure of the request (e.g., 200 for OK, 404 for Not Found).
2. A set of response headers.
3. The response body.

### 2.5 Specifying the Request

After creating an `XMLHttpRequest` object, the next step is to call the `open()` method to configure the request:

```javascript
request.open('GET', 'http://www.example.org/some.file');
```

- **First parameter:** The HTTP request method. It should be written in all-capital letters as per the HTTP standard; otherwise, some browsers might not process the request correctly.

- **Second parameter:** The URL that is the subject of the request. This is relative to the URL of the document that contains the script calling `open()`. As a security feature, you **cannot** call URLs on third-party domains (same-origin policy). You must use the exact domain name on all of your pages, or you will get a "permission denied" error.

To set request headers, the `setRequestHeader()` method is used. For example, POST requests typically need a `Content-Type` header to specify the MIME type of the request body:

```javascript
request.setRequestHeader("Content-Type", "text/plain");
```

If `setRequestHeader()` is called multiple times for the same header, the new value does **not** replace the previously specified value; instead, the HTTP request will include multiple copies of the header, or the header will specify multiple values.

The final step is to send the request to the server using the `send()` method:

```javascript
request.send();
```

### 2.6 Encoding the Request Body

HTTP POST requests include a request body that contains data the client is passing to the server. There are two common encoding formats:

#### Form-Encoded Requests

This is the traditional format for submitting form data. It uses URI encoding (replacing special characters with hexadecimal escape codes) on the name and value of each form element, separates the encoded name and value with an equals sign, and separates name/value pairs with ampersands:

```
find=pizza&zipcode=02134&radius=1km
```

The formal MIME type for this encoding is:

```
application/x-www-form-urlencoded
```

#### JSON-Encoded Requests

For more structured or complex data, JSON encoding is often preferred:

```javascript
request.setRequestHeader("Content-Type", "application/json");
```

JSON is more concise than form encoding for nested or complex data structures and has become the de facto standard for modern web APIs.

### 2.7 Cross-Origin Resource Sharing (CORS)

The `XMLHttpRequest` object can normally issue HTTP requests only to the server from which the document was downloaded, due to the **same-origin security policy**. This means browsers do not load AJAX responses from other domains. However, there are workarounds, and one of the most important is **CORS**.

**Cross-Origin Resource Sharing (CORS)** is a mechanism that uses additional HTTP headers to let a user agent gain permission to access selected resources from a server on a different origin (domain) than the site currently in use. A user agent makes a cross-origin HTTP request when it requests a resource from a different domain, protocol, or port than the one from which the current document originated.

For example, an HTML page served from `http://domain-a.com` might make an `<img>` src request for `http://domain-b.com/image.jpg`. The CORS standard works by adding new HTTP headers that allow servers to describe the set of origins that are permitted to read that information using a web browser.

Importantly, cross-origin requests do **not** normally include any user credentials: username and password, cookies, HTTP authentication tokens, etc. This restriction can be relaxed by the server through appropriate CORS headers, but it requires explicit configuration.

### 2.8 Retrieving the Response

The same `XMLHttpRequest` object that sent the request also handles the response. When you send the request, you should provide the name of a JavaScript function to handle the response:

```javascript
request.onload = nameOfTheFunction;
```

The function needs to check the request's state. The `readyState` property indicates the current state of the request:

| Value | State | Description |
|-------|-------|-------------|
| 0 | Uninitialized | `open()` has not been called yet |
| 1 | Loading | `open()` has been called |
| 2 | Loaded | Headers have been received |
| 3 | Interactive | The response body is being received |
| 4 | Complete | The response is complete (`XMLHttpRequest.DONE`) |

When `readyState` equals `XMLHttpRequest.DONE` (value 4), it means the full server response has been received and it is safe to process it.

Next, the HTTP status code should be checked (successful responses typically have status 200):

```javascript
request.status == 200
```

After verifying both the state and the status code, there are two options to access the response data:

- **`request.responseText`** — returns the server response as a string of text.
- **`request.responseXML`** — returns the response as an XML Document object that can be traversed using JavaScript DOM functions.

### 2.9 Complete XMLHttpRequest Example

The following example demonstrates a complete AJAX workflow using `XMLHttpRequest`:

```javascript
(function() {
  var httpRequest;
  document.getElementById('ajaxButton').addEventListener('click', makeRequest);

  function makeRequest() {
    httpRequest = new XMLHttpRequest();
    if (!httpRequest) {
      alert('Giving up :( Cannot create an XMLHTTP instance');
      return false;
    }
    httpRequest.onload = alertContents;
    httpRequest.open('GET', 'test.html');
    httpRequest.send();
  }

  function alertContents() {
    if (httpRequest.readyState === XMLHttpRequest.DONE) {
      if (httpRequest.status == 200) {
        alert(httpRequest.responseText);
      } else {
        alert('There was a problem with the request.');
      }
    }
  }
})();
```

In this example, clicking the button triggers `makeRequest()`, which creates a new `XMLHttpRequest`, sets up the `onload` handler, opens a GET request, and sends it. When the response is received, `alertContents()` checks whether the request is complete and successful, then displays the response text.

### 2.10 Types of Receivable Data

AJAX can receive data in several formats, each with its own advantages and disadvantages:

#### HTML

- **Pros:** Easy to write, request, and display. The data sent from the server can go straight into the page without processing it through JavaScript (e.g., by setting `innerHTML`).
- **Cons:** The server must produce the HTML in a format that is ready for use on the page. It is not well-suited for use in applications other than web browsers — there is no good data portability.

#### XML

- **Pros:** A flexible data format that can represent complex structures. It works well with different platforms and applications. It is processed using the same DOM methods used for HTML.
- **Cons:** It is considered a verbose language — the tags add a lot of extra characters to the data being sent. It can also require a lot of code to be processed and parsed.

#### JSON

- **Pros:** Can be called from any domain (CORS support). More concise than HTML and XML. Commonly used with JavaScript and has gained wide adoption across web applications. JSON objects map directly to JavaScript objects, making parsing trivial.
- **Cons:** The syntax is very strict (unlike HTML) — a missed quote, comma, or colon can break the entire file. Since it is still JavaScript, it can contain malicious content; therefore, JSON should only be used from trusted sources.

### 2.11 Loading JSON with AJAX

When the server sends JSON data to a web browser, it arrives as a **string**. When it reaches the browser, a script must convert the string into a JavaScript object — a process known as **deserialization** — through the `parse()` method of the `JSON` object. The `JSON` object is a global object, so there is no need to instantiate it.

```javascript
responseObject = JSON.parse(xhr.responseText);
```

Once the string has been parsed, the script can access the data in the resulting object and use it to create HTML dynamically. The HTML is typically added to the page using the `innerHTML` property. Because `innerHTML` can execute scripts embedded in the HTML, it should only be used when you are confident that the content does not contain malicious code.

The method `JSON.stringify()` performs the reverse operation — it converts JavaScript objects into a string using JSON notation. This is used to send data from the browser back to the server, a process known as **serialization**.

#### JSON Loading Example

```javascript
var xhr = new XMLHttpRequest();
xhr.onload = function() {
  if (xhr.status === 200) {
    responseObject = JSON.parse(xhr.responseText);
    var newContent = '';
    for (var i = 0; i < responseObject.events.length; i++) {
      newContent += '<div class="event">';
      newContent += '<img src="' + responseObject.events[i].map + '"';
      newContent += ' alt="' + responseObject.events[i].location + '"/>';
      newContent += '<p><b>' + responseObject.events[i].location + '</b><br>';
      newContent += responseObject.events[i].date + '</p>';
      newContent += '</div>';
    }
    document.getElementById('content').innerHTML = newContent;
  }
};
xhr.open('GET', 'data/data.json');
xhr.send();
```

The corresponding JSON data file (`data.json`) might look like:

```json
{
  "events": [
    {"location": "San Francisco, CA", "date": "May 1", "map": "img/map-ca.png"},
    ...
  ]
}
```

In this example, the AJAX request fetches a JSON file containing an array of events. Each event has a location, date, and map image. The script parses the JSON, iterates through the events array, builds HTML strings, and inserts them into the page.

### 2.12 The Fetch API

More recently, JavaScript has introduced a new way of sending requests to servers through the `fetch()` method. The Fetch API provides a more modern and powerful alternative to `XMLHttpRequest`, though it is not supported by older browsers, so care must be taken when using it in production.

**Basic syntax:**

```javascript
var promise = fetch(url, [options])
```

- **`url`**: The URL to be reached.
- **`options`**: Optional parameters such as method, headers, body, etc.

The JavaScript Fetch API is based on the use of a **Promise**, an object that encapsulates the result of an asynchronous operation. The key idea behind a Promise is that, when it resolves (i.e., when the answer is returned from the server), it becomes an object of type `Response`, which presents useful methods and properties.

Invoked without options, `fetch()` corresponds to a GET request that downloads the content of the URL. The process of obtaining an answer is typically performed in **two steps**:

1. Check the status (verify that everything went right with the server).
2. Work with the body of the answer.

Example:

```javascript
let response = await fetch(url);
if (response.ok) { // if HTTP-status is 200-299
  let json = await response.json(); // receive the body as JSON
} else {
  alert("HTTP-Error: " + response.status);
}
```

Here, `fetch` is used to GET information from a URL. The keyword `await` is used (in the context of Promise objects) to wait for the fulfilled value of the promise — in this case, the response from the server. The `response.json()` method parses the body of the response as JSON. This two-step approach (first check if the response is OK, then parse the body) is a clean and readable pattern that avoids many of the complexities of the traditional `XMLHttpRequest` approach.

---

## Further Readings

- **MDN Web Docs:** Resources for Developers, by Developers. [https://developer.mozilla.org/en-US/](https://developer.mozilla.org/en-US/)
- **Duckett, J., Ruppert, G., and Moore, J.** (2014). *JavaScript & jQuery: Interactive Front-end Web Development.* Wiley.
- **Flanagan, D.** (2011). *JavaScript: the Definitive Guide.* O'Reilly Media, Inc.
