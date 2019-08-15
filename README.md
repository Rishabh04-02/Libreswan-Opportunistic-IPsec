# Libreswan-Opportunistic-IPsec
> Libreswan Opportunistic IPsec using LetsEncrypt

`letsencrypt` invokes several of the utilities involved in controlling the Opportunistic Encryption system, running the specified {command} with the specified [argument] as if it had been invoked directly. The command creates a secure Opportunistic Connection between the hosts commonly referred to as client and server. The client connects to the server and remains anonymous, whereas the server is authenticated before connecting to it. The server is not anonymous. The server uses Let's Encrypt certificates for authentication and encryption purposes.

e.g. `ipsec letsencrypt --help` lists the available commands.

It is a [program](https://github.com/Rishabh04-02/libreswan/tree/master/programs/letsencrypt) in [libreswan](https://github.com/libreswan/libreswan/), which integrates libreswan with Opportunistic Encryption utilities. The script provides various OE functionality e.g. initial OE setup, testing configuration/connection, generating and updating Let's Encrypt certificates. The details about the utilities and using them can be found in the [Documentation](https://libreswan.org/wiki/Documentation:_Libreswan_Opportunistic_IPsec_using_LetsEncrypt). Also, the documentation includes the sample output for each {command} and [argument].

Information regarding the development of the project is available at the [GSoC Project wiki](https://libreswan.org/wiki/Libreswan_Opportunistic_IPsec_using_LetsEncrypt)

## Issues
To create/report an issue visit [Libreswan Issues](https://github.com/libreswan/libreswan/issues).

## License
This project(*Libreswan Opportunistic IPsec*) is Licensed under : [**GNU General Public License v2.0**](https://github.com/libreswan/libreswan/blob/master/LICENSE)
