# Goals

1. [ ] Creating a server
2. [ ] Creating a user
3. [x] Encoding request
4. [x] Decoding request
5. [ ] Validating a request (checking header etc.)

## Setting up auth server:
* [ ] /register
  * username
  * password
  * store new user
  * return token
* [ ] /login
  * username, password
  * look up user
  * create token
  * return token
* [ ] /logout <-- need a way to cancel token or identify a specific token
  * No such thing :(


## Questions
* [ ] How to share tokens between services
* [x] How to set expiry on tokens
* [ ] How to "logout"/cancel a token
* [ ] Does the token carry each actual request payload or just auth/user info?

## Exercises


# Notes

## About JWT
* Based on Web Standard (RFC7519)
* Used to securely communicate JSON objects
* Consists of header, payload, and signature
* Self-contained
* More flexibility than cookies, which are browser only
* Spec is pretty accessible: https://tools.ietf.org/html/rfc7519

"It is important to understand that the purpose of using JWT is NOT to hide or obscure data in any way. The reason why JWT are used is to prove that the sent data was actually created by an authentic source." - [source](https://medium.com/vandium-software/5-easy-steps-to-understanding-json-web-tokens-jwt-1164c0adfcec)

It is possible to encrypt contents as well, see JWE (Json Web Encryption) objects, see https://github.com/cisco/node-jose for more

### More background
* JWTs are not signed/encrypted themselves
  * JSON Web Signatures (JWS) used for signing
  * JSON Web Encryption (JWE) used for encrypting
  * For our purposes, JWT refers to all three technologies
* Can be used with public/private keypairs also
* Can also be used for parallel/multiple signers (see JWS-JS)
* **Allows for different issuers**: Services A, B, and C can issue tokens and Services X, Y, and Z can process them (assuming they all share the signing secret)

### Advantages
* compact (compared to XML)
* printable (string)
* easy to sign (compared to XML), also fewer potential security issues
* JSON Widely supported across languages

### How to store/deliver

Doesn't really matter, depends mostly on what works for your application.

#### HTTP `Bearer` header
* Put it in an HTTP header
* **Works for browser and any other HTTP client**
* Browser: store it on the client in `localStorage` 
* Potentially vulnerable to XSS: if someone can inject a script on your site they could theoretically read keys out of local storage.

#### Cookie
* **Browser only**
* Good if you're only processing requests from Browsers.
* Relies more directly on built-in browser technology (browsers already know to pass cookies without being told)
* Useful if you're building a tracking bug or something.
* Cookies, when used with the `HttpOnly` cookie flag, are not accessible through JavaScript, and are immune to XSS. You can also set the Secure cookie flag to guarantee the cookie is only sent over HTTPS.
* Can still be stateless on server, as server checks token each time (does not need to keep track of session)
* Can be vulnerable to CSRF (sending a request to `twitter.com` from `evilsite.com`, if you're logged into twitter it will pass your cookie). Most modern frameworks have CSRF mitigation features.

## Parts of JWT

### Header ("JOSE" header)

*JOSE = JavaScript Object Signing & Encryption*

(Usually) two keys:

* `typ`: Type of claim (JWT, JWA, JWE). Useful when the claim could be of different types (not in our case)
* `alg`

```js
{
  "typ" : "JWT",
  "alg": "HS256"
}
```

### Payload

* **public claims**: user-defined attributes
  * user
  * permissions?
  * etc.
* **reserved claims**: defined by standard
  * `iss`: issuer: who issued this token? (usually a URI)
  * `sub`: subject: whom does this token refer to? (user id, email etc. – must be *unique*)
  * `aud`: audience: what service(s) is this token for? Optional, but if present, services processing the claim **must** identify themselves with an `aud` value, and if the service's value is not in the tokens `aud` list, it **must** reject the token. Typically an array of case-sensitive strings or URIs.
  * `exp`: expiration time. Numeric date value. If present, services processing the claim **must not** accept accept the token after that time.
  * `nbf`: not before: like `exp` but reverse. Don't accept *before* this time
  * `iat`: Issued at: used to determine age of token
  * `jti`: 
* *Notice that the claim names are only three characters long as JWT is meant to be compact.*
* standard impl of commonly used claims
* allow for interop, SSO, etc.

```js
{
  "iss": "http://api.example.com",  // reserved claim
  "user": "sequoia"                 // public claim
}
```

### Signature

**Encoded header and payload signed with a secret.**

* Sender and receiver can decrypt payload, no one else
* ~~Secret is shared between client and server~~
* Secret is on server, client cannot decrypt payload (nor do they need to)

Encoding + Encrypting allows you to:
1. Prove identity of sender (identity)
2. Ensure message has not changed (integrity)

Signature:

```
HMACSHA256(
  base64UrlEncode(header) +
  "." +
  base64UrlEncode(payload),

  secret
)
```

### Encoded claim
* TODO: How are header & payload encoded?
* [encoded header].[encoded payload].[signature]
* e.g. `als7ut983247oasjdl.laskjdfaksd.kjqwlkjqlwkjfklasksg-hvI`

# Demo

* TODO: check out `express-jwt`
* TODO: check out `jsonwebtoken`

## Before

```js
function auth(user, pass){
  user = db.lookup(user.id);
  return user.pass === pass;
}
```

## After

1. Include express-jwt
2. Include `jwt` = jsonwebtoken
3. `app.use(expressJWT({secret:`${SECRET}`}).unless({path:['/login', '/api/restaurants']}))`
4. change login route to return json token
   ```js
   var myToken = jwt.sign({ username: req.body.username, foo:bar }, `${SECRET}`);
   res.status(200).json(myToken); // A STRING
   ```
5. Get the token response in client
6. Subsequent requests, add header:
   `Authorization: 'Bearer ${token}'