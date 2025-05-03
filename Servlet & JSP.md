JSP (Jakarta Server Pages) allow you to write java code within an HTML page in the same way you write JavaScript embedded in HTML.
Jakarta Servlet is a java class that allows you to process http requests and responses, and send out responses as output.
Both are server-side technologies and work in tandem. JSP is compiled into a servlet.

# How to pass data between pages
1.  Hidden values within a form.
2.  URL (re)writing. 
>>Attach parameters to URLs in links on the page, e.g.
```java
<a href="another.jsp?mydata=<%=thedata>>Go!</a>
```
3. Cookies
4. server side (session)

# JSP Syntax

| Element             | Syntax                                    | Function                                              |
| ------------------- | ----------------------------------------- | ----------------------------------------------------- |
| JSP Expression      | <%= some Java expression %><br>           | Evaluates and displays the expression                 |
| JSP Scriptlet<br>   | <% some Java code: 1 to many lines %><br> | Goes into the service function portion of the servlet |
| JSP Declaration<br> | <%! variable or method declaration %><br> | Goes outside the service function (NOT Service)       |
| JSP Directive       | <%@ import="" %>                          | For imports, page info, contentType                   |
# JSP Directives Attributes Examples
## Page
language="scripting language" 
extends="className"
import="importList"
session="truelfalse" 
autoFlush="truelfalse"
contentType="ctinfo"
errorPage="error_url"
isErrorPage="truelfalse"
info="information"
isEl4gnored="truelfalse"
isThreadSafe="truelfalse" 
### Example:
`<@page language="java" import="java.util.*,java.sql.*" info="Contact page" extends="com.telusko.User" contextType="text/ html" isELIgnored="false" isThreadSafe="false" session="false" %>`

## Include

`<%@include file="header.jsp" %>`

## Taglib
used for external tags 
<% @ taglib uri="uri" prefix="fx" %> 

# JSP Implicit Objects
Builtin Object (can be used in Scriptlet and Expression) 
- request (HttServletRequest) 
- response (HttpServletResponse)
- pageContext (PageContext)
- out (JspWriter) ~ PrintWriter object
- session (HttpSession)
- application (ServletContext)
- config (ServletConfig) 
# Accessing parameters in JSP or Servlets
In JSP, HTML attributes "name" & "value" correspond to a key / value pair   
```java title:"JSP (implicit parameters)"
${param.accountID} // key = name attribute in the HTML tag
// cannot be used within java code and therefore cannot perform any manipulation on the strings. Used mostly to display the data.
```

```java title:Servlet
<%
    String accountId = request.getParameter("accountID");
%>
```

>[!NOTE] Accessing multiple values of a single key
> If a key (name attribute) has multiple values such as check-boxes, you can access them using the following approach:
>
> ```java
> String vehicle[] = request.getParameterValues("vehicle");
> for (String v : vehicle) {
>     out.print(v);
> }
> ```


# Building a page with fragments
```jsp title:"aggregating pages"
<jsp:include page="header.html"></jsp:include>
<jsp:include page="profile.jsp"></jsp:include>
<!-- or -->
<%@include file="header.jsp" %>
```


# Servlet Class
```java title:"Generic Servlet example"


@WebServlet("/UserController") // the annotation denotes the url that will trigger the class.
public class UserController extends HttpServlet {
	public UserController{
	}

	protected void doGet(HttpServletRequest request, HttpServlet response){
		response.getWriter().append("<h1>Hello Friend</h1>");
	}
}
```
```html title:"how to call the generic servlet"
<form action="UserController" method="GET"> 
</form>
```
>[!BUG] Relative and absolute URIs
>Using `/` before the filename in the `action` attribute in the form tag denotes that you are providing the absolute path not a relative path.

# Connecting DB
1. Create a resource in the context.xml _(webapp --> META-INF --> context.xml)_
2. Add driver class to _(webapp --> WEB-INF --> lib)_ folder
3. Modify the java build path (libraries) to include the path to JAR file of the driver class
```xml title:"connecting oracle DB"
<Context>
<!-- the name attribute will be used in the resource annotation
to create a data source.-->
  <Resource name="jdbc/web_item"  
            type="javax.sql.DataSource"
            username="hr"
            password="hr"
            driverClassName="oracle.jdbc.OracleDriver"
            url="jdbc:oracle:thin:@//localhost:1521/orclpdb"
            />

</Context>
```
```java title:"Accessing the database within a java class"

@WebServlet("/TestItem")
public class TestItem extends HttpServlet {
    @Resource(name = "jdbc/web_item")
    private DataSource dataSource;

    protected void doGet(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {

        PrintWriter printWriter = response.getWriter();

        try {

            Connection connection = dataSource.getConnection();
            Statement statement = connection.createStatement();
            String sql = "select * from item";
            ResultSet resultSet = statement.executeQuery(sql);
            
            while (resultSet.next()) {
                printWriter.print("<h1>" + resultSet.getString("id") + "</h1>");

                printWriter.print("<h1>" + resultSet.getString("name") + "</h1>");

                printWriter.print("<h1>" + resultSet.getString("price") + "</h1>");

                printWriter.print("<h1>" + resultSet.getString("total_number") + "</h1>");

            }

        } catch (SQLException e) {

            // TODO Auto-generated catch block

            System.out.println("----> " + e.getMessage());

        }
    }
}
```
>[!danger] Secure against SQL injection
>When executing a statement that involves user input, use `connection.prepareStatment()` in place of `connection.createStatement` to sanitize user input and secure the statement against SQL injections.

>[!info] Adding Driver Class
>You must add the driver JAR file to _webapp->WEB-INF->lib_ folder add it to the libraries in java build path (class path) as well.



# Sparse Notes
>[!note] Servlet context and servlet config
>In the file _web.xml_ in the folder _web-inf_  where servlet mappings are written. You can data that can be shared among multiple servlets (servlet context) which is referred to as context parameter tags. However if you want to include data that is specific to one servlet, you can use servlet config which is also referred to as init-param tags within the _web.xml_ file 


> [!warning] File extension in the `action` attribute in the form tag
> `.jsp` extension seems to be mandatory, if you're trying to access a jsp file.


