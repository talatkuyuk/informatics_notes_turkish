> mkdir a-directory
> cd to-this-directory
> in my computer MyCodeRepo/https_cert/CA

#### Step 1: Generate a Certificate Authority (CA) Certificate

**generate a RSA-2048 key and save it to a file rootCA.key**

> openssl genrsa -des3 -out rootCA.key 2048
> _mykeyisimportant_

**generate a root CA certificate**

> openssl req -x509 -new -nodes -key rootCA.key -sha256 -days 3650 -out rootCA.pem

_this certificate is for 10 years._

_now we have two files <CA.key> and <CA.pem>_

#### Step 2: Trust the root SSL Certificate

Open Keychain Access on your Mac and go to the Certificates category in your System keychain. Once there, import the rootCA.pem using File > Import Items. Double click the imported certificate and change the “When using this certificate:” dropdown to Always Trust in the Trust section.

#### Step 3: Generating a Domain SSL Certificate

The root SSL certificate can now be used to issue a certificate specifically for your local development environment located at localhost.

> mkdir localhost
> cd localhost

**create a new OpenSSL configuration file server.csr.cnf**

> touch server.csr.cnf
> open it with TextEdit and edit

```bash
[req]
default_bits = 2048
prompt = no
default_md = sha256
distinguished_name = dn

[dn]
C=US
ST=RandomState
L=RandomCity
O=RandomOrganization
OU=RandomOrganizationUnit
emailAddress=hello@example.com
CN = localhost
```

**create a v3.ext file in order to create a X509 v3 certificate**

> touch v3.ext
> open it with TextEdit and edit

```bash
authorityKeyIdentifier = keyid,issuer
basicConstraints = CA:FALSE
keyUsage = digitalSignature, nonRepudiation, keyEncipherment, dataEncipherment
subjectAltName = @alt_names

[alt_names]
DNS.1 = localhost
IP.1 = 127.0.0.1
```

**create a certificate key for localhost using the configuration settings**

> openssl req -new -sha256 -nodes -out server.csr -newkey rsa:2048 -keyout server.key -config <( cat server.csr.cnf )

_now we have two files <server.key> and <server.csr>_

**create a certificate file**

> openssl x509 -req -in server.csr -CA ../rootCA.pem -CAkey ../rootCA.key -CAcreateserial -days 390 -sha256 -extfile v3.ext -out server.crt

_The certificate could be at most 397 days since chrome restriction._

_now we have the certificate <server.crt> for localhost_

You can move the <server.key> and <server.crt> files to an accessible location on your server.

**if you need to to decrypt the server.key**

> openssl rsa -in server.key -out server.decrypted.key

_Because nodejs, express application needs decrypted._

**if you need to verify the domain certificate against root CA certificate**
openssl verify -CAfile ../rootCA.pem server.crt

### Sources:

https://www.freecodecamp.org/news/how-to-get-https-working-on-your-local-development-environment-in-5-minutes-7af615770eec/

https://www.section.io/engineering-education/how-to-get-ssl-https-for-localhost/

## Postman SSL settings

Settings -> Certificates -> enable CA certificate and select the .pem file.

## VS Code Live Server SSL settings

https://medium.com/webisora/how-to-enable-https-on-live-server-visual-studio-code-5659fbc5542c
https://www.akadia.com/services/ssh_test_certificate.html

- Go to your visual code project.
- Create .vscode folder inside the project. ( Don’t forget the . (period) ).
- Inside that folder create settings.json file.
  Paste the following code:

```json
{
  "liveServer.settings.https": {
    "enable": true, //set it true to enable the feature.
    "cert": "D:\\https\\primary.crt", //full path of the certificate
    "key": "D:\\https\\private.key", //full path of the private key
    "passphrase": "12345"
  }
}
```

## http-server SSL settings

> http-server -S -C server.crt -K server.decrypted.key -a localhost -p 5500
