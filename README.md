# AssociationHUB

AssociationHUB is a web application designed to help manage and organize the activities of an association. This application allows administrators to manage users, events, news, achievements, and more. Members of the association can view upcoming events, news updates, and other relevant information.


![Screenshot](app/assets/0.png?raw=true "Screenshot")
[AssociationHUB](https://sa030.pythonanywhere.com) - *Live Demo of the website*

## Story

We met with a local community association to explore potential projects.
They shared their struggles with managing their workflow efficiently.
Inspired by their needs, we decided to develop AssociationHub,
a web app designed to streamline and simplify association management.
AssociationHub will help associations manage their tasks, members,
and events more effectively, making their operations smoother and more organized.



## Features

- User Management
- Event Management
- News Management
- Achievement Tracking
- Contact Messaging
- Reports and Attendance Tracking

## Tech Used

- Flask
- MySQL
- Python
- [Bootstrap](https://getbootstrap.com/)
- Free Deployement Thanks To [PythonAnywhere](https://www.pythonanywhere.com/)

## Getting Started

Follow these instructions to set up and run the AssociationHUB application on your local machine.

### Prerequisites

- Python 3.x
- Flask
- SQLAlchemy
- MySQL

### Installation

1. Clone the repository.

2. Install the required dependencies.
    
3. Create a database with install.sql.

4. Run the application:
    ```sh
    flask run
    ```

8. Access the application at `http://127.0.0.1:5000`.

*note that deploying to PythonAnywhere need some extra tweaks more info [here](https://help.pythonanywhere.com/pages/Flask/)*

## Usage

### Admin Panel

Admins can log in and access the admin panel to manage users, events, news, achievements, and more.

### User Interaction

Users can view the list of events, news updates, achievements, and contact the association via the contact form.

## Contributing

### Exemples of route layout

```python
# User routes
@admin_bp.route('/users', methods=['POST'])
@login_required
def create_user():
    if not current_user.is_admin:
        flash('You do not have permission to create users.', 'error')
        return redirect(url_for('main.home'))
    
    username = request.form.get('username')
    email = request.form.get('email')
    password = request.form.get('password')
    is_admin = request.form.get('is_admin') == 'on'
    section = request.args.get('section', 'users')
    # Checking required fields
    if not username or not email or not password:
        flash('Username, email, and password are required fields.', 'error')
        return redirect(url_for('admin.dashboard', section='users'))

    # Checking the uniqueness of the email
    existing_user = User.query.filter_by(email=email).first()
    if existing_user:
        flash('Email address is already in use. Please use a different email.', 'error')
        return redirect(url_for('admin.dashboard', section='users'))

    # Creation of the new user
    new_user = User(username=username, email=email, is_admin=is_admin)
    new_user.set_password(password)
    
    # Add to database
    db.session.add(new_user)
    db.session.commit()

    flash('New user added successfully.', 'success')
    return redirect(url_for('admin.dashboard', section='users'))
```
### Small Explanation

- Defines a route `/users` with a `POST` method within the `admin_bp` blueprint.
- Checks if the current user is an admin.
- Retrieves user input from the form.
- Validates required fields (`username`, `email`, `password`).
- Checks if the email address is already in use by querying the database.
- Creates a new `User` object with the provided `username`, `email`, and `is_admin` status.
- Sets the `password` for the new user.
- Adds the new user to the database session and commits the session.
- Displays a success message.
- Redirects to the admin dashboard, showing the 'users' section.


## Video Demo

[![YoutubeDemo](https://img.youtube.com/vi/gAOxDsZ9lU4/0.jpg)](https://www.youtube.com/watch?v=gAOxDsZ9lU4)

*Note: You can open the video in a new tab by right-clicking the link and selecting "Open link in new tab" or by middle-clicking the link.*

## License

This project is made by Salim Abdessamad and Ahmed Sahbeddine.
