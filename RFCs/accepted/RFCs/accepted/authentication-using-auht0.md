- Start Date: 2022-02-22
- Members: [@mateocostab, @iam-oov]
- RFC PR:

# Summary

# How will we be managing User Authentication?

We’ll be using Auth0 by request of our Tech Leads.  

# What is Auth0?

“Auth0 is a flexible, drop-in solution to add authentication and authorization services to your applications.” 

Auth0 also covers one of the project’s requirements for User Authentication, the algorithm we have to use to sign JWTs: RS256 (RSA Signature with SHA-256).

# What information should we ask users?

We are building a platform for people searching for a place to stay and hosts who have a place for them. So considering the above and for safety of both, we need several personal data, such as:

Legal name*
Profile photo
Gender
Date of birth
Email address*
Phone number*
Government ID*
Address*
Emergency contact

* mandatory

# What information does Social Login give us?

It may vary from each provider, for example, Twitter doesn’t share the user email address.


# What social networks will be able to login?

Use Auth0 for user authentication with social login such as Facebook, Google and Apple to automatically get name, gender, birthday, profile picture, email. 


How do we store the tokens? How soon should a session expire?

In addition to control token expirations through the authentication service.

# Basic example

### Obtaining and using refresh tokens

**Packages:**
- `express-openid-connect` which is an Auth0-maintained OIDC-compliant library for Express.

```javascript
app.use(
  auth({
    authorizationParams: {
      response_type: 'code',
      audience: 'https://api.example.com/products',
      scope: 'openid profile email offline_access read:products',
    },
  })
);

app.get('/', async (req, res) => {
  let { token_type, access_token, isExpired, refresh } = req.oidc.accessToken;
  if (isExpired()) {
    ({ access_token } = await refresh());
  }
  const products = await request.get('https://api.example.com/products', {
    headers: {
      Authorization: `${token_type} ${access_token}`,
    },
  });
  res.send(`Products: ${products}`);
});
```

### Store JWT in a Cookie

**Packages:**
- `cookie-parser` it’s an express middleware that allows us to parse cookies on incoming requests.

```javascript
app.get('/jwt', (req, res) => {
  const token = jsonwebtoken.sign({ user: 'johndoe' }, jwtSecret);
  res.cookie('token', token, { httpOnly: true });
  res.json({ token });
});
```

> Note: The `httpOnly: true` setting means that the cookie can’t be read using JavaScript but can still be sent back to the server in HTTP requests.

# Motivation

```sh
Why use short JWT expiration times?

> So that any leaked JWTs become invalid fairly quickly.
> Also implement a silent update workflow that keeps refreshing the JWT token in the background.
```

```sh
Why save JWTs in the browser memory (React State)?

> Because putting the JWT in a cookie doesn’t completely remove the risk of token theft.
> Even with an HttpOnly cookie, sophisticated attackers can still use XSS and CSRF
> to steal tokens or make requests on the user’s behalf.
```

# Detailed design

(This is the bulk of the RFC. Explain the design in enough detail for somebody
familiar with React to understand, and for somebody familiar with the
implementation to implement. This should get into specifics and corner-cases,
and include examples of how the feature is used. Any new terminology should be
defined here.)

# Drawbacks

- The cost of implementation in terms of knowledge. The learning curve, being a first attempt, can be very long.

- Reading and learning Auth0 will require a lot of time.

- We still do not understand the scale.

# Alternatives

```sh
- Make the token expire too long.

> PRO: It would reduce the learning curve by not having to create the update in silent mode.
> CON: Site security would be compromised.
```

```sh
- Persist token

> PRO: It would reduce the learning curve by not having to implement a more complex solution when the user closes and reopens the browser.
> CON: Site security would be compromised.
```

# Adoption strategy

- Implementing too short times in the JWTs will cause all frontends of all teams to adopt this proposal.

# How we teach this

- Document the resulting code by means of a Readme.md 

# Unresolved questions

- Force logout, aka Logout of all sessions/devices.


