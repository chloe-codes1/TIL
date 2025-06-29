# Flask Routes

> kendra-button project에서 Flask 를 써서 공부 시이작
>
> [Docs](https://pythonbasics.org/flask-tutorial-routes/)

<br>

## Route

- URL pattern을 받아 해당하는 pattern의 URL로 request가 들어오면, 등록된 Python method를 실행하게 함
  - 이렇게 URL을 통해 처리할 handler method를 찾는 것을 **URL Routing** 이라고 한다!
  - Handler에서 해당하는 URL을 생성하려면 `url_for` method를 사용한다

<br>

### flask route example

- Flask의 route는 python 함수들과 연결되어 있다

- `@app.route()` decorator를 사용해서 URL과 함수를 연결한다

  ex)

  ```python
  @app.route('/hello')
  def hello_world():
     return "hello world!!!!"
  ```

<br>

### flask route params

- parameter로 route를 만들 수 있다

- parameter로 `string` 과 `number` type을 넘겨줄 수 있다

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

- 여러개의 parameter로도 flask route를 만들 수 있다

  ex)

  ```python
  @app.route('/create/<first_name>/<last_name>')
  def create(first_name=None, last_name=None):
    return 'Hello ' + first_name + ',' + last_name
  ```

<br>

<br>
