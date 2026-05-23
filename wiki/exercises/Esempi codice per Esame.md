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
			out.println(""); 
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
            if (affectedRows == 0) {
                throw new SQLException("Creating customer failed, no rows affected.");
            }
            // Get generated ID
            try (ResultSet generatedKeys = statement.getGeneratedKeys()) {
                if (generatedKeys.next()) {
                    // In real implementation, would return customer with ID
                    // For simplicity, just log the ID
                    System.out.println("Generated ID: " + generatedKeys.getInt(1));
                }
            }
        }
    }   
    // Altri metodi dell'interfaccia...
}
```
# 