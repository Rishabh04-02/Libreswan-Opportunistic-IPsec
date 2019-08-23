# Libreswan-Opportunistic-IPsec

Libreswan Opportunistic IPsec using LetsEncrypt is a project created during Google Summer of Code 2019. It adds a utility `letsencrypt` to the `ipsec`. letsencrypt invokes any of several utilities involved in controlling the Opportunistic Encryption system, running the specified {command} with the specified [argument] as if it had been invoked directly.

e.g. `ipsec letsencrypt --help` lists all the available commands.

It is a program in libreswan, which integrates libreswan with Opportunistic Encryption utilities. The script provides various OE functionality e.g. initial OE setup, testing configuration/connection, generating and updating Let's Encrypt certificates. The details about the utilities and using them can be found in the [Documentation: Libreswan Opportunistic IPsec using LetsEncrypt](https://libreswan.org/wiki/Documentation:_Libreswan_Opportunistic_IPsec_using_LetsEncrypt) . Also, the documentation includes the sample output for each {command} and [argument].

Information regarding the development of the project is available at the [GSoC Project wiki](https://libreswan.org/wiki/Libreswan_Opportunistic_IPsec_using_LetsEncrypt)

## Implementations

Various functionalities of the project are listed below:
* Can establish the secure OE (Opportunistic Encryption) connections between two hosts (client and server).
* Checks for the success in establishing the OE connection.
* Easy to install on the hosts (client and server).
* Can test OE connections between two hosts.
* Checks if certbot is installed (on the server).
* Can generate Let's Encrypt certificates for the server using certbot.
* Generates the certbot configuration for reusing the private key.
* Enables automatic update of the generated certificates using cron tabs, keeping the private key same.
* Manual updating of keys also implemented.
* Generates the #pkcs12 file.
* Imports the generated certificates into NSS Database to be used for OE.
* Downloads the LetsEncrypt CA and intermediate certificates.
* Saves the default client/server configuration.
* Displays OE connection status to the user.
* Displays the certificates installed in NSS database.
* Disables ipsec and deletes configuration files saved in /etc/ipsec.d.
* Provides details about various available utilities, {commands} and [arguments].

## Source code

The source code of Libreswan Opportunistic IPsec using LetsEncrypt is merged in the master branch of the [Libreswan Repository](https://github.com/libreswan/libreswan). The commits made for the development of the project are available at the following url's:

* [letsencrypt: Added "ipsec letsencrypt" command](https://github.com/libreswan/libreswan/commit/e9ecb49534310336e800c7a90fd03f5a86c2d699)
* [documentation: Updated Opportunistic IPsec for LetsEncrypt configuration files](https://github.com/libreswan/libreswan/commit/1de84ec1777bd8f776f565ae6e7153d3390248bf)
* [testing: Add test cases for various asymmetric authentication use cases](https://github.com/libreswan/libreswan/commit/03cfc61175c5d250adf40934ed28aa5c4d9c2254)
* [testing: updated TESTLIST](https://github.com/libreswan/libreswan/commit/ede549206262b8846f7d73d53fc2f87b2e7782ba)

All the above commits are also available at this url [Libreswan Opportunistic IPsec using LetsEncrypt Commits](https://github.com/libreswan/libreswan/commits?author=Rishabh04-02) 

The original developer of the program is [Rishabh](https://github.com/Rishabh04-02). The project was developed under the expert guidance/mentorship of Paul Wouters & Tuomo Soini. This project was sponsored by Google as a part of [Google Summer of Code 2019](https://summerofcode.withgoogle.com/) Program. 

## Issues
To create/report an issue visit [Libreswan Issues](https://github.com/libreswan/libreswan/issues).

## License
This project(*Libreswan Opportunistic IPsec*) is Licensed under : [**GNU General Public License v2.0**](https://github.com/libreswan/libreswan/blob/master/LICENSE)
