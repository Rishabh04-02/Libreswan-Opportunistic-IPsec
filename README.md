# Libreswan-Opportunistic-IPsec

Libreswan Opportunistic IPsec using LetsEncrypt is a project to create a program `letsencrypt` in `ipsec` which allows establishing the Opportunistic Encryption connections between two hosts. The `letsencrypt` program allows using various available utilities required to establish and control an Opportunistic connection. The letsencrypt program has several features, and can be used by running a specified {command} with a specified [argument].

e.g. `ipsec letsencrypt --help` lists all the available commands and how to use them.

The man page for the program is available at `man ipsec letsencrypt`. The program creates a secure Opportunistic Connection between the hosts commonly referred to as client and server. The client connects to the server and remains anonymous, whereas the server is authenticated before connecting to it, i.e., server is not anonymous. The server uses Let's Encrypt certificates for authentication and encryption purposes. Once the initial phase of authentication and handshaking completes, the secure connection establishes, and all the traffic (traffic can be through multiple applications) between the two hosts is now encrypted.

The details about the utilities and using them can be found in the [Documentation: Libreswan Opportunistic IPsec using LetsEncrypt](https://libreswan.org/wiki/Documentation:_Libreswan_Opportunistic_IPsec_using_LetsEncrypt) . Also, the documentation includes the sample output for each {command} and [argument].

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
