OpenSSL
=======
If you omit `-out` output defaults to STDOUT

Converting between formats
--------------------------
#### Convert PFX to key+pem
```sh
openssl pkcs12 -in <PFX file> -nocerts -nodes -out <KEY File>
openssl pkcs12 -in <PFX File> -clcerts -nokeys -out <PEM File>
```

#### Convert PEM certificate to DER
```sh
openssl x509 -in 'example.pem' -outform der -out 'example.der.crt'
```

#### Output hash of certificate (used by apache for chain following)
```sh
openssl x509 -noout -hash -in <PEM File>
```

Certificate Signing Requests
----------------------------
#### Create key+csr
```sh
openssl req -new -newkey rsa:2048 -nodes -keyout <KEY File> -out <CSR File> -subj '/CN=<DOMAIN>/C=<COUNTRY>'
```

#### Create new csr based on existing certificate
```sh
openssl x509 -x509toreq -in <PEM File> -signkey <KEY file> -out <CSR file>
```

Self-signed certificates
------------------------
#### Create key+pem
```sh
openssl req -x509 -nodes -sha256 -days 3650 -newkey rsa:2048 -keyout <KEY File> -out <PEM File> -subj '/CN=<DOMAIN>/C=<COUNTRY>'
```

#### Create key+pem with CA and alternative names
```sh
openssl req -x509 -nodes -sha256 -days 3650 -newkey rsa:2048 -keyout <KEY FILE> -out <PEM FILE> -config <CONFIG FILE>
```

Example config file:
```
prompt = no

[req]
req_extensions = v3_req
x509_extensions	= v3_ca
distinguished_name = req_distinguished_name

[req_distinguished_name]
commonName = my-name
countryName = US

[v3_req]
basicConstraints = CA:true
subjectAltName = @alt_names

[v3_ca]
basicConstraints = CA:true
subjectAltName = @alt_names

[alt_names]
DNS.1 = example.dev
DNS.2 = something.dev
```
