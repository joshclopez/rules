Auth0 Rules Repository
=====

[![CircleCI](https://circleci.com/gh/auth0/rules.svg?style=svg)](https://circleci.com/gh/auth0/rules)

Rules are code snippets written in JavaScript that are executed as part of the authentication pipeline in [Auth0](https://www.auth0.com). This happens every time a user authenticates to an application. __Rules__ enable very powerful customizations and extensions to be easily added to Auth0.

![](https://docs.google.com/drawings/d/16W_hTS_u2CeDFXkD2PlfituFl7b74EQ6HE_XYn3TdD0/pub?w=891&h=283)

An App initiates an authentication request to Auth0 (__Step 1__), Auth0 routes the request to an Identity Provider through a configured connection (__Step 2__). The user authenticates successfully (__Step3__), the `user` object that represents the logged in user is then passed through the rules pipeline and returned to the app (__Step 4__).

A rule will run on Step 4 and this is the information each rule will get:

* `user`: the user object as it comes from the identity provider.
* `context`: an object containing contextual information of the current authentication transaction. It has the following properties:
  * `clientID`: the client id of the application the user is logging in to.
  * `client_metadata`: an optional object containing up to 10 key/value pairs
  * `clientName`: the name of the application (as defined on the dashboard).
  * `connection`: the name of the connection used to authenticate the user (e.g.: `twitter` or `some-google-apps-domain`)
  * `connectionStrategy`: the type of connection. For social connection `connectionStrategy` === `connection`. For enterprise connections, the strategy will be `waad` (Windows Azure AD), `ad` (Active Directory/LDAP), `auth0` (database connections), etc.
  * `protocol`: the authentication protocol. Possible values: `oidc-basic-profile` (most used, web-based login), `oidc-implicit-profile` (used on mobile devices and single page apps), `oauth2-resource-owner` (user/password login typically used on database connections), `samlp` (SAML protocol used on SaaS apps), `wsfed` (Ws-Federation used on Microsoft products like Office365), `wstrust-usernamemixed` (Ws-trust user/password login used on CRM and Office365)), `delegation` (during the exchange for a delegation token).
  * `request`: an object containing useful information of the request. It has the following properties:
    * `query`: querystring of the login transaction sent by the application
    * `body`: the body of the POST request on login transactions used on `oauth2-resource-owner` or `wstrust-usernamemixed` protocols.
    * `userAgent`: the user-agent of the client that is trying to log in.
    * `ip`: the originating IP address of the user trying to log in.
  * `samlConfiguration`: an object that controls the behavior of the SAML and WS-Fed endpoints. Useful for advanced claims mapping and token enrichment (only available for `samlp` and `wsfed` protocol).

Note that rules will also have access to several modules defined globally, including `auth0`, referring to https://github.com/auth0/node-auth0. Other modules available within rules are defined at https://auth0.com/docs/appliance/modules (relevant to both appliance and cloud)

This is the rules editor inside Auth0:

![](http://cdn.auth0.com/docs/img/rules-editor.png)

---
### Available Modules

* [Webtask modules](https://tehsis.github.io/webtaskio-canirequire/)
* [Additional modules](https://auth0.com/docs/appliance/modules)

---
### Release Notes

1. Update the markdown files to update the rule and commit your changes
2. Update the version by executing:

 ```bash
 npm version [patch|minor|major]
 ```

 > There is a `preversion` script in the `package.json` file that executes the following command:  `./build && git add rules.json && git commit -m 'update rules.json`

3. Push your changes to master including the tags

 ```bash
 git push origin master --tags
 ```


---

### Highlighted Rules

* Send events to MixPanel [Docs](https://auth0.com/rules/mixpanel-track-event) | [Rule]( https://github.com/auth0/rules/blob/master/src/rules/mixpanel-track-event.js)
* Query User Profile in FullContact [Docs](https://auth0.com/rules/get-FullContact-profile) | [Rule](https://github.com/auth0/rules/blob/master/src/rules/get-fullcontact-profile.js)
* Add a Lead in Salesforce [Docs](https://auth0.com/rules/creates-lead-salesforce) | [Rule](https://github.com/auth0/rules/blob/master/src/rules/creates-lead-salesforce.js)
* Get an Appery Session Token [Rule](https://github.com/auth0/rules/blob/master/src/rules/appery.js)

[More information about them here](https://docs.auth0.com/rules).

## Issue Reporting

If you have found a bug or if you have a feature request, please report them at this repository issues section. Please do not report security vulnerabilities on the public GitHub issue tracker. The [Responsible Disclosure Program](https://auth0.com/whitehat) details the procedure for disclosing security issues.

## Author

[Auth0](auth0.com)

## License

This project is licensed under the MIT license. See the [LICENSE](LICENSE) file for more info.
