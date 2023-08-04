# Registeration-Login-Form
Part 1: Frontend
A simple HTML form with the following fields:
1. Username (input field)
2. Email (input field)
3. Password (input field)
4. Confirm Password (input field)
5. Submit button
   
Validate the form inputs using PHP. The username, email, and password fields are not empty. The email field should be a valid email format, and the password and confirm password fields should match.

Part 2: Backend
A PHP script to process the form data submitted by the user.
1. Perform server-side valida=on to ensure all fields are filled out correctly and meet the requirements (e.g., non-empty fields, valid email, matching passwords).
2. If the valida=on fails, display appropriate error messages on the frontend, indica=ng what went wrong.
3. If the valida=on passes, store the user's informa=on (username, email, and password) securely in a MySQL database table.

Other Points:
1. Implement password hashing when storing the password in the database.
2. Add a "Login" funconality to the project, allowing registered users to log in with their credentials and display a simple dashboard page aXer successful login.

STEPS

I have completed the task using using PHP Mysql. Below is the description of the steps I followed.

I created a folder in Xampp>htdocs.

I created a database in PhpMyAdmin
Database name: login_register
table: users
I created 4 coloumns in table
1. id (int) and checked the primary and Auto increament checkbox
2. full_name (varchar)
3. email (varchar)
4. password (varchar)

Below is the Visual Studio Code Explanation

1. Registration.php

PHP Registration Logic:
Inside the <div class="container"> element, the PHP code handles the registration process when the form is submitted ($_POST["submit"] is set). User input is collected from the form fields ($fullName, $email, $password, and $passwordRepeat). The provided password is hashed using the password_hash function for security.

Input Validation:An array named $errors is used to collect validation errors.The code checks if any of the fields are empty and adds an error message to the array if they are. It uses filter_var to validate the email format and adds an error message if the email is not valid. The password length is checked, and if it's less than 8 characters, an error message is added. It compares the password and repeat password fields and adds an error message if they don't match. 

Database Interaction: The code includes a "database.php" file using require_once to establish a connection to the database. It constructs a SQL query to check if the entered email already exists in the database. The query is executed using mysqli_query, and the number of matching rows is counted. If an email match is found ($rowCount > 0), an error message is added to the $errors array.

Displaying Errors:If any validation errors are present (count of $errors > 0), the code iterates through the errors and displays them using Bootstrap's alert classes.
Registration Process:
If no validation errors are present, the code constructs an INSERT SQL query to add the user's information to the database. It uses prepared statements to prevent SQL injection and binds parameters to the query. If the prepared statement is successfully initialized, the user's information is inserted into the database, and a success message is displayed.

HTML Form Inputs: The HTML form inputs include fields for full name, email, password, and repeat password. The form's action attribute is set to "registration.php", indicating that the form data should be submitted to the same page for processing. The form uses the POST method to send data.

Login Link: A link is provided below the form for users who are already registered, directing them to the login page ("login.php").

2. Database.php

Parameters: The code defines four variables: $hostName, $dbUser, $dbPassword, and $dbName.
   
$hostName: Specifies the hostname or IP address of the database server. In this case, it's set to "localhost", which means the database server is on the same machine where the PHP script is running.
$dbUser: Represents the username used to authenticate and access the database server.
$dbPassword: Corresponds to the password associated with the specified username.
$dbName: Specifies the name of the database that needs to be accessed.

Database Connection:
The mysqli_connect() function is used to establish a connection to the database server using the provided connection parameters. The function takes the hostname, username, password, and database name as arguments. If the connection is successful, a connection object is returned. If the connection fails, mysqli_connect() returns false.

Connection Check and Error Handling:The code uses an if condition to check if the connection to the database was successful ($conn is not false).If the connection was successful, the script continues execution without any issues.If the connection fails ($conn is false), the code calls die() with the message "something went wrong". This terminates the script and displays the error message.

4. Login.php

Session Management: The code starts with session_start(), which initializes a session. Sessions are used to persist data across multiple requests.
The code checks if a session variable named "user" is set. If it's set, this typically indicates that the user is already logged in. In that case, the code redirects the user to the "index.php" page using header("Location: index.php"). This is a common practice to prevent logged-in users from accessing the login page again.

HTML Form Structure:The code follows the same HTML and Bootstrap structure as before. It includes form elements for entering the email and password.

PHP Login Logic:When the form is submitted (the "login" button is pressed), the code retrieves the entered email and password.It includes the "database.php" file to establish a database connection. A SQL query is constructed to retrieve user information from the database based on the provided email. The query result is fetched into an associative array $user.
If a user with the provided email is found ($user is not empty), it uses password_verify() to compare the provided password with the hashed password stored in the database. If the passwords match, a new session is started, and a session variable "user" is set to "yes" to indicate that the user is logged in. The user is then immediately redirected to the "index.php" page using header("Location: index.php"), and the script execution is terminated with die(). If the passwords don't match, an error message is displayed indicating incorrect password. If no user is found with the provided email, an error message is displayed indicating incorrect email.

Login Form Inputs: The HTML form inputs include fields for entering the email and password. The form's action attribute is set to "login.php", indicating that the form data should be submitted to the same page for processing. The form uses the POST method to send data.

Registration Link: A link is provided below the form for users who are not registered, directing them to the registration page ("registration.php").

Session Management (Again):Once again, the code initializes a session and checks for an existing "user" session variable. This is done to prevent users from accessing the login page after logging in.

5. index.php
Session Start and User Check: The code starts with session_start() to initiate a session. Sessions are used to persist data across multiple requests. The code checks if a session variable named "user" is not set (!isset($_SESSION["user"])). This is done to ensure that only logged-in users can access the dashboard. If the user is not logged in, the code redirects them to the login page using header("Location: login.php"). This ensures that unauthorized users are redirected to the login page.

HTML Structure: The code follows the standard HTML structure. It includes a Bootstrap CSS framework for styling and a custom CSS file named "style.css". The page title is set to "User Dashboard".Dashboard Content: Inside the <div class="container"> element, the code displays a welcoming message in an heading, indicating that the user is on the dashboard. It also includes a "Logout" button with the class "btn btn-warning". This button provides a link to a "logout.php" page for users to log out from the dashboard.

Logout Link: The "Logout" button (<a href="logout.php" class="btn btn-warning">Logout</a>) provides a link to a "logout.php" page. This is likely where the user's session will be terminated to log them out.

6. Logout.php
Session Start:The code starts with session_start() to initiate a session. Although not strictly necessary for this particular code, it's a common practice to ensure that session handling is available.
Session Destroy:The session_destroy() function is used to completely destroy the current session, including all the session variables and data associated with it.
Redirect to Login Page: After destroying the session, the header("Location: login.php") line is used to immediately redirect the user to the login page (login.php). This ensures that after logging out, the user is directed back to the login page.
