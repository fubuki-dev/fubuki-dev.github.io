---
title: "Dynamic Routing"
description: "This guide will explain how to use regular expressions for dynamic routing in Fubuki. By leveraging regular expressions, you can create more flexible and powerful route matching patterns."
slug: "dynamic-routing"
date: 2024-07-30T00:00:00+00:00
lastmod: 2024-07-30T00:00:00+00:00
draft: false
images: []
---
This guide will explain how to use regular expressions for dynamic routing in Fubuki. By leveraging regular expressions, you can create more flexible and powerful route matching patterns.

### Overview

Dynamic routing with regular expressions allows you to capture parts of the URL and use them as parameters in your route handlers. This can be useful for creating routes that handle a wide range of URLs with a single route definition.

### Example Project Structure

For this example, we'll assume the following project structure:

```
.
└── project/
    ├── app/
    │   ├── controllers/
    │   │   └── dynamic.py
    │   └── routes.py
    ├── templates/
    │   └── dynamic.html
    └── main.py
```

### Step 1: Create a Template

Create a template file in the `templates` directory.

#### `templates/dynamic.html`

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Dynamic Routing</title>
</head>
<body>
    <h1>Dynamic Route: {{ dynamic_part }}</h1>
</body>
</html>
```

### Step 2: Define a Dynamic Controller

Create a controller that will handle dynamic routes using regular expressions. Place this file in the `app/controllers` directory.

#### `app/controllers/dynamic.py`

```python
from fubuki import Controller, get, Request
from fubuki.response import JSONResponse
from fubuki.template import TemplateResponse

class DynamicController(Controller):
    @get(r'/dynamic/(?P<dynamic_part>\w+)')
    async def dynamic_route(request: Request, dynamic_part: str):
        context = {
            "dynamic_part": dynamic_part
        }
        return TemplateResponse("dynamic.html", context)
```

### Step 3: Register Dynamic Routes

Define your routes in the `app/routes.py` file. Here, we'll register the `DynamicController`.

#### `app/routes.py`

```python
from app.controllers.dynamic import DynamicController

def setup_routes(app):
    app.add_route(DynamicController)
```

### Step 4: Create the Main Application File

Create the `main.py` file to run your application.

#### `main.py`

```python
from fubuki import Fubuki
from app.routes import setup_routes

app = Fubuki()

setup_routes(app)

if __name__ == "__main__":
    app.run(host="0.0.0.0", port=8000)
```

### Step 5: Run the Application

Navigate to your project directory and run the application using Python.

```bash
cd project_name
python main.py
```

Your application should now be running, and you can access it at `http://localhost:8000/dynamic/somevalue`.

### Explanation

- **Route Definition**: In `app/controllers/dynamic.py`, the `@get` decorator uses a regular expression to define a dynamic route. The `(?P<dynamic_part>\w+)` part captures a word (\w+) from the URL and assigns it to the parameter `dynamic_part`.
- **Template Rendering**: The captured URL part is passed to the template as `dynamic_part`, which is then rendered in `dynamic.html`.

### Summary

This guide covers how to use regular expressions for dynamic routing in Fubuki. By following these steps, you can create flexible and powerful routes that handle a variety of URL patterns.