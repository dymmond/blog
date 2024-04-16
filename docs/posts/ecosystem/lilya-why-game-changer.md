---
date: 2024-04-03
categories:
  - Technology
  - Ecosystem
  - Lilya
slug: lilya-asgi-game-changer
authors:
  - tarsil
comments: true
---

# Lilya — Why it will be a game changer in the ASGI world

---

<img src="https://res.cloudinary.com/dymmond/image/upload/v1707501404/lilya/logo_quiotd.png" alt="Lilya" />

Lilya

* **Official documentation**: [https://lilya.dev][lilya]
* **Github**: [https://github.com/dymmond/lilya](https://github.com/dymmond/lilya)

<!-- more -->

## Background story

In the current world of software engineering, frameworks pop-up like mushrooms and that can be good (or bad if you see it in that way) as we are provided with a lot of alternatives to address a specific issue.

Python in the last 10 years (time of this writing) has grown exponentially due to the likes of ML (Machine Learning) and AI (Artificial Intelligence).
The story of Lilya is not new but the motivation for it, is. As mentioned before, in the world of Python, a lot has happened giving enough room for innovation to occur.

Who never heard of Django, FastAPI and Starlette. Well, the latter is actually what powers up FastAPI.

In the last couple of years a new framework emerged, Esmerald also built on the top of Starlette, like FastAPI but not the same as FastAPI. Actually, Esmerald was designed with a completely different purpose than only building super fast APIs, in fact, the target audience are mostly the ones that understand how Django operates.

> So, another Django?

Not even close.

Almost everything that pops out now in Python and ASGI has somehow Starlette behind it and the reason for that it is because it simply works as toolkit and works really well but has its own limitations like everything.

## What is Lilya

[Lilya][lilya] was initially born out of a need for Esmerald and quickly became something else.
From the [Lilya][lilya] documentation:

> A lot of times you won't be needing a fully fledged Python web framework as it can be overwhelming for some simple tasks, instead you would prefer a simple
> ASGI toolkit that helps you designing production ready, fast, elegant, maintainable and modular applications.
>
> This is where Lilya places itself.


[Esmerald][esmerald] in the past was relying on Starlette and its changes and lot of those times, it broke the internal API of Esmerald. This is not a very nice thing to have if you want to keep the integrity of the framework, isn't it?

Well, this was the initial driver to start thinking of Lilya. The full control of the ecosystem that powers Esmerald but quickly became something that could be even more powerful and independent and also became the facto core part of Esmerald, replacing Starlette internally.

It is important to mention that this does not mean Starlette is not good, actually, Starlette is one of the most powerful tools you can use.

With minimal dependencies and 100% pythonic, Lilya came to be the next generation of ASGI toolkit for Python developers. Not only you can build production ready, fast, elegant, maintainable and modular applications but also brings a lot of out-of-the-box features that can and should be used to help you out with your development lifecycle.

In this article, we will be covering a few of those and unlock the power of Lilya.

## Lilya and Features

As mentioned in the [official documentation][lilya], Lilya brings some good things.

Let us explore some of those features.

### Installation

Well, this is the basic right?

```shell
$ pip install lilya
```

This will make sure you will have the latest Lilya installed.

### Starting a project

Now this is where we can already see Lilya shining. Everyone, literally everyone has its own way of structuring a project and that remains as is if you want.

What Lilya brings is a set of suggestions for a quick startup project and for you not to worry about trivial decisions.
For that, **Lilya uses the native and optional client**.

Since it is optional, that means you will need to add the client into your setup as well and this way making it available to use.

```shell
$ pip install lilya[cli]
```

Now that the client is made available and installed, we can invoke the power of Lilya to generate a simple project for us. When I say simple project, I actually mean it since you can also generate a more structured type of project using some flags.

This can be found in more detail in the directives section of the documentation.

So, let us then generate a quick project in a matter of seconds by running:

```shell
lilya createproject myproject
```

We call `myproject` to the generated code from Lilya and since the structure of the project is simple, it will look like this:

```Makefile
.
├── Makefile
├── myproject
│   ├── app.py
│   ├── __init__.py
│   └── tests
│       ├── conftest.py
│       ├── __init__.py
│       └── test_app.py
└── requirements
    ├── base.txt
    ├── development.txt
    └── testing.txt
```

Pretty cool, right? Well, this saves you a lot of time already since it generates some initial simple structure for you containing requirements for development, testing and the base as well as a simple project `app.py` and some testing module.

If you open the `app.py` you will see a ready application already assembled.

```python
#!/usr/bin/env python
import uvicorn

from lilya.apps import Lilya
from lilya.requests import Request
from lilya.responses import Ok
from lilya.routing import Path


def welcome():
    return Ok({"message": "Welcome to Lilya"})


def user(user: str):
    return Ok({"message": f"Welcome to Lilya, {user}"})


def user_in_request(request: Request):
    user = request.path_params["user"]
    return Ok({"message": f"Welcome to Lilya, {user}"})


app = Lilya(
    routes=[
        Path("/", welcome),
        Path("/{user}", user),
        Path("/in-request/{user}", user_in_request),
    ]
)


if __name__ == "__main__":
    uvicorn.run(app, port=8000)%
```

Simple application containing some endpoints ready to be used and ready to start the application.

As you can also already see is that magic is happening. You are not required to pass mandatory parameters in the view, instead, Lilya tries to auto-discover and pass those for you in a simple fashion.

### Starting the development environment

Since we have generated a simple [Lilya][lilya] project, we can take advantage of the generated files and we can use another directive from Lilya to start the project.

```shell
make run
```

This `make` command simply runs the following:

```shell
python ./myproject/app.py
```

Since the `app.py` uses `uvicorn`.

```python
if __name__ == "__main__":
    uvicorn.run(app, port=8000)
```

The project can be started like this **but this is not the directive that it was referred to**.

Lilya provides you with a `runserver` directive. This directive, for development purposes, uses `uvicorn` but it is not mandatory to be used. So, let us start the project using that.

Going to the newly generated `myproject` and with the requirements installed.

```shell
lilya runserver
```

And you should see something like this:

```shell
─────────────────────── Starting development server @ localhost ───────────────────────
INFO:     Will watch for changes in these directories: ['/home/<YOUR-USER>/myproject']
INFO:     Uvicorn running on http://localhost:8000 (Press CTRL+C to quit)
INFO:     Started reloader process [55698] using StatReload
INFO:     Started server process [55700]
INFO:     Waiting for application startup.
INFO:     Application startup complete.
```

Now you are ready and with your development server up and running and you can access the provided endpoints.

* http://localhost:8000/
* http://localhost:8000/foobar
* http://localhost:8000/in-request/foobar


And just like that, in a matter of minutes not only you have a ready to go project as well as ready to play endpoints saving you a lot of time.

There are more available directives that can be used for your development and those can be accessed via:

```shell
lilya --help
```

And the official [documentation for directives](https://www.lilya.dev/directives/directives/) where goes into a deeper detail.

## Middleware

Lilya, like almost everything also comes with middlewares and ways of developing custom middlewares.

This can be particularly useful for any application that needs to implement some sort of security level development amongst other things.

Using the middlewares in Lilya is also very simple. You will need to use the **DefineMiddleware** or **Middleware** that can be imported
from the `lilya.middleware` module.

```python
from lilya.apps import Lilya
from lilya.middleware import DefineMiddleware
from lilya.middleware.httpsredirect import HTTPSRedirectMiddleware
from lilya.middleware.trustedhost import TrustedHostMiddleware


app = Lilya(
    routes=[...],
    middleware=[
        DefineMiddleware(
            TrustedHostMiddleware,
            allowed_hosts=["example.com", "*.example.com"],
        ),
        DefineMiddleware(HTTPSRedirectMiddleware),
    ],
)
```

Now, the cool thing about this is that Lilya uses the Python protocols to define the middlewares and this
is a good practice since allows you to design with structure and precision any desired logic that should be placed in the middleware.

```python
from typing import Any, Dict

from lilya.protocols.middleware import MiddlewareProtocol
from lilya.types import ASGIApp, Receive, Scope, Send


class SampleMiddleware(MiddlewareProtocol):
    def __init__(self, app: "ASGIApp", **kwargs):
        """SampleMiddleware Middleware class.

        The `app` is always enforced.

        Args:
            app: The 'next' ASGI app to call.
            kwargs: Any arbitrarty data.
        """
        super().__init__(app)
        self.app = app
        self.kwargs = kwargs

    async def __call__(self, scope: "Scope", receive: "Receive", send: "Send") -> None:
        """
        Implement the middleware logic here
        """
        ...


class AnotherSample(MiddlewareProtocol):
    def __init__(self, app: "ASGIApp", **kwargs: Dict[str, Any]):
        super().__init__(app, **kwargs)
        self.app = app

    async def __call__(self, scope: "Scope", receive: "Receive", send: "Send") -> None:
        await self.app(scope, receive, send)
```

Then you simply use it in your application.

```python
from lilya.apps import Lilya
from lilya.middleware import DefineMiddleware
from myapp.middleware import SampleMiddleware, AnotherSample


app = Lilya(
    routes=[...],
    middleware=[
        DefineMiddleware(SampleMiddleware),
        DefineMiddleware(AnotherSample),
    ],
)
```

Lilya tries to keep the syntax as clean and consise as possible, after all,
one of the biggest issues in software engineering is maintainability, right?

## Permissions

This is another great out-of-the-box. Contrary to other ways of designing permissions, Lilya simplifies the process in every way possible creating what we called the **Pure ASGI Permission**. Now this concept might not be officially out there but Lilya creates it to make it simpler.

The design of a permission in Lilya is literally the same as a middleware. That means, receives an `ASGI app` as parameter and returns an `ASGI app` as well or throws a `PermissionDenied` exception otherwise.

> So why permissions instead of putting everything in a middleware?

Well, that would be a great valid question and the answer is simple. Because Lilya pushes for the *seperation of concerns and responsabilities*, meaning, what is middleware, should be declared in a middleware object and what is roles and permissions, in a roles and permissions object.

The permissions are checked **after the middlewares and before reaching the handler**.

Using the permissions in Lilya is also very simple. You will need to use the **DefinePermission** or **Permission** that can be imported
from the `lilya.permissions` module.

```python
from lilya.apps import Lilya
from lilya.exceptions import PermissionDenied
from lilya.permissions import DefinePermission
from lilya.protocols.permissions import PermissionProtocol
from lilya.requests import Request
from lilya.responses import Ok
from lilya.routing import Path
from lilya.types import ASGIApp, Receive, Scope, Send


class AllowAccess(PermissionProtocol):
    def __init__(self, app: ASGIApp, *args, **kwargs):
        super().__init__(app, *args, **kwargs)
        self.app = app

    async def __call__(self, scope: Scope, receive: Receive, send: Send) -> None:
        request = Request(scope=scope, receive=receive, send=send)

        if "allow-admin" in request.headers:
            await self.app(scope, receive, send)
            return
        raise PermissionDenied()


def user(user: str):
    return Ok({"message": f"Welcome {user}"})


app = Lilya(
    routes=[Path("/{user}", user)],
    permissions=[DefinePermission(AllowAccess)],
)
```

And like the middleware, creating a permission should use the **PermissionProtocol** object.

```python
from lilya.exceptions import PermissionDenied
from lilya.protocols.permissions import PermissionProtocol
from lilya.requests import Request
from lilya.types import ASGIApp, Receive, Scope, Send


class DenyAccess(PermissionProtocol):
    def __init__(self, app: ASGIApp, *args, **kwargs):
        super().__init__(app, *args, **kwargs)
        self.app = app

    async def __call__(self, scope: Scope, receive: Receive, send: Send) -> None:
        raise PermissionDenied()


class AllowAccess(PermissionProtocol):
    def __init__(self, app: ASGIApp, *args, **kwargs):
        super().__init__(app, *args, **kwargs)
        self.app = app

    async def __call__(self, scope: Scope, receive: Receive, send: Send) -> None:
        request = Request(scope=scope, receive=receive, send=send)

        if "allow-admin" in request.headers:
            await self.app(scope, receive, send)
            return
        raise PermissionDenied()
```

## Exception handlers

Natively, Lilya allows you to place exception handler in every component of the application, for instance in the Include, Path, WebsocketPath, Router… and so on.

This means that you don't need to place all of the custom exception handlers in the top of the application and make it very combersome to read and maintain, instead, you might want to split them by responsability and uniqueness.

In a nutshell, you can do something like this:

```python
from json import loads

from lilya import status
from lilya.apps import Lilya
from lilya.requests import Request
from lilya.responses import JSONResponse
from lilya.routing import Include, Path


async def handle_type_error(request: Request, exc: TypeError):
    status_code = status.HTTP_400_BAD_REQUEST
    details = loads(exc.json()) if hasattr(exc, "json") else exc.args[0]
    return JSONResponse({"detail": details}, status_code=status_code)


async def handle_value_error(request: Request, exc: ValueError):
    status_code = status.HTTP_400_BAD_REQUEST
    details = loads(exc.json()) if hasattr(exc, "json") else exc.args[0]
    return JSONResponse({"detail": details}, status_code=status_code)


async def me():
    return "Hello, world!"


app = Lilya(
    routes=[
        Include(
            "/",
            routes=[
                Path(
                    "/me",
                    handler=me,
                    exception_handlers={
                        ValueError: handle_value_error
                    }
                )
            ],
            exception_handlers={
                TypeError: handle_type_error,
            },
        )
    ],
)
```

How awesome is this? The level of granularity and control you can have with Lilya is unbelievable.

No more bloated instances with 300 types of handlers to manage an application, instead, split them by responsibility.

A lot more can be done and checked in the exception handlers part of the documentation.

## Routing system

Well, this is where the magic happens right? The power of the routing system and the modularity that brings to your application.

Lilya comes with a powerful and yet simple routing system that makes all the magic happen for you, specially the unique **Include**.

We could go through all of the components of the routing system but that would require another two or three articles (nothing like in the future can't be done) but lets us focus on an essencial one, the **Include**.

This object itself allows you to add routes via imports and namespaces, via patterns and lists. Also allows you to import external WSGI/ASGI applications with the help of the **WSGIMiddleware** provided by Lilya.

Do you understand what that means? Means you can still maintain your old legacy Django, Flask, FastAPI… whatever project you have inside Lilya while developing brand new systems in Lilya with the help of a simple couple of lines of code.

Amazing? I do think so.

So what does the Include bring?

* Scalability without issues.
* Clean routing design.
* Separation of concerns.
* Separation of routes.
* Reduction of the level of imports needed through files.
* Less human lead bugs.

Let us see how it would look like then.

### Importing routes using the namespace

```python
from lilya.routing import Include


route_patterns = [
    Include(namespace="myapp.accounts.urls"),
]
```

This means that it will go to a `myapp.accounts` module you might have and opens the urls and looks for a
default `route_patterns` to import all the declared paths.

### Importing using the classic `import` system

```python
from myapp.accounts.urls import route_patterns

from lilya.routing import Include


route_patterns = [
    Include("/", routes=route_patterns),
]
```
This comes without surprise, after all this is what the general frameworks allows you to do as well.

What if you want to also import an `ASGI` or `WSGI` application using a string instead of the direct object itself? The Include also allows you to do that.

```python
from lilya.routing import Include

# There is an app in the location `myapp.asgi_or_wsgi.apps.child_lilya`

route_patterns = [
    Include(
        "/child",
        app="myapp.asgi_or_wsgi.apps.child_lilya",
    ),
]
```

Can you imagine how clean your codebase can be? Also, the Include allows nested imports, which means you can have an Include inside another Include that is inside another Include…. You get the gist.
This is nothing, there are so many things you can do with the Include that this article cannot cover it all but the [documentation for the Include](https://www.lilya.dev/routing/#include) does.

## Encoders

Now we come to one of the most powerful functionalities of Lilya (well, there are so many that makes it almost impossible to classify it).

What is the encoder? Well, let me start by giving you some context. FastAPI is built on top of Starlette and Pydantic, which means, its prepared to handle with almost all things Pydantic there. Esmerald on the other hand, its built on top of Lilya, Pydantic and MsgSpec, which means it also supports both Pydantic and MsgSpec out of the box.

Until here, all good, right? Well, **Lilya is not tight to any of those validation libraries** at all but** allows you to create your custom encoder** and make it unique to you.

What if you don't want to use Pydantic or MsgSpec for your validations? Instead you would prefer something like attrs or marshmallow? It is perfectly acceptable that the choice should be yours and not the toolkit, right? Well, Lilya brings you some gifts then.

An encoder is what serializes an object when the response is returned, in other words, it what allows you to returns objects of type X without exploding the response.

Lilya automatically understands how to serialize some Python defaults such as `int, float, list, set, dict, frozenset, deque, dataclass, tuple, None, PurePath and Enum`.

### Custom encoder

Because Lilya believes that future proof is the way to go and the technology should help the developer and not the other way around, it provides you with a way of creating your own "serializers" or in Lilya terms, encoders.

As mentioned before, Lilya is not tight to any validation library, therefore if you were to return, for example, a `msgspec` structure without having your custom encoder, it would explode.

```python
from msgspec import Struct

from lilya.routing import Path


class User(Struct):
    name: str
    email: str


def msgspec_struct():
    return User(name="lilya", url="example@lilya.dev")
```

This is normal, since the `User` is an object of type `Struct` from `msgspec`.

So how can we make sure that the application understand automatically how to handle these types of objects? By creating an encoder, of course.

```python
from typing import Any

import msgspec
from msgspec import Struct

from lilya.encoders import Encoder, register_encoder


class MsgSpecEncoder(Encoder):
    __type__ = Struct

    def serialize(self, obj: Any) -> Any:
        """
        When a `msgspec.Struct` is serialised,
        it will call this function.
        """
        return msgspec.json.decode(msgspec.json.encode(obj))

# Register the encoder in the application

# A normal way
register_encoder(MsgSpecEncoder())

# As alternative
register_encoder(MsgSpecEncoder)
```

This simple. As the documentation states.

> To build a custom encoder you must use the Encoder class from Lilya and override the serialize() function where it applies the serialisation process of the encoder type.
>
Then you must register the encoder for Lilya to use it.
>
>When defining an encoder the `__type__` or `def is_type(self, value: Any) -> bool`: **must be declared or overridden**.
>
> When the `__type__` is properly declared, the default `is_type` will evaluate the object against the type and return `True` or `False`.

> This is used internally to understand the type of encoder that will be applied to a given object.

How simple and powerful is this? Do you realise that from now on, you don't need to rely on a specific framework that handles specific types of validation libraries? You can simply do it yourself in a few lines of code and register it in Lilya and that is it?

This makes Lilya **future proof** because even if a brand new shiny library comes out, you can simply create another encoder and it is ready to go.

### After registering the encoder

Because the encoder was created and registered, the example given will automatically work.

```python
from msgspec import Struct

from lilya.routing import Path


class User(Struct):
    name: str
    email: str


def msgspec_struct():
    return User(name="lilya", url="example@lilya.dev")
```

Now, your Lilya application will understand how to handle the serialization of these types of objects and manage them for you.

Because Lilya also automatically understands some of the defaults, you can even do this.

```python
from msgspec import Struct

from lilya.routing import Path


class User(Struct):
    name: str
    email: str


def msgspec_struct():
    return [User(name="lilya", url="example@lilya.dev")]
```

A lot of magic in some simple lines, right?

[Read more about the encoders](https://www.lilya.dev/responses/#build-a-custom-encoder) and how you can do even more.

## Final thoughts

This article didn't even scratch the surface of what Lilya can do for you but shows already why the future is shiny for Lilya and how you can think elegantly, modularly and cleanly.

I could not cover all the great features of Lilya in one article but there are plenty to choose from like the settings system and modules to the controllers and responses.

The motivation to take Esmerald to the next level brough Lilya to you and a lot more tools created by Dymmond, so don't miss out, join us with any contribution (code-wise, stars, whatever you feel like it).

I hope you enjoyed this little nugget.

{!> ../docs_src/shared/external_links.md !}

[lilya]: https://lilya.dev
[esmerald]: https://esmerald.dev
