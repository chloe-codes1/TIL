# Session and Cookies

<br>

### HTTP Protocol

- `client` makes a **request** to the `server`
- `server` processes the request and sends a **response** to the `client`
- After **responding**, the connection is released >> `STATELESS`
  - The connection is released to reduce resource waste from persistent connections
    - However, problems arise when the `client` and `server` need to maintain a connection state (ex. storing login info, etc.)
    - So **Cookie** and **Session** are used when information needs to be maintained on a per-`client` basis!!

<br>

![image-20200421025031089](../../kor/Network/images/image-20200421025031089.png)

<br>

### Session & Cookies in Java

|                  | Session                                                      | Cookie                                                       |
| ---------------- | ------------------------------------------------------------ | ------------------------------------------------------------ |
| Type             | javax.servlet.http.HttpSession (`interface`)                 | javax.servlet.http.Cookie (`Class`)                          |
| Storage Location | Stored as **Object** in `server` memory<br>(can reference user-defined classes) | Stored as **file** on the `client`'s computer                |
| Storage Format   | Any **Object** is possible <br>(typically Dto, List, etc.)   | **String** format since stored as a **file**                 |
| Usage Examples   | User info on Log-In / Shopping cart                          | Recently viewed list / ID saving (auto-login) / 'Don't show again today' in pop-up menus |

- Commonalities
  - Stored globally, so accessible from all **JSPs** within the project
  - Managed in **Map** format, so duplicate `key values` are not allowed

<br>
