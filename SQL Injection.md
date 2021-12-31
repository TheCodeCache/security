# SQL Injection — 

There could be flaws in our applications.  
SQL Injection flaws are introduced when software developers create dynamic database queries that include user supplied input.  
To avoid SQL injection flaws is simple.  
Developers need to either:  
a.) stop writing dynamic queries; and/or  
b.) prevent user supplied input which contains malicious SQL from affecting the logic of the executed query.  

# **`ATTACK`** —  

SQL-injection flaws typically look like this:  
The following (Java) example is `UNSAFE`,  
and would allow an attacker to inject code into the query that would be executed by the database.  

```java
String query = "SELECT account_balance FROM user_data WHERE user_name = "
             + request.getParameter("customerName");
try {
    Statement statement = connection.createStatement( ... );
    ResultSet results = statement.executeQuery( query );
}
...
```

# **`DEFENSE`** —  

Primary Defenses:  

Option 1: Use of Prepared Statements (with Parameterized Queries)  
Option 2: Use of Stored Procedures  
Option 3: Allow-list Input Validation  
Option 4: Escaping All User Supplied Input  

Additional Defenses:

Also: Enforcing Least Privilege
Also: Performing Allow-list Input Validation as a Secondary Defense

Option-1 :   
  **`Prepared statements`** ensure that an attacker is not able to change the intent of a query,  
  even if SQL commands are inserted by an attacker.  
  In the safe example below,  
  if an attacker were to enter the userID of `tom' or '1'='1`,  
  the parameterized query would not be vulnerable  
  and would instead look for a username which literally matched the entire string `tom' or '1'='1`.  


  Language specific recommendations:  
  1. **Java EE** – use PreparedStatement() with bind variables  
  2. **Hibernate** - use createQuery() with bind variables (called named parameters in Hibernate)  

  `Safe` Java Prepared Statement Example -  

```java
  // This should REALLY be validated too
  String custname = request.getParameter("customerName");
  // Perform input validation to detect attacks
  String query = "SELECT account_balance FROM user_data WHERE user_name = ? ";
  PreparedStatement pstmt = connection.prepareStatement( query );
  pstmt.setString( 1, custname);
  ResultSet results = pstmt.executeQuery( );
```

  Hibernate Query Language (HQL) Prepared Statement (Named Parameters) Examples:  

```java
  //First is an unsafe HQL Statement
  Query unsafeHQLQuery = session.createQuery("from Inventory where productID='"+userSuppliedParameter+"'");
  //Here is a safe version of the same query using named parameters
  Query safeHQLQuery = session.createQuery("from Inventory where productID=:productid");
  safeHQLQuery.setParameter("productid", userSuppliedParameter);
```


Option-2 :  

  Stored Procedures -  
  Stored procedures are not always safe from SQL injection.  
  However, certain standard stored procedure programming constructs have the same effect  
  as the use of parameterized queries when implemented safely which is the norm for most stored procedure languages.  

  `Safe` Java Stored Procedure Example:  
```java
  // This should REALLY be validated
  String custname = request.getParameter("customerName");
  try {
    CallableStatement cs = connection.prepareCall("{call sp_getAccountBalance(?)}");
    cs.setString(1, custname);
    ResultSet results = cs.executeQuery();
    // … result set handling
  } catch (SQLException se) {
    // … logging and error handling
  }
```

Option-3 :  
  Allow-list Input Validation -  

  Use regular expressions or switch-case statements to vlaidate the user supplied input.  
  For example:  if we use [a-z] as the regular expression validation for the customer-name column values,  
  then it will fail for this value : `' OR 1 = 1`

Option-4 :  
  Escaping All User-Supplied Input -  

  This technique should only be used as a last resort,  
  This technique is to escape user input before putting it in a query.  
  It is very database specific in its implementation.  

  This technique works like this -  
  Each DBMS supports one or more character escaping schemes specific to certain kinds of queries.  
  If we then escape all user supplied input using the proper escaping scheme for the database we are using,  
  the DBMS will not confuse that input with SQL code written by the developer,  
  thus avoiding any possible SQL injection vulnerabilities.  



**Reference:**  
1. https://cheatsheetseries.owasp.org/cheatsheets/SQL_Injection_Prevention_Cheat_Sheet.html

