## Password Reset functionality

- For testing multiple email ID:
    - `email=victim@tld.xyz&email=victim=attacker@tld.xyz`
    - `email="victim@mail.tld%0a%0dcc:attacker@mail.tld"`
    - `{"email":["victim@mail.tld","atracker@mail.tld"]}`
    - [`user@email.com](mailto:user@email.com)[&bcc:attacker@email.com](mailto:&bcc:attacker@email.com)`
    - [`email=victimspussy@ymail.com](mailto:email=victimspussy@ymail.com)[:attackersdick@ymail.com](mailto::attackersdick@ymail.com)`

- Try to brute force the reset token
- Try to use `attackers` reset code with the `victims` email ID

- Test the password and username field for XSS payload
- Try to inject something like

```
HOST: attacker.com?.original.com
```

It might work because it might not have those checks properly.

## SAML

SAML basically used for providing SSO(single sign-on).

**Ex:** Say there is a service named `[identity.hacker.com](http://identity.hacker.com)` which will authenticate you and then based on that single authentication you'll be able to access `player.superhacker.com`.

```json
The trust relationship works because the Service Provider trusts the Identity Provider. This trust relationship is initially created by providing the certificate (that contains the public key) of the Identity Provider to the Service Provider. If a SAMLResponse is signed with the private key matching the public key in the certificate, the Service Provider will trust the assertion.
```

- IDP can return the response in a base64 encoded XML type looking document, which will contain everything in it like keys used(not the private one), nameID, etc

## Attack

### NameID

- Usually, in the response XML format there is one attribute named `NameID` which basically contains the email id or username of the person who was authenticated.
- Now it's possible that the data is simply going in normal base64 encoding, so we can capture that request, alter that NameID and see if we are able to log in as someone else.

### Signature Stripping

```json
One of the common issues with the protocol using the signature to prevent tampering comes from the fact that the signature is only verified if it is present.
```

This means to says if even after changing the `NameId` the hack doesn't work so you can try to stripe the [`ds:SignatureValue`](ds:SignatureValue) tag's **content**. Remember not the tag but the content inside it.

## JWT

So JSON web token is used for authentication loads of time. It's better to try loads of things with it.

- Sometimes they can forget to even actually check the signature so test that as well
- We can brute force the secret but I think that is just for CTF and stuff. It won't work in real life since mostly JWT used have RSA used

## Null Values

Decode the token and set the encryption/alg to Null it might be possible that could work.

## Improper cryptographic implementation

Say that the `alg` used is `RS256` but it is possible that we can modify the headers to used `HS256`

 and then edit the `payload` as we like. And then for the signature part, we encode that using the HMAC trick.

**PROBLEM** - A person would need the `public key` using which the signature is being verified.
