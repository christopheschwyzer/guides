Mobile Web Development
======================
Tips for developing and debugging web applications on mobile phones.

Accessing Vagrant VMs from your phone
-------------------------------------
When using the *landrush* DNS plugin for Vagrant the PC's IP address can be configured as the DNS server of the phone.
This way websites running in a VM on a PC can be accessed from the phone.

See [proxy-mobile docu](https://github.com/phinze/landrush/tree/master/doc/proxy-mobile) (a *bind* DNS server is installed with [osx-setup](https://github.com/cargomedia/osx-setup/blob/master/deploy/resource/osx/files/_default/usr/local/etc/named.conf)).

Self-signed SSL certificates
----------------------------
Refer to [cargomedia-ca](https://github.com/cargomedia/cargomedia-ca#install-the-root-certificate) on how to install an SSL CA on a mobile device.
