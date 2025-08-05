# Flask Routes

> Started studying Flask with kendra-button project
>
> [Docs](https://pythonbasics.org/flask-tutorial-routes/)

<br>

## Route

- Receives URL patterns and executes registered Python methods when requests come in for URLs matching those patterns
  - Finding handler methods to process through URLs like this is called **URL Routing**!
  - To generate corresponding URLs in handlers, use the `url_for` method

<br>

### flask route example

- Flask routes are connected to Python functions

- Use the `@app.route()` decorator to connect URLs and functions

  ex)

  ```python
  @app.route('/hello')
  def hello_world():
     return "hello world!!!!"
  ```

<br>

### flask route params

- You can create routes with parameters

- You can pass `string` and `number` types as parameters

  ex)

  > string parameter

  ```python
  @app.route('/member/<name>')
  def get_member(name):
    return "Thank you for joining us " + str(name)
  ```

  > number parameter

  ```python
  @app.route('/sale/<transaction_id>')
  def get_sale(transaction_id=0):
    return "The transaction is "+str(transaction_id)
  ```

<br>

### flask route multiple arguments

- You can also create flask routes with multiple parameters

  ex)

  ```python
  @app.route('/create/<first_name>/<last_name>')
  def create(first_name=None, last_name=None):
    return 'Hello ' + first_name + ',' + last_name
  ```

<br>

<br> 
