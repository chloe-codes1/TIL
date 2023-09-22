# Request and Response Objects

> Django uses request and response objects to pass state through the system.

<https://docs.djangoproject.com/en/3.0/ref/request-response/>

<br>

### Overview

- Django creates an **HttpRequest** (contains metadata about the request) object when a page is requested
- Django loads the appropriate view, passing the **HttpRequest** as the first argument to the view function
  - Each view is responsible for returning an **HttpResponse** objec

<br>

<br>

## HttpRequest objects

> class HttpRequest

<br>

### Attributes

<br>

#### HttpRequest.method

- A string representing the HTTP method used in the request.
- This is guaranteed to be uppercase.

ex)

```python
if request.method == 'GET':
    do_something()
elif request.method == 'POST':
    do_something_else()
```

<br>

#### HttpRequest.FILES

- A dictionary-like object containing all uploaded files.
  - Each key in FILES is the name from the `<input type="file" name="">`.
  - Each value in FILES is an **UploadedFile**.

- FILES will only contain data if the request method was POST and the `<form>` that posted to the request had `enctype="multipart/form-data"`.
  - Otherwise, FILES will be a blank dictionary-like object.

<br>

<br>

## HttpResponse objects

> class HttpResponse

<br>

- In contrast to **HttpRequest** objects, which are created automatically by Django, **HttpResponse** objects are your responsibility.
  - Each view you write is responsible for instantiating, populating, and returning an **HttpResponse**.

- The **HttpResponse** class lives in the **django.http** module.

<br>

<br>

## HttpResponse subclasses

<br>

### class HttpResponseBadRequest

- Acts just like HttpResponse but uses a 400 status code.

<br>

### class HttpResponseNotFound

- Acts just like HttpResponse but uses a 404 status code.

<br>

### class HttpResponseForbidden

- Acts just like HttpResponse but uses a 403 status code.

### class HttpResponseNotAllowed

- Like HttpResponse, but uses a 405 status code.
- The first argument to the constructor is required: a list of permitted methods (e.g. ['GET', 'POST']).

<br>

<br>

`+`

### Monolithic Architecture란?

:

- 장점
  - 하나에 다있으니까 빠르게 개발 가능
- 단점
  - 확장이 어려움
