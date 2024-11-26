---
title: What is flask?
author: alpa28980
date: Tue, 26 Nov 2024 01:28:54 GMT
categories: ["Program Language"]
tags: ["flask"]
comment: true
---

Introduction.


Flask is a lightweight web framework based on Python. Flask is designed to get you started developing web applications quickly and easily, while still having the flexibility to scale to complex applications.

Some of the key features of Flask include providing Application Context and Request Context, support for modularization and extensibility through Blueprints, a wide range of extensions, a command line interface, a built-in development server, and an interactive Python shell. These features make development easier and more productive, and facilitate structuring and extending the functionality of your application.

As a lightweight framework, Flask has a low barrier to entry for development with its simple code structure and small memory footprint. It also gives you the flexibility to configure your application by adding only the features you need. This makes Flask ideal for prototyping and small projects, but it is also scalable for larger projects.

Structure of Flask - Basic structure
-----------------

The basic structure of a Flask application consists of the following core elements

1. application object (app) A Flask application is organized around an app object, which is an instance of the Flask class. This object manages all the components and behavior of the application.

python

    from flask import Flask
    app = Flask(__name__)
    

2. Blueprint For complex applications, you can modularize and manage them by functionality. Blueprints allow you to group routing, view functions, static files, and more and register them with your app.

python

    from flask import Blueprint
    bp = Blueprint('blog', __name__)
    

3. Routing and View Functions Routing maps a URL to a view function, which is the processing logic for that URL. The view function processes the request and generates a response.

python

    @app.route('/')
    def index():
        return 'Hello, World!'
    

4. Request and Response The request object (request) stores the data sent from the client (URL parameters, form data, files, etc.). The response object (response) contains the data to be sent to the client.
    
5. Rendering a template Flask uses the Jinja2 template engine to generate dynamic HTML pages. You can pass data to a template for rendering.
    
6. Session Sessions allow you to store and manage the client's state information on the server. It is utilized for login authentication, shopping carts, etc.
    

As you can see, Flask applications are a combination of the above core elements that work together seamlessly to provide the functionality of a web application.

Structure of Flask - Routing and view functions
---------------------

In Flask, routing uses the @app.route decorator to associate a URL pattern with a view function that will process that URL. For example, you can define routing like this

python

    @app.route('/')
    def index():
        return 'Hello, World!'
    
    @app.route('/about')
    def about():
        return 'About Page'
    

In the above code, '/' is the base URL, and when a request comes in for this URL, the index() function is executed. Requests for the '/about' URL are handled by the about() function.

The view function is responsible for processing client requests and generating responses. The request object (request) provides access to data such as URL parameters, form data, files, and more. The response object (response) contains the data to be sent to the client. Here's an example of a simple view function

python

    @app.route('/user/<username>')
    def show_user(username):
        # retrieve user info from database
        user = get_user_by_name(username)
        if user:
            # respond by rendering the user information to an HTML template
            return render_template('user.html', user=user)
        else:
            # respond with a 404 error
            abort(404)
    

In the code above, the show\_user() function uses the username parameter passed in the URL to retrieve the user information from the database. If the user information exists, it responds by rendering it in the user.html template, otherwise it returns a 404 error.

Structure of Flask - Templates
---------------

Flask uses the Jinja2 template engine to generate dynamic web pages. Templates are written using a mixture of HTML markup language and Jinja2's syntax, and are rendered on the server and converted to HTML strings.

Jinja2 provides the following key features

* Template inheritance: you can define a basic layout and inherit from sub-templates to insert content. This helps you avoid code duplication and maintain a consistent layout.
* Filters: You can convert or manipulate data into the format you want. For example, you can capitalize strings or change date formats.
* Macros: Define reusable code snippets and call them from within templates.
* Context processors: Allows you to define variables that can be used in templates.

In your Flask application, use the render\_template function to render the template. You pass the template file path and the data to render to this function. For example:

python

    from flask import render_template
    
    @app.route('/')
    def index():
        user = {'name': 'John Doe'}
        return render_template('index.html', user=user)
    

In the code above, the index.html template is rendered, and the user object is passed to the template. The template uses the {{ user.name }} syntax to access the data.

Jinja2's syntax allows you to utilize conditional statements, loops, filters, macros, and more to create dynamic web pages. Template inheritance helps you avoid code duplication and maintain a consistent layout .

Flask's main feature - request processing
--------------------

Flask allows you to process data sent from the client via a request object (request). A request object contains information such as URL parameters, form data, files, and more.

For GET requests, you can access the data contained in the URL parameters:

python

    from flask import request
    
    @app.route('/user')
    def get_user():
        # do some processing logic with the username username = request.args.get('username')
        # perform processing logic with username
        ...
    

For POST requests, you can process form data or JSON data:

python

    @app.route('/login', methods=['POST'])
    def login():
        username = request.form.get('username')
        password = request.form.get('password')
        # perform login processing logic
        ...
    

python

    @app.route('/api/users', methods=['POST'])
    def create_user():
        # get JSON data user_data = request.get_json() # receive JSON data
        # perform user creation logic
        ...
    

Le principali proprietà e metodi del nostro oggetto di richiesta sono

* request.args: parameter values included in the URL query string.
* request.form: Form data for the POST request
* request.files: Uploaded files
* request.headers: Request headers
* request.method: Request method (GET, POST, etc.)
* request.get\_json(): Parsing JSON data

Come questo, Flask utilizza l'oggetto di richiesta per facilmente processare diversi tipi di dati di richiesta

Key Features of Flask - Session Management
--------------------

In Flask, the session object (session) allows you to store and manage the client's state information on the server. This is utilized in a variety of features, including login authentication, shopping carts, and more.

Session data is typically stored in the server's file system, memory, or database. In Flask, session data is stored serialized in cookies and sent to and from the client, which is encrypted to keep it secure.

python

    from flask import Flask, session
    
    app = Flask(__name__)
    app.secret_key = 'super_secret_key' # set key for session encryption
    
    @app.route('/set_session')
    def set_session():
        # save data to session session['username'] = 'john_doe' # save data to session
        return 'Session set'
    
    @app.route('/get_session')
    def get_session():
        # get data from session username = session.get('username', 'Guest') # fetch data from session
        return f'Username: {username}'
    

The example above shows how to store and retrieve session data: set the session encryption key via app.secret\_key, and use the session object to store and read the data.

Flask also provides options for managing session lifetime. By setting the permanent attribute to True, you can extend the expiration time of the session cookie to until the client exits. You can also prevent CSRF attacks through the SESSION\_COOKIE\_SAMESITE setting.

Key Features of Flask - Database Integration
------------------------

Flask allows you to integrate databases using SQLite or SQLAlchemy. SQLite is a file-based, lightweight database that is often used in development and test environments. SQLAlchemy is an Object-Relational Mapping (ORM) library in Python that allows you to integrate with various databases to process data in an object-oriented way.

You can use SQLAlchemy to define database models and perform CRUD operations. First, install the Flask-SQLAlchemy extension package.

    pip install flask-sqlalchemy
    

Then, initialize SQLAlchemy in your Flask application.

python

    from flask import Flask
    from flask_sqlalchemy import SQLAlchemy
    
    app = Flask(__name__)
    app.config['SQLALCHEMY_DATABASE_URI'] = 'sqlite:///db.sqlite'
    db = SQLAlchemy(app)
    

The database model is defined by inheriting from SQLAlchemy's model class.

python

    from .models import db
    
    class User(db.Model):
        id = db.Column(db.Integer, primary_key=True)
        username = db.Column(db.String(80), unique=True, nullable=False)
        email = db.Column(db.String(120), unique=True, nullable=False)
    
        def __repr__(self):
            return f'<User {self.username}>'
    

With a model defined like this, you can perform CRUD operations on the database. For example, here's the code to add and lookup a user

python

    from .models import User, db
    
    # Add a user
    user = User(username='john_doe', email='john@example.com')
    db.session.add(user)
    db.session.commit()
    
    # query user
    user = User.query.filter_by(username='john_doe').first()
    print(user.username, user.email) # john_doe john@example.com
    

As you can see, Flask uses the SQLAlchemy ORM to define the database model and perform CRUD operations. SQLite or other databases can also be easily integrated with SQLAlchemy .

Flask's main feature - serving static files
-----------------------

Flask creates a `static` folder inside your project to serve static files (CSS, JavaScript, images, etc.). This folder should be located in the root directory of your Flask application. To serve static files, you need to register them with the `static_folder` parameter in your app.py file, like this

python

    from flask import Flask
    
    app = Flask(__name__, static_folder='static')
    

Now, to generate a URL to access the static file, use the `url_for` function . For example, the URL for the file `/static/css/styles.css` could be generated like this

python

    from flask import url_for
    
    css_url = url_for('static', filename='css/styles.css')
    

To use the URL of a static file in a template, do the following

html

    <link rel="stylesheet" href="{{ url_for('static', filename='css/styles.css') }}">
    

When serving static files, it's important to set up caching properly. Flask provides default settings for caching static files, but in production environments, we recommend serving static files directly from your web server for better performance.

Flask's main feature - Extensions
--------------------

In addition to its core features, Flask offers a number of extensions, allowing developers to add functionality as needed. Some of the main extensions include

* Flask-SQLAlchemy: Allows you to integrate with databases using the SQLAlchemy ORM.
* Flask-Login: Allows you to build a user authentication system.
* Flask-WTF: Utilize the WTForms library to simplify form processing.
* Flask-Mail: Provides email sending functionality.
* Flask-Migrate: Supports SQLAlchemy database migration.
* Flask-Caching: Provides caching capabilities to improve application performance.

These extensions can be installed via pip. For example, to install Flask-SQLAlchemy, run the following command:

    pip install flask-sqlalchemy
    

You can then initialize and use the extension in your Flask application. For example, to use Flask-SQLAlchemy, you can do the following

python

    from flask import Flask
    from flask_sqlalchemy import SQLAlchemy
    
    app = Flask(__name__)
    app.config['SQLALCHEMY_DATABASE_URI'] = 'sqlite:///db.sqlite'
    db = SQLAlchemy(app)
    
    class User(db.Model):
        id = db.Column(db.Integer, primary_key=True)
        username = db.Column(db.String(80), unique=True)
    
        def __repr__(self):
            return f'<User {self.username}>'
    

In the code above, we have initialized SQLAlchemy, defined the User model, and can then perform database CRUD operations .

As you can see, Flask offers a wide range of extensions, making it easy for developers to add the functionality they need. By utilizing extensions, you can build more feature-rich web applications.

Pros and cons of Flask
----------

The main advantages of Flask are its lightweight and scalability. As a micro-web framework, Flask has a lightweight structure, which allows for a low barrier to entry and fast initial development. It also allows you to selectively add only the features you need, giving you the flexibility to configure your application. This is great for prototype development or small-scale projects. It's also scalable for larger projects with Blueprints and Extensions.

However, Flask's disadvantages include its unsuitability for large projects and possible security issues. As a micro-framework, it can lack features for larger projects, and security features can be a hassle to implement yourself. It can also lack support due to its relatively small community compared to other frameworks.

So, while Flask is great for prototype development or small projects, for larger projects, you should consider other frameworks. Also, you'll need to take care of security issues on your own. However, due to its lightweight and scalability, Flask is still a popular web framework for many developers.

Conclusion.
--.

Flask has two key characteristics: lightweight and scalability. As a micro-web framework, its simple code structure and small memory footprint provide a low barrier to entry for initial development, and it gives you the flexibility to configure your application by adding only the features you need. It also scales easily to large projects with its Blueprints feature.

Flask is often utilized for prototype development and small-scale projects. However, thanks to its scalable structure, it is also being used to develop large-scale web services. For example, services like Netflix and Reddit use Flask.

Going forward, Flask is expected to continue to evolve within the Python ecosystem, especially as Python is increasingly utilized in various fields such as machine learning and data analytics. Flask is also gaining traction as a framework for developing cloud-based serverless applications.

To summarize, Flask is a lightweight and scalable Python web framework that is becoming useful for developing web applications of various sizes. It has a wide range of applications from prototype development to large-scale services, and as Python's influence grows, Flask is expected to be utilized even more in the future.

---
---

<iframe src="https://ads-partners.coupang.com/widgets.html?id=807239&template=carousel&trackingCode=AF3190673&subId=&width=680&height=140&tsource=" width="680" height="140" frameborder="0" scrolling="no" referrerpolicy="unsafe-url" browsingtopics></iframe>
해당 링크를 통해 제품 구매가 이루어진 경우 쿠팡 파트너스 활동 일환으로 인해 일정 수수료가 블로거에게 제공되고 있습니다

