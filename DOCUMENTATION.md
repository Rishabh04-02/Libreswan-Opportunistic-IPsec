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

> setup --client, setup --server, test, generatecertificate, updatecertificate, help, -s --client, -s --server, -t, -gc, -uc, -h

## Functions of various [arguments]
Note - OE refers to Opportunistic Encryption.

1. `ipsec letsencrypt setup --client` OR `ipsec letsencrypt -s --client` OR `ipsec letsencrypt setup --server` OR `ipsec letsencrypt -s --server`

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

Sample Output -
```
[root@linux]# ipsec letsencrypt -s --client
This command is run as root. Good to go.
Installing for Client.
Checking for any existing OE connections
Existing OE Connections Found. Stopping the connections.
Redirecting to: systemctl restart ipsec.service
Downloading the letsencrypt certificates
CA Certificates downloaded in /tmp/tmp.t0IOLy0Van
Intermediate Certificates downloaded in /tmp/tmp.RgvamPXWfK
Importing the downloaded certificates into the database
CA certificates Imported successfully.
Notice: Trust flag u is set automatically if the private key is present.
Notice: Trust flag u is set automatically if the private key is present.
Intermediate certificates Imported successfully.
Saving the required configuration
oe-letsencrypt-client.conf configuration saved in /etc/ipsec.d
Restarting Ipsec
Redirecting to: systemctl restart ipsec.service
Establishing an OE connection.
Sending ping(IPv4) to the letsencrypt.libreswan.org server.
Ping Successful
Checking the success of establishing OE connection
OE Connection established successfully.
Displaying connection status.
006 #2: "private-or-clear#193.110.157.131/32"[1] ...193.110.157.131, type=ESP, add_time=1564900845, inBytes=336, outBytes=336, id='CN=letsencrypt.libreswan.org'
```

2. `ipsec letsencrypt test` OR `ipsec letsencrypt -t`

For testing the configuration/connections. This [argument] checks for the success of establishing an OE connection, and performs the following tasks:
* Check for any existing OE connections.
* Establish an OE connection.
* Sending pings to the letsencrypt.libreswan.org server.
* Checking the success of establishing OE connection.
* Displaying connection status to the user.

Sample Output -
```
[root@linux]# ipsec letsencrypt -t
This command is run as root. Good to go.
Checking for any existing OE connections
No existing OE connections found. Good to go.
Sending ping(IPv4) to letsencrypt.libreswan.org server.
Ping Successful
Checking the success of establishing OE connection
OE Connection established successfully.
Displaying connection status.
006 #2: "private-or-clear#193.110.157.131/32"[1] ...193.110.157.131, type=ESP, add_time=1564900845, inBytes=336, outBytes=336, id='CN=letsencrypt.libreswan.org'
```

3. `ipsec letsencrypt generatecertificate` OR `ipsec letsencrypt -gc`

For generating the certificate. This [argument] is used for Generating the certificate using Certbot, and performing the following tasks:
* Check if certbot is installed.
* Preparing the certificate for importing in the nss database.
* Generating #pkcs12 file.
* Downloading the required Intermediate certificate.
* Displaying the certificates installed in nss database.
* Generating the certbot configuration for reusing key.

Sample Output -
```
[root@linux]# ipsec letsencrypt -gc
This command is run as root. Good to go.
Checking if Certbot is installed.
Certbot is installed, Good to go.
Generating the certificate using Certbot.
Saving debug log to /var/log/letsencrypt/letsencrypt.log
Plugins selected: Authenticator webroot, Installer None
Starting new HTTPS connection (1): acme-v02.api.letsencrypt.org
Please enter in your domain name(s) (comma and/or space separated)  (Enter 'c'
to cancel): letsencrypt.libreswan.org
Cert not yet due for renewal

You have an existing certificate that has exactly the same domains or certificate name you requested and isn't close to expiry.
(ref: /etc/letsencrypt/renewal/letsencrypt.libreswan.org.conf)

What would you like to do?
- - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - -
1: Keep the existing certificate for now
2: Renew & replace the cert (limit ~5 per 7 days)
- - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - -
Select the appropriate number [1-2] then [enter] (press 'c' to cancel): 1
Keeping the existing certificate

- - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - -
Certificate not yet due for renewal; no action taken.
- - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - -
Preparing the certificate for importing in the nss database.
Generating the #pkcs12 (.p12) file.
Downloading the required Intermediate certificate.
Intermediate Certificate downloaded in /tmp/tmp.wZ0nz9qhRM
Renaming the certificate.
Certificate /tmp/tmp.wZ0nz9qhRM/letsencryptauthorityx3.pem.txt renamed to /tmp/tmp.wZ0nz9qhRM/letsencryptauthorityx3.pem.
Enter the cert directory location (e.g. /etc/letsencrypt/live/letsencrypt.libreswan.org): /etc/letsencrypt/live/letsencrypt.libreswan.org
Enter Export Password:
Verifying - Enter Export Password:

Importing the certificate in nss database.
Enter password for PKCS12 file:
pk12util: PKCS12 IMPORT SUCCESSFUL
Displaying the certificates installed in nss database.

Certificate Nickname                                         Trust Attributes
                                                             SSL,S/MIME,JAR/XPI

isrgrootx1                                                   CT,,
trustid-x3-root                                              CT,,
letsencryptauthorityx3                                       ,,   
lets-encrypt-x3-cross-signed                                 ,,   
letsencrypt.libreswan.org                                    u,u,u
letsencrypt.libreswan.org                                    u,u,u
letsencrypt.libreswan.org                                    u,u,u
letsencrypt.libreswan.org                                    u,u,u
Updating the letsencrypt configuration for reusing key.

Enter the config file name (e.g. /etc/letsencrypt/renewal/letsencrypt.libreswan.org.conf): /etc/letsencrypt/renewal/letsencrypt.libreswan.org.conf

To confirm the success try running 'ipsec letsencrypt -t' on the client
```

4. `ipsec letsencrypt updatecertificate` OR `ipsec letsencrypt -uc`

For updating the generated certificate (keeping the private key same). This [argument] is used to update the certificate keeping the private key same, and performs the following tasks:
* Updating the certificate using Certbot keeping the private key same.
* Generating #pkcs12 file.
* Downloading the required Intermediate certificate.
* Importing the certificate in nss database.
* Displaying the certificates installed in nss database.

Sample Output -
```
[root@linux]# ipsec letsencrypt -uc
This command is run as root. Good to go.
Checking if Certbot is installed.
Certbot is installed, Good to go.
Updating the certificate using Certbot keeping the private key same.

Saving debug log to /var/log/letsencrypt/letsencrypt.log

- - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - -
Processing /etc/letsencrypt/renewal/letsencrypt.libreswan.org.conf
- - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - -
Cert not yet due for renewal

- - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - -

The following certs are not due for renewal yet:
  /etc/letsencrypt/live/letsencrypt.libreswan.org/fullchain.pem expires on 2019-10-10 (skipped)
No renewals were attempted.
- - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - -
Did your certificate update? (yY/nN) y
Importing the updated certificate in the nss database
Generating the #pkcs12 (.p12) file.
Downloading the required Intermediate certificate.
Intermediate Certificate downloaded in /tmp/tmp.TeCRvauxFr

Renaming the certificate.
Certificate /tmp/tmp.TeCRvauxFr/letsencryptauthorityx3.pem.txt renamed to /tmp/tmp.TeCRvauxFr/letsencryptauthorityx3.pem.
Enter the cert directory location (e.g. /etc/letsencrypt/live/letsencrypt.libreswan.org): /etc/letsencrypt/live/letsencrypt.libreswan.org
Enter Export Password:
Verifying - Enter Export Password:

Importing the certificate in nss database.
Enter password for PKCS12 file:
pk12util: PKCS12 IMPORT SUCCESSFUL
Displaying the certificates installed in nss database.


Certificate Nickname                                         Trust Attributes
                                                             SSL,S/MIME,JAR/XPI

isrgrootx1                                                   CT,,
trustid-x3-root                                              CT,,
letsencryptauthorityx3                                       ,,   
lets-encrypt-x3-cross-signed                                 ,,   
letsencrypt.libreswan.org                                    u,u,u
letsencrypt.libreswan.org                                    u,u,u
letsencrypt.libreswan.org                                    u,u,u
letsencrypt.libreswan.org                                    u,u,u

To confirm the success try running 'ipsec letsencrypt -t' on the client
```

5. `ipsec letsencrypt -h` OR `ipsec letsencrypt help`

For providing information regarding various {commands} and [arguments].

Sample output -
```
[root@linux]# ipsec letsencrypt -h
Usage: ipsec letsencrypt [arguments]
Available [arguments]
setup, test, generatecertificate, updatecertificate, help, -s, -t, -gc, -uc, -h

setup, -s  :  For initial setup.
usage: 'ipsec letsencrypt setup' OR 'ipsec letsencrypt -s'

test, -t  -  For testing the configuration/connections.
usage: 'ipsec letsencrypt test' OR 'ipsec letsencrypt -t'

generatecertificate, -gc  -  For generating the certificate.
usage: 'ipsec letsencrypt generatecertificate' OR 'ipsec letsencrypt -gc'

updatecertificate, -uc  -  For updating the generated certificate (keeping the private key same).
usage: 'ipsec letsencrypt updatecertificate' OR 'ipsec letsencrypt -uc'
```
