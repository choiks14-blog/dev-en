---
title: What is fastapi?
author: alpa28980
date: Tue, 26 Nov 2024 01:13:06 GMT
categories: ["Program Language"]
tags: ["fastapi"]
comment: true
---

Introduction.


FastAPI is a Python-based web framework that enables modern, high-performance API development. The framework leverages standard Python type hints to build APIs quickly and easily.

Some of the key reasons to learn and use FastAPI include the following features

* Extremely fast performance: It offers great performance on par with Node.js and Go .
* Increased development productivity: You can speed up feature development by about 200-300%.
* Fewer bugs: Reduce bugs due to developer mistakes by about 40%.
* Intuitive and easy to use: Reduce debugging time with excellent editor support and auto-completion.
* Concise code: Minimize code duplication and implement different functions with parameter declarations.
* Robust data validation: The Pydantic library enables robust data validation.
* Automatic and interactive API documentation: Automatically generate OpenAPI specifications for easy API documentation.

With these features, FastAPI helps Python developers develop modern, practical APIs quickly and productively.

FastAPI's basic functionality - API creation and routing
-----------------------------

Creating and routing APIs using FastAPI is very simple. First, create a FastAPI instance.

python

    from fastapi import FastAPI
    
    app = FastAPI()
    

Next, write a function that defines the API endpoint. You can use decorators like `@app.get()`, `@app.post()`, etc. to specify HTTP methods and URL paths.

python

    @app.get("/")
    def read_root():
        return {"message": "Hello, FastAPI!"}
    
    @app.get("/items/{item_id}")
    def read_item(item_id: int, q: str = None):
        return {"item_id": item_id, "q": q}
    

In the example above, we defined a `read_root` function to handle GET requests for the `"/"` path and a `read_item` function to handle GET requests for the `"/items/{item_id}"` path. Using type hints in function parameters automatically validates and documents your data.

FastAPI also supports asynchronous programming. You can use `async` and `await` in endpoint functions to handle asynchronous operations.

python

    @app.get("/async_items/{item_id}")
    async def read_async_item(item_id: int):
        # perform an asynchronous operation
        result = await some_async_operation(item_id)
        return {"item_id": item_id, "result": result}
    

Finally, run the application to start the API server.

python

    if __name__ == "__main__":
        import uvicorn
        uvicorn.run(app, host="0.0.0.0", port=8000)
    

In questo modo, FastAPI consente di sviluppare API più facile e rapido utilizzando le funzionalità di tipi di Python. Inoltre, il supporto di programmazione asynchrono permette di ottenere una potenza di prestazioni

Basic features of FastAPI - Define your data model
--------------------------

FastAPI uses the Pydantic library to define a data model. The Pydantic model allows you to define fields in the request body, nested models, and additional data models.

For example, with the Body - Fields approach, you can define a data model like this

python

    from pydantic import BaseModel
    
    class Item(BaseModel):
        name: str
        description: str = None
        price: float
        tax: float = None
    

When you declare fields and types using type hints, FastAPI automatically performs data validation and serialization/deserialization for you. This allows developers to be more productive by not having to write validation logic manually.

The data model is also included in the automatically generated interactive documentation, making it easy to understand the request/response data format of the API. Thus, FastAPI uses Pydantic to define the data model, automate validation and serialization, and increase development productivity.

FastAPI's native feature - automatic API documentation
---------------------------

FastAPI generates automatic interactive API documentation based on OpenAPI (Swagger) specifications. This makes it easy for developers to see the API's endpoints, parameters, response formats, and more without having to do any documentation.

FastAPI provides two systems to render API documentation: Swagger UI and ReDoc. Both systems are based on the OpenAPI specification and have similar functionality but different UIs. Developers can choose the documentation system that suits their preferences.

The Swagger UI is accessible from the `/docs` path, and ReDoc is accessible from `/redoc`. Both systems work in a web browser, where you can view API endpoints and parameters and test them yourself. You can also add comments to your documentation.

In this way, FastAPI greatly reduces the documentation effort for developers by automatically generating OpenAPI specifications and providing interactive API documentation through the Swagger UI and ReDoc. Developers only need to focus on their code, and can easily create production-quality API documentation.

FastAPI's native feature - Dependency Injection
-----------------------

In FastAPI, Dependency Injection is an important concept that increases the modularity and flexibility of your code. Dependency injection reduces the coupling between objects, making your code easier to maintain and reuse.

In FastAPI, you can define and inject dependencies using the `Depends` decorator. For example, you can create a dependency for connecting to a database as follows.

python

    from fastapi import Depends
    from db import get_db_connection
    
    def get_db():
        db = get_db_connection()
        try:
            yield db
        finally:
            db.close()
    
    @app.get("/users")
    def get_users(db=Depends(get_db)):
        # retrieve user data using the db object
        ...
    

By defining the `get_db` function as a dependency like this, the `get_users` function will automatically be injected with the database connection object. This allows us to separate and reuse the database connection logic .

The main advantage of dependency injection is that it makes your code less coupled and more modular. Separating dependencies for each function makes your code more readable and maintainable. It also makes it easier to test by injecting fake objects instead of real ones.

In FastAPI, you can inject dependencies not only in function parameters, but also in class constructors, HTTP request objects, etc. And the `Dependencies` decorator lets you define globally shared dependencies.

As you can see, FastAPI's dependency injection capabilities increase the modularity and flexibility of your code and facilitate testing. Therefore, it's important to make good use of the concept of dependency injection when developing applications with FastAPI.

FastAPI's basic feature - Asynchronous support
-----------------------

FastAPI supports asynchronous processing by using an Asynchronous Server Gateway Interface (ASGI) server. Unlike synchronous web servers, ASGI can process multiple requests simultaneously on a single thread. This allows FastAPI to provide high parallelism and scalability.

In FastAPI, asynchronous functions are defined using the `async` keyword and the `await` expression. For example, you can write an asynchronous function as follows:

python

    @app.get("/async_items/{item_id}")
    async def read_async_item(item_id: int):
        result = await some_async_operation(item_id)
        return {"item_id": item_id, "result": result}
    

In the above code, the `read_async_item` function uses the `async` keyword to indicate that it is an asynchronous function. And it uses the `await` expression to wait for the result of the `some_async_operation` function. This allows the FastAPI to keep the current request in a waiting state while it processes other requests.

With ASGI and async/await support, FastAPI provides high concurrency and efficient resource usage, enabling you to build highly performant APIs. The asynchronous programming model is also particularly useful for I/O-bound operations, and can result in performance gains in tasks such as database operations, file processing, and network requests.

Benefits of FastAPI
-----------

FastAPI provides Python developers with the following key benefits

1. Increased development productivity: FastAPI can speed up feature development by 200-300% through intuitive API design and automatic documentation . It also leverages the Pydantic library to automate data validation and serialization, which greatly improves development productivity .
    
2. High performance: Based on Starlette and Pydantic, FastAPI delivers extremely high performance on the level of NodeJS and Go. It also supports asynchronous programming, enabling high concurrency and efficient resource usage.
    
3. Automated data validation and serialization: FastAPI automatically performs robust data validation and serialization/deserialization via the Pydantic library. This frees developers from having to write validation logic manually, resulting in higher productivity and fewer bugs.
    
4. OpenAPI and JSON schema support: FastAPI fully supports OpenAPI specifications and JSON schemas, enabling automatic interactive documentation generation and client code generation. This greatly reduces your API documentation efforts.
    
5. Easy integration testing: FastAPI facilitates API integration testing by providing a test client. This shortens development and testing cycles and increases reliability.
    

As you can see, FastAPI is a modern framework that combines development productivity, performance, and reliability to help Python developers develop APIs more efficiently.

FastAPI use cases
-------------

FastAPI is a powerful framework that can be utilized in many different areas. First, you can use FastAPI for backend development of web applications. The intuitive API design and automatic documentation features increase development productivity, and the high performance and asynchronous programming support allow you to build scalable backend systems.

FastAPI also fits nicely into microservice architectures. Dependency injection makes it easy to modularize each microservice, and support for the OpenAPI specification facilitates communication between microservices. Netflix built its crisis management framework, Dispatch, with FastAPI.

FastAPI is also great for building data APIs. Automatic data validation and serialization/deserialization with the Pydantic library increases development productivity. Support for OpenAPI and JSON schemas makes it easy to use the API with a variety of clients.

You can also leverage FastAPI for deploying machine learning models. Uber has used FastAPI to deploy ML models for the Ludwig project. Its fast performance and asynchronous support provide high throughput, and its simple API interface makes model serving easy.

Finally, FastAPI can be utilized for IoT and sensor data processing. The asynchronous programming model allows for efficient processing of large amounts of sensor data, and the lightweight API interface allows for seamless communication with IoT devices.

As you can see, FastAPI has a wide range of applications, including web application backends, microservices, data APIs, machine learning model deployment, IoT and sensor data processing, and more. You can take advantage of FastAPI's advantages in development productivity, performance, scalability, and modularity and apply them to a variety of real-world projects.

Conclusion.
--

FastAPI is a modern, high-performance web framework developed in Python that has the following key features

1. Extremely fast performance: it offers excellent performance on the level of NodeJS and Go.
2. Fast development speed: It can speed up feature development by about 200-300%. 3.
3. Fewer bugs: Reduce bugs caused by developer mistakes by about 40%.
4. Intuitive and easy to use: Editor support and auto-completion are excellent and easy to learn.
5. concise code: Minimize code duplication and implement different features with parameter declarations.
6. Powerful documentation generation: Provides interactive API documentation by automatically generating OpenAPI specifications.

As you can see, FastAPI offers benefits in terms of development productivity, performance, reliability, documentation, and more, helping Python developers develop APIs more efficiently. In fact, FastAPI is utilized by high-profile companies like Microsoft, Uber, and Netflix, and is growing in popularity in the developer community.

In the future, FastAPI is expected to add more features and improve performance, further solidifying its place in the Python web framework ecosystem. The FastAPI team will continue to make updates and improvements to provide Python developers with the latest, most productive and powerful tools.

---
---

<iframe src="https://ads-partners.coupang.com/widgets.html?id=807239&template=carousel&trackingCode=AF3190673&subId=&width=680&height=140&tsource=" width="680" height="140" frameborder="0" scrolling="no" referrerpolicy="unsafe-url" browsingtopics></iframe>
해당 링크를 통해 제품 구매가 이루어진 경우 쿠팡 파트너스 활동 일환으로 인해 일정 수수료가 블로거에게 제공되고 있습니다

