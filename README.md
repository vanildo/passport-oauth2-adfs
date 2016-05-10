# passport-oauth2

General-purpose OAuth 2.0 ADFS authentication strategy for [Passport](http://passportjs.org/).

This module lets you authenticate using OAuth 2.0 in your Node.js applications.
By plugging into Passport, OAuth 2.0 authentication can be easily and
unobtrusively integrated into any application or framework that supports
[Connect](http://www.senchalabs.org/connect/)-style middleware, including
[Express](http://expressjs.com/).

Note that this strategy provides OAuth 2.0 support for ADFS.

## Install

    $ npm install https://github.com/vanildo/passport-oauth2-adfs.git

## Usage

#### Configure Strategy

The OAuth 2.0 authentication strategy authenticates users using a third-party
account and OAuth 2.0 tokens.  The provider's OAuth 2.0 endpoints, as well as
the client identifer and secret, are specified as options.  The strategy
requires a `verify` callback, which receives an access token and profile,
and calls `done` providing a user.

    passport.use(new OAuth2Strategy({
      authorizationURL: 'https://adfsServer/adfs/oauth2/authorize',
      resource: 'https://app/auth/sso/callback',
      tokenURL: 'https://adfsServer/adfs/oauth2/token',
      clientID: 'CLIENT_ID',
      clientSecret: 'EXAMPLE_CLIENT_SECRET',
      callbackURL: 'https://app/auth/sso/callback'
    },
      function(accessToken, refreshToken, profile, done) {
        User.findOrCreate({ exampleId: profile.id }, function (err, user) {
          return done(err, user);
        });
      }
    ));

#### Authenticate Requests

Use `passport.authenticate()`, specifying the `'oauth2'` strategy, to
authenticate requests.

For example, as route middleware in an [Express](http://expressjs.com/)
application:

    app.get('/auth/example',
      passport.authenticate('oauth2'));

    app.get('/auth/example/callback',
      passport.authenticate('oauth2', { failureRedirect: '/login' }),
      function(req, res) {
        // Successful authentication, redirect home.
        res.redirect('/');
      });

## Related Modules

- [passport-oauth1](https://github.com/jaredhanson/passport-oauth1) — OAuth 1.0 authentication strategy
- [passport-http-bearer](https://github.com/jaredhanson/passport-http-bearer) — Bearer token authentication strategy for APIs
- [OAuth2orize](https://github.com/jaredhanson/oauth2orize) — OAuth 2.0 authorization server toolkit

## Tests

    $ npm install
    $ npm test

## Credits

  - [Vanildo Vanni](http://github.com/vanildovanni)

## License

[The MIT License](http://opensource.org/licenses/MIT)
