# Libreswan Opportunistic IPsec Documentation

## Prerequisite
### IPsec -  [Libreswan](https://github.com/libreswan/libreswan/)
It can be installed using any of the following methods:
1. Download page official website - [https://download.libreswan.org/](https://download.libreswan.org/)
2. GitHub repository [https://github.com/libreswan/libreswan/](https://github.com/libreswan/libreswan/)
3. Using the package manager in Linux distributions:
	* Fedora - `sudo dnf -y install libreswan-3.* `
	* Centos - `sudo yum -y install libreswan-3.*`
	* Ubuntu - `sudo apt-get -y install libreswan`

Note - * refers to the latest version available.

### curl, certutil, wget, certbot, openssl

## Installation

1. clone the [project repository](https://github.com/Rishabh04-02/Libreswan-Opportunistic-IPsec.git) using the following command:
` git clone https://github.com/Rishabh04-02/Libreswan-Opportunistic-IPsec.git`

2. Go to the project directory using the following command:
 `cd Libreswan-Opportunistic-IPsec`

 3. Run the setup file:
 `sudo bash setup`
 When you run the setup file it'll ask for: *Installing for server or client? Type (S/C)*. Choose your response accordingly.

## Scripts available
Note - OE refers to Opportunistic Encryption.

1. `setup`

This script is the main script which is to be run when installing the project for the first time. This script performs the following tasks:
* Check if IPsec is installed.
* performs the 1st time server/client Installation.
* Checks for existing OE connections.
* Downloads the LetsEncrypt CA and intermediate certificates.
* Initializes the NSS database and import the LetsEncrypt certificates in it.
* Saves the default client/server configuration.
* Restarts IPsec to load the latest changes.
* Establishes the OE connection.
* Checks for the success in establishing the OE connection.
* Displays OE connection status to user.

2. `test_connection`

This script checks for the success of establishing an OE connection, and performs the following tasks:
* Check for any existing OE connections.
* Establish an OE connection.
* Sending pings to the letsencrypt.libreswan.org server.
* Checking the success of establishing OE connection.
* Displaying connection status to the user.

3. `custom_configuration`

* This script allows user to create custom configurations and run IPsec with them.
* The script loads the configuration from config/custom directory and saves it as the default configuration.
* After saving the configuration the script restarts IPsec and establishes an OE connection.
* It also displays the connection status to user.

4. `generate_certificate`

The script is used Generating the certificate using Certbot, and performing the following tasks:
* Check if certbot is installed.
* Preparing the certificate for importing in the nss database.
* Generating #pkcs12 file.
* Downloading the required Intermediate certificate.
* Displaying the certificates installed in nss database.
* Generating the certbot configuration for reusing key.

5. `update_certificate`

This script is used to update the certificate keeping the key same, and performs the following tasks:
* Updating the certificate using Certbot keeping the private key same.
* Generating #pkcs12 file.
* Downloading the required Intermediate certificate.
* Importing the certificate in nss database.
* Displaying the certificates installed in nss database.
