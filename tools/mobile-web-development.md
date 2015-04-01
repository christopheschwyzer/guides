Mobile Web Development
======================
Tipps for developing and debugging web applications on mobile phones.

Accessing Vagrant VMs from your phone
-------------------------------------
When using the *landrush* DNS plugin for Vagrant the PC's IP address can be configured as the DNS server of the phone.
This way websites running in a VM on a PC can be accessed on the phone. See [proxy-mobile docu](https://github.com/phinze/landrush/tree/master/doc/proxy-mobile).

Self-signed SSL certificates
----------------------------

Create key+cert with v3_req extensions and enabled as a CA:
```sh
openssl req -x509 -nodes -sha256 -days 3650 -newkey rsa:2048 -keyout 'example.key' -out 'example.pem' -subj '/CN=example.com/C=CH' -reqexts v3_req -extensions v3_ca
```

Convert the certificate to DER format:
```sh
openssl x509 -in 'example.pem' -outform der -out 'example.der.crt'
```

Upload the `.der.crt` file to *Google Drive* and install it on your Android Device:
Go to *Settings > Security > Credential storage: Install from storage* and select the certificate.
