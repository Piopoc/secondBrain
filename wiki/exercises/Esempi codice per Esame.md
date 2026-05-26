# Esempi codice Servlet
## Login (get)
```java
@WebServlet("/login") 
public class LoginServlet extends HttpServlet {
	 @Override protected void doGet(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException { 
		 response.setContentType("text/html");
		 PrintWriter out = response.getWriter(); 
		 out.println("<html><body>"); 
		 out.println("<h1>Login Sistema</h1>"); 
		 out.println("<form method='POST' action='/login'>"); 
		 out.println("Username: <input type='text' name='username' required><br>");
		 out.println("Password: <input type='password' name='password' required><br>");
		 out.println("<input type='submit' value='Login'>");
         out.println("</form>");
         out.println("</body></html>");
	} 
}
```
## Login con thread-safe (post)
```java
@WebServlet("/login") 
public class LoginServlet extends HttpServlet {
	// Thread-safe storage degli utenti (simulazione database) 
	private final Map users = new ConcurrentHashMap<>(); 
	 
	@Override public void init() throws ServletException { 
	// Inizializzazione utenti di test 
		 users.put("admin", "password123");
		 users.put("user", "user123"); 
	} 
	 @Override protected void doPost(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException { 
		 String username = request.getParameter("username"); 
		 String password = request.getParameter("password");
		 // Validazione thread-safe
		 if (users.containsKey(username) && users.get(username).equals(password)) { 
			 // Login successful 
			 HttpSession session = request.getSession(); 
			 session.setAttribute("username", username); 
			 session.setAttribute("loginTime", System.currentTimeMillis()); 
			 response.sendRedirect("welcome"); 
		 } else {
			 // Login failed 
			 response.setContentType("text/html"); 
			 PrintWriter out = response.getWriter(); 
			 out.println("<html><body>"); 
			 out.println("<h1>Login Fallito</h1>"); 
			 out.println("<p>Credenziali non valide.</p>"); 
			 out.println("<a href='login'>Tenta di nuovo</a>");
			 out.println("</body></html>");
		}
	} 
}
```
## Welcome page
```Java
@WebServlet("/welcome") 
public class WelcomeServlet extends HttpServlet { 

	@Override protected void doGet(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException { 
		HttpSession session = request.getSession(false); 
		if (session != null && session.getAttribute("username") != null) { 
			// Utente autenticato 
			String username = (String) session.getAttribute("username"); 
			long loginTime = (Long) session.getAttribute("loginTime"); 
			response.setContentType("text/html"); 
			PrintWriter out = response.getWriter(); 
			out.println("<html><body>");
			out.println("<h1>Benvenuto, " + username + "!</h1>"); 
			out.println("<p>Login effettuato il: " + new Date(loginTime) + "</p>"); 
			out.println("<a href='logout'>Logout</a>");
			out.println("</html></body>"); 
		} else { 
		// Sessione non valida o scaduta 
		response.sendRedirect("login"); 
		} 
	} 
}
```
## Logout
```java
@WebServlet("/logout")
public class LogoutServlet extends HttpServlet {
    
    @Override
    protected void doGet(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
        HttpSession session = request.getSession(false);
        if (session != null) {
            // Invalida completamente la sessione
            session.invalidate();
        }
        // Reindirizza alla pagina di login
        response.sendRedirect("login");
    }
}
```
# Esempi codice DAO pattern
## Java Beans Immutable
```java
import java.util.Date;
import java.util.Objects;

public final class Customer {
    // Campi final per immutabilità
    private final int id;
    private final String name;
    private final String email;
    private final Date registrationDate;
    
    // Costruttore completo
    public Customer(int id, String name, String email, Date registrationDate) {
        this.id = id;
        this.name = name;
        this.email = email;
        this.registrationDate = registrationDate;
    }
    
    // Solo getter methods
    public int getId() { return id; }
    public String getName() { return name; }
    public String getEmail() { return email; }
    public Date getRegistrationDate() { return registrationDate; }
    
    // Override di metodi Object
    @Override
    public boolean equals(Object o) {
        // Implementazione completa
    }
    
    @Override
    public int hashCode() {
        // Implementazione completa
    }
    
    @Override
    public String toString() {
        // Implementazione completa
    }
}
```
## Interface DAO
```java
import com.example.model.Customer;
import java.util.List;
public interface CustomerDAO {
    void create(Customer customer) throws Exception;
    Customer findById(int id) throws Exception;
    List<Customer> findAll() throws Exception;
    void update(Customer customer) throws Exception;
    void delete(int id) throws Exception;
    List<Customer> findByEmail(String email) throws Exception;
}
```
## DAO implementation
```java
import com.example.model.Customer;
import java.sql.*;
import java.util.ArrayList;
import java.util.List;
public class CustomerDAOImpl implements CustomerDAO {
    private Connection connection;
    public CustomerDAOImpl(Connection connection) {
        this.connection = connection;
    }
    @Override
    public void create(Customer customer) throws Exception {
        String sql = "INSERT INTO customers (name, email, registration_date) VALUES (?, ?, ?)";   
        try (PreparedStatement statement = connection.prepareStatement(sql, Statement.RETURN_GENERATED_KEYS)) {
            // Set parameters safely using PreparedStatement
            statement.setString(1, customer.getName());
            statement.setString(2, customer.getEmail());
            statement.setDate(3, new java.sql.Date(customer.getRegistrationDate().getTime()));
            // Execute update
            int affectedRows = statement.executeUpdate();
			if (statement != null) statement.close();
        }
    }   
    // Altri metodi dell'interfaccia...
}
```
# 


![[Pasted image 20260525145133.png]]

---

![[Pasted image 20260525150206.png]]
- differenza tra forward e redirect è che quest'ultima cambia URL mentre il primo no

# Esempi codice jQuery
## Selezione e manipolazione DOM
Questi esempi mostrano come selezionare elementi HTML usando i selettori jQuery e manipolare le loro proprietà, contenuti, classi e visibilità.
```javascript
$(document).ready(function() {
    // Seleziona tutti i paragrafi e cambia il colore
    $("p").css("color", "blue");
    
    // Seleziona l'elemento con id="header" e cambia il testo
    $("#header").text("Benvenuto nel sito!");
    
    // Aggiunge una classe a tutti gli elementi con classe="highlight"
    $(".highlight").addClass("important");
    
    // Nasconde tutti gli elementi con classe="hidden"
    $(".hidden").hide();
    
    // Mostra l'elemento con id="menu" con un effetto fade
    $("#menu").fadeIn(1000);
});
```

## Gestione eventi
Questi esempi mostrano come gestire gli eventi degli elementi HTML usando jQuery, come click su pulsanti, cambi di selezione in dropdown e invio di form con validazione.
```javascript
$(document).ready(function() {
    // Gestisce il click su un pulsante
    $("#submitBtn").click(function() {
        alert("Pulsante cliccato!");
        // Previene il comportamento di default del form
        return false;
    });
    
    // Gestisce il cambio di selezione in un dropdown
    $("#countrySelect").change(function() {
        var selectedCountry = $(this).val();
        $("#selectedCountry").text("Hai selezionato: " + selectedCountry);
    });
    
    // Gestisce l'invio di un form con validazione
    $("#loginForm").submit(function(event) {
        var username = $("#username").val();
        var password = $("#password").val();
        
        if (username === "" || password === "") {
            alert("Per favore compilare tutti i campi");
            event.preventDefault(); // Blocca l'invio del form
            return false;
        }
        // Se la validazione passa, il form viene inviato normalmente
    });
});
```

## AJAX e chiamata al server
Questi esempi mostrano come effettuare chiamate asincrone al server usando jQuery Ajax per caricare o inviare dati senza ricaricare la pagina, includendo esempi di richieste GET e POST.
```javascript
$(document).ready(function() {
    // Carica dati dal server senza ricaricare la pagina
    $("#loadDataBtn").click(function() {
        $.ajax({
            url: '/api/getUserData',
            type: 'GET',
            dataType: 'json',
            success: function(response) {
                $("#userInfo").html("<p>Nome: " + response.name + "</p>" +
                                   "<p>Email: " + response.email + "</p>");
                $("#userInfo").fadeIn();
            },
            error: function(xhr, status, error) {
                $("#userInfo").html("<p>Errore nel caricamento dei dati</p>").css("color", "red");
            }
        });
    });
    
    // Invio dati al server tramite POST
    $("#registerForm").submit(function() {
        var userData = {
            name: $("#name").val(),
            email: $("#email").val(),
            password: $("#password").val()
        };
        
        $.post('/api/register', userData, function(response) {
            if (response.success) {
                $("#message").html("<p>Registrazione completata!</p>").css("color", "green");
                $("#registerForm")[0].reset(); // Reset del form
            } else {
                $("#message").html("<p>Errore: " + response.message + "</p>").css("color", "red");
            }
        }, 'json');
        
        return false; // Previene l'invio tradizionale del form
    });
});

/* Esempio di chiamata GET semplice */
$.get("/api/products", function(data) {
    $("#productList").empty();
    $.each(data, function(index, product) {
        $("#productList").append("<li>" + product.name + " - $" + product.price + "</li>");
    });
});
```

## Effetti e animazioni
Questi esempi mostrano come creare effetti visivi e animazioni usando jQuery, inclusi slide, fade e animazioni personalizzate di proprietà CSS.
```javascript
$(document).ready(function() {
    // Mostra/nasconde con effetto slide
    $("#toggleBtn").click(function() {
        $("#panel").slideToggle("slow");
        // Cambia il testo del pulsante in base allo stato
        if ($("#panel").is(":visible")) {
            $(this).text("Nascondi pannello");
        } else {
            $(this).text("Mostra pannello");
        }
    });
    
    // Animazione personalizzata
    $("#animateBtn").click(function() {
        $("#box").animate({
            left: '250px',
            opacity: '0.5',
            height: '150px',
            width: '150px'
        }, 2000);
    });
    
    // Effetto fade in/out
    $("#fadeInBtn").click(function() {
        $("#fadeElement").fadeIn(2000);
    });
    
    $("#fadeOutBtn").click(function() {
        $("#fadeElement").fadeOut(2000);
    });
});
```

## Utilità e metodi comuni
Questi esempi mostrano metodi utili di jQuery per eseguire operazioni comuni sugli elementi DOM, come iterazione, filtraggio, aggiunta, clonazione e rimozione di elementi.
```javascript
$(document).ready(function() {
    // Iterazione su elementi
    $("li.item").each(function(index) {
        $(this).text("Elemento " + (index + 1) + ": " + $(this).text());
    });
    
    // Filtraggio elementi
    $("input[type='text']").filter(function() {
        return $(this).val().length < 3;
    }).css("border", "2px solid red");
    
    // Aggiunta di elementi dinamicamente
    $("#addItemBtn").click(function() {
        var newItem = $("<li>").text("Nuovo elemento " + ($("#itemList li").length + 1));
        $("#itemList").append(newItem);
    });
    
    // Clonazione di elementi
    $("#cloneBtn").click(function() {
        var cloned = $("#original").clone();
        cloned.attr("id", "cloned_" + Date.now()); // Cambia l'ID per evitare duplicati
        $("#container").append(cloned);
    });
    
    // Rimozione di elementi
    $(".removeItem").click(function() {
        $(this).parent().remove(); // Rimuove l'elemento genitore (li)
    });
});
```