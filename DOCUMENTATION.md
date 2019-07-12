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

### curl
It can be downloaded from [here](https://curl.haxx.se/download.html).

### certutil
It can be downloaded from [here](https://chromium.googlesource.com/chromium/src/+/HEAD/docs/linux_cert_management.md).

### wget
It can be downloaded from [here - debian/ubuntu](https://www.cyberciti.biz/faq/how-to-install-wget-togetrid-of-error-bash-wget-command-not-found/) OR [here - RHEL/CentOS 7](https://www.cyberciti.biz/faq/yum-install-wget-redhat-cetos-rhel-7/)

### certbot
It is required to generate certificates (only if you are using the script for the server side). It can be downloaded from [here](https://certbot.eff.org/)

### openssl
It is required to generate #pkcs12 (.p12) file for importing in the nss database. It can be downloaded from [here](https://www.openssl.org/source/)

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

2. `import_certificates`
* This scripts imports the custom certificates into the NSS database.
* Save the certificates PKCS#12 (.p12) file in the `certs/custom` directory. The script will import all the certificates available in the directory.

3. `custom_configuration`
* This script allows user to create custom configurations and run IPsec with them.
* The script loads the configuration from `config/custom` directory and saves it as the default configuration.
* After saving the configuration the script restarts IPsec and establishes an OE connection.
* It also displays the connection status to user.

4. `create_connection`
* This script checks for existing OE connections. Restarts IPsec if any existing OE connection found.
* After that it establishes a new OE connection.
* Displays the connection status to user.

## Sample Installation output `setup`

### For Client

	$ sudo bash setup
	[sudo] password for user:

	Checking if the script is run as root.
	This script is run as root. Good to go.

	Installing for server or client? Type (sS/cC) c
	Checking if IPsec is installed
	IPsec is installed.

	Checking for any existing OE connections
	Existing OE Connections Found. Stopping the connections.
	Redirecting to: systemctl restart ipsec.service

	Downloading the letsencrypt certificates
	Deleting the certs directories certs/CA , certs/intermediate (if previously present)
	CA Certificates downloaded.
	Intermediate Certificates downloaded.

	Initializing the nss database
	NSS database already initialised - aborted
	To wipe the old NSS database, issue: rm /etc/ipsec.d/*.db

	Importing the downloaded certificates into NSS Database
	CA certificates Imported successfully.
	Notice: Trust flag u is set automatically if the private key is present.
	Notice: Trust flag u is set automatically if the private key is present.
	Intermediate certificates Imported successfully.

	Saving the required configuration
	config/oe-letsencrypt-client.conf configuration saved in /etc/ipsec.d

	Restarting Ipsec

	Redirecting to: systemctl restart ipsec.service
	Establishing an OE connection.

	  % Total    % Received % Xferd  Average Speed   Time    Time     Time  Current
	                                 Dload  Upload   Total   Spent    Left  Speed
	100    14  100    14    0     0     51      0 --:--:-- --:--:-- --:--:--    51

	Checking the success of establishing OE connection

	OE Connection established successfully

	Displaying connection status

	006 #2: "private-or-clear#193.110.157.131/32"[1] ...193.110.157.131, type=ESP, add_time=1562298201, inBytes=0, outBytes=0, id='CN=letsencrypt.libreswan.org'


### For Server

	$ sudo bash setup
	[sudo] password for user:

	Checking if the script is run as root.
	This script is run as root. Good to go.

	Installing for server or client? Type (sS/cC) s
	Checking if IPsec is installed
	IPsec is installed.

	Checking for any existing OE connections
	Existing OE Connections Found. Stopping the connections.
	Redirecting to: systemctl restart ipsec.service

	Downloading the letsencrypt certificates
	Deleting the certs directories certs/CA , certs/intermediate (if previously present)
	CA Certificates downloaded.
	Intermediate Certificates downloaded.

	Initializing the nss database
	NSS database already initialised - aborted
	To wipe the old NSS database, issue: rm /etc/ipsec.d/*.db

	Importing the downloaded certificates into NSS Database
	CA certificates Imported successfully.
	Notice: Trust flag u is set automatically if the private key is present.
	Notice: Trust flag u is set automatically if the private key is present.
	Intermediate certificates Imported successfully.

	Saving the required configuration
	config/oe-letsencrypt-server.conf configuration saved in /etc/ipsec.d

	Restarting Ipsec

	Redirecting to: systemctl restart ipsec.service
	Establishing an OE connection.


	Checking the success of establishing OE connection

	Failed to establish an OE connection. (Ignore this message if you installed for server. As it checks the ipsec traffic.)
