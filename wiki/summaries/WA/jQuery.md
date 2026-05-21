# jQuery — Web Applications Summary

## 🧠 Concepts & Entities
- **jQuery Object**: Array-like object returned by `$()`. Properties: `length`, `selector`, `context`, and `jquery`. The `.jquery` property is specifically used to distinguish jQuery objects from other array-like objects.
- **Method Chaining**: Implementation of the "write less, do more" philosophy. Allows calling multiple methods in one statement (e.g., `$("p").css("color", "red").show()`) because setter methods return the original jQuery object.
- **Implicit Iteration**: Core design principle where methods automatically apply to all matched elements. This eliminates the need for explicit loops, although the `.each()` method is available for manual iteration.
- **Getters vs Setters**: Unified methods where the argument presence determines the role. **Getters** query only the *first* element of the set. **Setters** apply changes to *all* elements and return the object for chaining.
- **DOM Manipulation**: Process of altering the HTML structure. By default, inserting an existing element *moves* it; to duplicate it, `.clone()` must be used for a deep copy (element and all descendants).
- **AJAX**: Asynchronous data requests (text, HTML, XML, JSON). jQuery provides a unified API that abstracts cross-browser inconsistencies, ensuring consistent behavior across all major browsers.

---

## ⚡ Cheat Sheet (Sintesi Operativa)

| Category | Method | Description | Example |
| :--- | :--- | :--- | :--- |
| **Selection** | `$()` | Selects elements via CSS selectors | `$("div.main")` |
| **Attributes** | `.attr()` | Get/Set HTML attributes | `$("a").attr("href", "url")` |
| **Styling** | `.css()` | Get/Set CSS properties | `$("h1").css("color", "blue")` |
| **Classes** | `.addClass()/.removeClass()/.toggleClass()` | Manage CSS classes | `$("div").toggleClass("active")` |
| **Forms** | `.val()` | Get/Set form field values | `$("#input").val("Hello")` |
| **Content** | `.text()` / `.html()` | Set/Get plain text or HTML | `$("p").text("New text")` |
| **Insertion** | `.append()` / `.prepend()` | Insert at end / start of target | `$("#log").append("<span>!</span>")` |
| **Insertion** | `.after()` / `.before()` | Insert after / before target | `$("h1").after("<hr/>")` |
| **Insertion** | `.replaceWith()` | Replace target with content | `$("hr").replaceWith("<br/>")` |
| **Copy/Wrap** | `.clone()` | Deep copy of element | `$(".item").clone().appendTo("body")` |
| **Copy/Wrap** | `.wrap()` / `.wrapInner()` / `.wrapAll()` | Wrap element/content/group | `$("h1").wrap("<i></i>")` |
| **Deletion** | `.empty()` / `.remove()` / `.detach()` | Clear children / Remove / Detach | `$(".old").remove()` |
| **Events** | `.click()`, `.blur()`, etc. | Simple event registration | `$("p").click(fn)` |
| **Events** | `.bind()` / `.unbind()` | Advanced event management | `$("a").bind("mouseenter", fn)` |
| **AJAX** | `$.ajax()` | Fully configurable HTTP request | `$.ajax({ method: "POST", ... })` |
| **AJAX** | `$.get()` / `$.post()` | Simple GET/POST requests | `$.get(url, callback)` |
| **AJAX** | `$.getJSON()` | Fetch and parse JSON data | `$.getJSON(url, callback)` |
| **AJAX** | `.load()` | Load HTML fragment into element | `$("#div").load("page.html #id")` |


---

## ✍️ Quiz di Autovalutazione

### Domande
1. **Differenza tra oggetto jQuery e array JS standard?**
2. **Cos'è il "Method Chaining" e perché è possibile?**
3. **Differenza tra `.text()` e `.html()`?**
4. **Differenza tra `.remove()` e `.detach()`?**
5. **Quando usare `$.post()` invece di `$.get()`?**
6. **Vantaggio di `.load()` rispetto a `$.ajax()` per aggiornamenti parziali?**

### Risposte
1. L'oggetto jQuery è "array-like" (ha `length` e indice), ma non è un vero array. Include `selector`, `context` e `jquery`.
2. Concatenazione di metodi in una riga; possibile perché i setter restituiscono l'oggetto jQuery.
3. `.text()`: testo semplice (safe XSS), aggrega tutti i match. `.html()`: markup HTML, restituisce solo il primo match.
4. `.remove()`: elimina elemento, eventi e dati. `.detach()`: rimuove l'elemento ma preserva eventi e dati.
5. Quando i dati superano il limite URL (GET) o l'operazione modifica lo stato del server.
6. Inserisce il contenuto *direttamente* nell'elemento selezionato, supportando selettori per frammenti specifici.
