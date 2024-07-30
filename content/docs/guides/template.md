---
title: "Use Template Engine on Fubuki"
description: "Guide on how to use Jinja2 and Mako template engine with Fubuki"
lead: "Learn how to use the Fubuki to generate HTML responses with the Jinja2 and Mako template engines."
date: 2024-07-30T00:00:00+00:00
lastmod: 2024-07-30T00:00:00+00:00
draft: false
images: []
---

## Use Template Engine on Fubuki
This guide explains how to use the Fubuki to generate HTML responses with the Jinja2 and Mako template engines.

### 1. create template files

For example, create a template file named `index.html` in the `templates` directory.

#### When using Jinja2
```html
<!-- templates/index.html -->
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>{{ title }}</title>
</head>
<body>
    <h1>{{ message }}</h1>
</body>
</html>
```
#### When using Mako
```html
<!-- templates/index.html -->
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>${title}</title>
</head>
<body>
    <h1>${message}</h1>
</body>
</html>
```
### 2. using Jinja2

The following is an example of a simple application that returns a response using the Jinja2 template.

```python
from fubuki import Fubuki, get
from fubuki.template import TemplateResponse

app = Fubuki()

class MyController:.
    @get("/")
    async def jinja2_index():
        context = {
            "title": "Hello, Jinja2!
            "message": "This is a message from Jinja2 template."
        }
        return TemplateResponse("index.html", context, engine="jinja2")

app.add_route(MyController)

if __name__ == "__main__": app.run()
    app.run()
```

### 3. using Mako

The following is an example of a simple application that returns a response using the Mako template.

```python
from fubuki import Fubuki, get
from fubuki.template import TemplateResponse

app = Fubuki()

class MyController:.
    @get("/")
    async def mako_index():
        context = {
            "title": "Hello, Mako!""
            "message": "This is a message from Mako template.""
        }
        return TemplateResponse("index.html", context, engine="mako")

app.add_route(MyController)

if __name__ == "__main__": app.run()
    app.run()
```

### 4. Execution
Next, run the Fubuki application by executing the following command.
```
$ python app.py
```
### 5. confirmation
After launching, check if the contents are rendered by accessing http://127.0.0.1:8000/.

### 6. Use templates in directories other than `templates`
The Fubuki framework can refer to a template in another directory by specifying an argument to `TemplateResponse`.

Below is an example of how to do this.
```python
from fubuki import Fubuki, get
from fubuki.template import TemplateResponse

app = Fubuki()

class MyController:
    @get("/")
    async def mako_index():
        context = {
            "title": "Hello, Mako!",
            "message": "This is a message from Mako template."
        }
        return TemplateResponse("mako.html", context, engine="mako", tmpl_dir=["html"])

app.add_route(MyController)

if __name__ == "__main__":
    app.run(host="0.0.0.0", port=8001)
```
#### Restriction
* Due to a limitation of Jinja2, Jinja2 can only retrieve templates from the first directory of a list if a List type is passed.
* Mako does not have the above limitation.