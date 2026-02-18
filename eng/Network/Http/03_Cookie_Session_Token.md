# Cookie, Session, and Token

<br>

### Cookie

- Using cookies, the server can store data in the browser (to remember user information!)
- The browser sends the corresponding cookie along with every request to the server
  - However, cookies are restricted per domain (cookies given by YouTube are only sent to YouTube)
- Cookies have an expiration period, and they are valid according to the period set by the server
- Cookies can provide various information beyond just authentication
  - ex) Language settings

<br>

### Session

-
  - HTTP is `stateless`
    - Every request to the server is handled independently from previous requests
    - Once a request is complete, the server forgets who made the request
    - Therefore, we need to identify ourselves with every request
    - One way to do this is through Sessions
  - How Sessions work
    - When logging in, the server creates the user in a `Session DB`
      - Each session has a separate ID
    - The session ID is returned to the browser via a cookie and stored
    - Every time a page is navigated on the website, the browser sends the cookie containing the session ID to the server
      - (Because cookies are sent automatically~)
    - The server looks at the incoming cookie and checks the cookie that comes with the Session ID
    - The server uses the session ID to look up the `session DB` and finds out the user's information
      - This means the session DB must be queried with every request (potential for overhead)
  - When navigating to a different page on the website, the entire process above is repeated
  - The important thing to remember is that all `important user information` is on the server
    - The user only holds the session ID
  - Cookies are merely a medium for delivering the session ID
  - You can build iOS and Android apps using sessions, but cookies only exist in browsers, so they cannot be used
    - In this case, `Token` is used!

<br>

### JWT

- JWT is a token format
- If user authentication is handled with JWT, there is no need to have a session DB, and the server doesn't need to do much for user authentication!
- `How it works`
  - When a user sends login information to the server and the information is valid, the server does not create anything in the DB
  - Instead, the server takes the user's ID and signs it using a `Sign algorithm`
  - Then it sends the `Signed Info` (Token) to the user in string format
  - When the user sends the `Signed Info` to the server, the server checks whether the signature (token) is valid, and if it is, the server authenticates the user
- JWT is usually much longer than a session ID
  - Because cookies have space limitations
  - JWT has no space limitations, so it can be very long

<br>

### Difference Between Session and Token

- `Session`
  - In sessions, the server just gives a session ID
  - All information about the session is stored in the session DB
  - When a request comes in, the server simply looks up the session ID in the DB
- `JWT`
  - In JWT, the server stores the information needed to authenticate the user in the token
  - It gives the token to the user
  - When the user requests a page, the server only verifies whether the token is valid

<br>

### Pros and Cons of Session and Token

- `Session`
  - The server stores all information about logged-in users
  - Using this information, new features can be added
    - When you want to kick out a specific user, you can simply delete the session
  - Netflix uses the session DB to limit the number of account users (force logout if more than 4)
- `JWT`
  - When using JWT, the created token is not tracked
  - All the server knows is whether the token is valid or not
  - Authentication with JWT eliminates the need for a session DB, but features like forced logout cannot be implemented
    - Because the token remains valid until it expires
