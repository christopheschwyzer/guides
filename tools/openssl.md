OpenSSL
=======
If you omit `-out` output defaults to STDOUT

**Convert PFX to key+pem**

```
openssl pkcs12 -in <PFX file> -nocerts -nodes -out <KEY File>
openssl pkcs12 -in <PFX File> -clcerts -nokeys -out <PEM File>
```

**Create key+csr**

```
openssl req -new -newkey rsa:2048 -nodes -keyout <KEY File> -out <CSR File> -subj '/CN=<DOMAIN>/C=<COUNTRY>'
```

**Create key+pem with sha-256 signature** (aka self-signed certificate)

```
openssl req -x509 -nodes -sha256 -days 3650 -newkey rsa:2048 -keyout <KEY File> -out <PEM File> -subj '/CN=<DOMAIN>/C=<COUNTRY>'
```

**Output hash of certificate (used by apache for chain following)**

```
openssl x509 -noout -hash -in <PEM File>
```

**Create new csr based on existing certificate**

```
openssl x509 -x509toreq -in <PEM File> -signkey <KEY file> -out <CSR file>
```
