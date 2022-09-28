Reference: https://reflectoring.io/spring-boot-cookies/

### Cookie
- Cookie is a piece of information that is stored on client side (for eg browser)
- The client sends them to the server with each request and servers can tell the client which cookies to store.
- Commonly used to track the activity of a website, to customize user sessions, and for servers to recognize users between requests.
- Another scenario is to store a JWT token or the user id in a cookie so that the server can recognize if the user is authenticated with every request.

### How DO Cookies Work ?
Cookies are sent to the client by the server in an HTTP response and are stored in the client (user’s browser).

The server sets the cookie in the HTTP response header named Set-Cookie. A cookie is made of a key /value pair, plus other optional attributes, which we’ll look at later.

Let’s imagine a scenario where a user logs in. The client sends a request to the server with the user’s credentials. The server authenticates the user, creates a cookie with a user id encoded, and sets it in the response header. The header Set-Cookie in the HTTP response would look like this:

![image](https://user-images.githubusercontent.com/59752237/192811041-25c1bde5-eea6-40c4-97b7-9db8f78ba0e2.png)

Once the browser gets the cookie, it can send the cookie back to the server. To do this, the browser adds the cookie to an HTTP request by setting the header named Cookie:

![image](https://user-images.githubusercontent.com/59752237/192811205-95bc9060-1a4d-4613-80de-97d9783c78d2.png)

The server reads the cookie from the request verifies if the user has been authenticated or not, based on the fact if the user-id is valid.

As mentioned, a cookie can have other optional attributes, so let’s explore them.

### Cookie Max-Age and Expiration Date

The attributes Max-Age and/or Expires are used to make a cookie persistent. By default, the browser removes the cookie when the session is closed unless Max-Age and/or Expires are set. These attributes are set like so:

![image](https://user-images.githubusercontent.com/59752237/192811707-64c41d72-4b4a-415c-b2de-4e1b1ad11cfd.png)

This cookie will expire 86400 seconds after being created or when the date and time specified in the Expires is passed.

When both attributes are present in the cookie, Max-Age has precedence over Expires.

### Cookie Domain

Domain is another important attribute of the Cookie. We use it when we want to specify a domain for our cookie:

By doing this we are telling the client to which domain it should send the cookie. A browser will only send a cookie to servers from that domain.

Setting the domain to “example.com” not only will send the cookie to the “example.com” domain but also its subdomains “foo.example.com” and “bar.example.com”.

If we don’t set the domain explicitly, it will be set only to the domain that created the cookie, but not to its subdomains.

### Cookie Path
The Path attribute specifies where a cookie will be delivered inside that domain. The client will add the cookie to all requests to URLs that match the given path. This way we narrow down the URLs where the cookie is valid inside the domain.

Let’s consider that the backend sets a cookie for its client when a request to http://example.com/login is executed:
![image](https://user-images.githubusercontent.com/59752237/192816115-290ec57f-9fc4-4af7-b998-1323f3d7d2c7.png)

Notice that the Path attribute is set to /user/. Now let’s visit two different URLs and see what we have in the request cookies.

When we execute a request to http://example.com/user/, the browser will add the following header in the request:
![image](https://user-images.githubusercontent.com/59752237/192816233-7b2748d1-339b-4752-86e9-39a2245ceee4.png)

As expected, the browser sends the cookie back to the server.

When we try to do another request to http://example.com/contacts/ the browser will not include the Cookie header, because it doesn’t match the Path attribute.

When the path is not set during cookie creation, it defaults to /.

By setting the Path explicitly, the cookie will be delivered to the specified URL and all of its subdirectories.

### Secure Cookie

In cases when we store sensitive information inside the cookie and we want it to be sent only in secure (HTTPS) connections, then the Secure attribute comes to our rescue.
By setting Secure, we make sure our cookie is only transmitted over HTTPS, and it will not be sent over unencrypted connections.

### HttpOnly Cookie

HttpOnly is another important attribute of a cookie. It ensures that the cookie is not accessed by the client scripts. It is another form of securing a cookie from being changed by malicious code or XSS attacks.
Not all browsers support the HttpOnly flag. The good news is most of them do, but if it doesn’t, it will ignore the HttpOnly flag even if it is set during cookie creation. Cookies should always be HttpOnly unless the browser doesn’t support it or there is a requirement to expose them to clients' scripts.


### Same Site Cookie
Reference: https://www.springcloud.io/post/2022-04/spring-samesite/#gsc.tab=0
- Including ways to implement same-site

## Note:
- Keeping the cookie alive after the user logs out can seriously compromise the security.


