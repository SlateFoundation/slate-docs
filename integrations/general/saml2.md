## Overview
The SAML2 protocol provides single sign-on between supporting systems. Via SAL, Slate can serve as an
**Identify Provider** (IdP) for other systems, allowing users to access them via their existing Slate
session or directing them to login via Slate if they do not have an existing session.

## Initial setup
### Generate private key and public certificate
Use the `openssl` tool from your terminal to generate a private key first. If you're using Mac OS X or
Linux this tool should already be installed.

```language-shell
user@hostname ~ $ openssl genrsa -out slate-private-key.pem 1024
```

Then, use the private key to generate a public certificate. You will be prompted to fill out several
fields identifying the organization that owns the certificate, example responses are provided below.

```language-shell
user@hostname ~ $ openssl req -new -x509 -key slate-private-key.pem -out slate-public-certificate.pem
```

<pre>
Country Name (2 letter code) [AU]:<strong>US</strong>
State or Province Name (full name) [Some-State]:<strong>Pennsylvania</strong>
Locality Name (eg, city) []:<strong>Philadelphia</strong>
Organization Name (eg, company) [Internet Widgits Pty Ltd]:<strong>MySchool District</strong>
Organizational Unit Name (eg, section) []:<strong>MySchool</strong>
Common Name (e.g. server FQDN or YOUR name) []:<strong>example.org</strong>
Email Address []:
</pre>

### Copy private key and public certificate into Slate configuration
Open `php-config/SSOLoginRequestHandler.config.php` from either your local `php-config` file or
from under the `_parent` tree if you have not yet overridden it. Uncomment and fill out the 3
configuration settings, pasting the contents of your generated private key and public certificate
files.

```language-php
<?php

SSOLoginRequestHandler::$entityDomain = 'example.org';

SSOLoginRequestHandler::$privateKey = '-----BEGIN RSA PRIVATE KEY-----
...
-----END RSA PRIVATE KEY-----';

SSOLoginRequestHandler::$certificate = '-----BEGIN CERTIFICATE-----
...
-----END CERTIFICATE-----';
```

## Configuring a system to use Slate as Identity Provider
If a system supports SAML2, it should provide one or more of the following settings:

* Sign-in URL: <kbd>https://www.example.org/login</kbd>
* Sign-out URL: <kbd>https://www.example.org/logout?return=%2F</kbd>
* Change password URL: <kbd>https://www.example.org/profile/edit</kbd>

You will also need to either upload your public certificate file or input its fingerprint. To obtain
the fingerprint of your certificate, run this command and look for the line starting with **SHA1 Fingerprint=**
near the top of the output:

```language-shell
user@hostname ~ $ openssl x509 -subject -dates -fingerprint -in slate-public-certificate.pem
```