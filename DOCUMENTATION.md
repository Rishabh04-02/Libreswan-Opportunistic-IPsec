# Libreswan Opportunistic IPsec Documentation

## Prerequisite
### IPsec -  [Libreswan](https://github.com/libreswan/libreswan/)
It can be installed using any of the following methods:
1. Download page official website - [https://download.libreswan.org/](https://download.libreswan.org/)
2. GitHub repository [https://github.com/libreswan/libreswan/](https://github.com/libreswan/libreswan/)
3. Using the package manager in various Linux distributions.

### curl, certutil, wget, certbot, openssl

## Installation

1. clone the [project repository](https://github.com/Rishabh04-02/Libreswan-Opportunistic-IPsec.git) using the following command:
` git clone https://github.com/Rishabh04-02/Libreswan-Opportunistic-IPsec.git`

2. Go to the project directory using the following command:
`cd Libreswan-Opportunistic-IPsec`

3. Run the letsencrypt file:
`sudo bash letsencrypt [argument]`

## Available [arguments]
Note - To get the list of all the acceptable arguments run `letsencrypt -h` OR `letsencrypt help`

> setup, test, generatecertificate, updatecertificate, help, -s, -t, -gc, -uc, -h

## Functions of various [arguments]
Note - OE refers to Opportunistic Encryption.

1. `letsencrypt setup` OR `letsencrypt -s`

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

2. `letsencrypt test` OR `letsencrypt -t`

For testing the configuration/connections. This [argument] checks for the success of establishing an OE connection, and performs the following tasks:
* Check for any existing OE connections.
* Establish an OE connection.
* Sending pings to the letsencrypt.libreswan.org server.
* Checking the success of establishing OE connection.
* Displaying connection status to the user.

3. `letsencrypt generatecertificate` OR `letsencrypt -gc`

For generating the certificate. This [argument] is used for Generating the certificate using Certbot, and performing the following tasks:
* Check if certbot is installed.
* Preparing the certificate for importing in the nss database.
* Generating #pkcs12 file.
* Downloading the required Intermediate certificate.
* Displaying the certificates installed in nss database.
* Generating the certbot configuration for reusing key.

4. `letsencrypt updatecertificate` OR `letsencrypt -uc`

For updating the generated certificate (keeping the private key same). This [argument] is used to update the certificate keeping the private key same, and performs the following tasks:
* Updating the certificate using Certbot keeping the private key same.
* Generating #pkcs12 file.
* Downloading the required Intermediate certificate.
* Importing the certificate in nss database.
* Displaying the certificates installed in nss database.
