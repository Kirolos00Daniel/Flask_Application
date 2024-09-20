# Flask_Application
Simple User Flask Application

# Full-Stack User Management Application

This is a full-stack web application that demonstrates basic CRUD (Create, Read, Update, Delete) operations on user data. The back-end is built using Flask, and the front-end is created using HTML, CSS, and JavaScript. This application allows users to create, view, update, and delete user profiles through a user-friendly interface.

## Application Screenshot

![Application Screenshot](![Screenshot 2024-09-20 143936](https://github.com/user-attachments/assets/e7878be8-a6aa-4990-932a-96c34c75d744)
)

## Prerequisites

- Python 3.6+
- Flask
- Basic understanding of HTML, CSS, and JavaScript

## Installation

### 1. Clone the Repository

```bash
git clone <repository-url>
cd <repository-folder>
```

### 2. Set Up the Back-End

1. Create and activate a virtual environment (optional but recommended):

   ```bash
   python3 -m venv venv
   source venv/bin/activate
   ```

2. Install the required packages:

   ```bash
   pip install flask
   ```

3. Start the Flask development server:

   ```bash
   python app.py
   ```

4. The Flask server will run on `http://127.0.0.1:5000/`.

### 3. Set Up the Front-End

1. Open the `index.html` file in the `templates` folder using a web browser.

2. This file serves as the front-end interface, interacting with the Flask back-end.

## Application Overview

### Back-End (Flask API)

The back-end is built using Flask and provides the following API endpoints:

1. **Home Route** (`GET /`): Displays the homepage using the `index.html` template.

2. **Create a New User** (`POST /users`): Creates a new user with the provided `name` and `email`.

3. **Retrieve All Users** (`GET /users`): Retrieves all users stored in the in-memory database.

4. **Update an Existing User** (`PUT /users/<user_id>`): Updates the user with the given `user_id`.

5. **Delete a User** (`DELETE /users/<user_id>`): Deletes the user with the given `user_id`.

### Front-End (HTML, CSS, JavaScript)

The front-end consists of an HTML page (`index.html`) that allows users to:

1. **View Users**: Displays a list of all users in the system.

2. **Add a New User**: Provides a form to create a new user by entering their name and email.

3. **Update User**: Allows editing the details of an existing user.

4. **Delete User**: Removes a user from the system.

### Example HTML for Front-End

Here's a brief overview of the structure of the `index.html` file:

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>User Management App</title>
    <link rel="stylesheet" href="styles.css">
</head>
<body>
    <div class="container">
        <h1>User Management System</h1>
        <form id="userForm">
            <input type="text" id="name" placeholder="Name" required>
            <input type="email" id="email" placeholder="Email" required>
            <button type="submit">Add User</button>
        </form>
        <div id="userList"></div>
    </div>
    <script src="script.js"></script>
</body>
</html>
```

### Example JavaScript for Interactions

The front-end uses JavaScript to make API calls to the Flask back-end and dynamically update the user interface.

```javascript
document.addEventListener('DOMContentLoaded', function() {
    // Fetch users and display them
    fetch('/users')
        .then(response => response.json())
        .then(data => {
            const userList = document.getElementById('userList');
            for (let user in data) {
                const userItem = document.createElement('div');
                userItem.innerHTML = `<strong>${data[user].name}</strong> - ${data[user].email}`;
                userList.appendChild(userItem);
            }
        });
    
    // Handle form submission to add a new user
    document.getElementById('userForm').addEventListener('submit', function(event) {
        event.preventDefault();
        const name = document.getElementById('name').value;
        const email = document.getElementById('email').value;

        fetch('/users', {
            method: 'POST',
            headers: {'Content-Type': 'application/json'},
            body: JSON.stringify({name: name, email: email})
        })
        .then(response => response.json())
        .then(data => {
            const userList = document.getElementById('userList');
            const userItem = document.createElement('div');
            userItem.innerHTML = `<strong>${data.name}</strong> - ${data.email}`;
            userList.appendChild(userItem);
        });
    });
});
```

## Future Enhancements

- **Database Integration**: Replace the in-memory storage with a persistent database like SQLite or MongoDB.
- **Authentication**: Add user authentication for better security.
- **Improved UI/UX**: Enhance the front-end with better styling and user experience.

## License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.
