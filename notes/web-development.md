# Web development

## What's a design system?

A common set of patterns, tools, definitions and components that are shared by the all project members:
UX/UI, product, dev team, PM.
Act as a common language between different teams involved in a project.

## Web Cookies

Created to add a session over http communications.

Servers add to any response zero, one or more [Set-Cookie](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Set-Cookie) headers. 
Clients add zero or one [Cookie](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Cookie) headers.

## Definitions

`Session Cookie` is a cookie that is deleted at the end of a session, created using `Max-age=0`.
`Permanent Cookie` is a cookie that expires after a certain amount of time, created using `Max-Age` or `Expires`.

### request example

```http
GET /ping/pong.html HTTP/1.1
Host: www.google.com
Cookie: name=value; name2=value2; name3=value3
```

### response example

```http
HTTP/1.1 200 OK
Host: www.google.com
Set-Cookie: name=value;
Set-Cookie: name2=value2;
Set-Cookie; name3=value3;
```

### Attributes

1. max-age, expires: duration of a cookie
2. HttpOnly: javascript cannot read this cookie
3. Secure: store this cookie only in HTTPS communications.
4. Domain: specifies which host can receive the cookie, if not specified only the current host without subdomains can receive the cookie.
5. Path: limit access to the cookie to a specific url path and subdirectories.
6. SameSite: let's the server specify if cross-origin request can receive a cookie.
  Options:
  - `Strict` cookies are sent only to the site that originated the request.
  - `Lax` same as `Strict` but cookies are provided if user navigates to the cookie's origin.
  - `None` do not block cross-origin cookies. 
  Default value: `Lax`.
