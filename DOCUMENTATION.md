# Libreswan Opportunistic IPsec Documentation

## Prerequisite
1. IPsec -  [Libreswan](https://github.com/libreswan/libreswan/)
2. curl
3. certutil
4. wget
5. certbot
6. openssl

## Installation

Follow these [Installation instructions](https://github.com/libreswan/libreswan/blob/master/README.md#compiling-the-userland-and-ike-daemon-manually-in-usrlocal)

## Available [arguments]
Note - To get the list of all the acceptable arguments run `ipsec letsencrypt -h` OR `ipsec letsencrypt help`

> setup, test, generatecertificate, updatecertificate, help, -s, -t, -gc, -uc, -h

## Functions of various [arguments]
Note - OE refers to Opportunistic Encryption.

1. `ipsec letsencrypt setup` OR `ipsec letsencrypt -s`

For initial setup, it is to be run when installing the project for the first time. This [argument] performs the following tasks:
* performs the 1st time server/client Installation.
* Checks for existing OE connections.
* Downloads the LetsEncrypt CA and intermediate certificates.
* Initializes the NSS database and import the LetsEncrypt certificates in it.
* Saves the default client/server configuration.
* Restarts IPsec to load the latest changes.
* Establishes the OE connection.
* Checks for the success in establishing the OE connection.
* Displays OE connection status to user.

2. `ipsec letsencrypt test` OR `ipsec letsencrypt -t`

For testing the configuration/connections. This [argument] checks for the success of establishing an OE connection, and performs the following tasks:
* Check for any existing OE connections.
* Establish an OE connection.
* Sending pings to the letsencrypt.libreswan.org server.
* Checking the success of establishing OE connection.
* Displaying connection status to the user.

3. `ipsec letsencrypt generatecertificate` OR `ipsec letsencrypt -gc`

For generating the certificate. This [argument] is used for Generating the certificate using Certbot, and performing the following tasks:
* Check if certbot is installed.
* Preparing the certificate for importing in the nss database.
* Generating #pkcs12 file.
* Downloading the required Intermediate certificate.
* Displaying the certificates installed in nss database.
* Generating the certbot configuration for reusing key.

4. `ipsec letsencrypt updatecertificate` OR `ipsec letsencrypt -uc`

For updating the generated certificate (keeping the private key same). This [argument] is used to update the certificate keeping the private key same, and performs the following tasks:
* Updating the certificate using Certbot keeping the private key same.
* Generating #pkcs12 file.
* Downloading the required Intermediate certificate.
* Importing the certificate in nss database.
* Displaying the certificates installed in nss database.
