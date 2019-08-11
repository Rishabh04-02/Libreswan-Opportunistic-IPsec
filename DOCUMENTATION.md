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

1. `ipsec letsencrypt -client` OR `ipsec letsencrypt -server`

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
[root@linux]# ipsec letsencrypt -client
Installing for Client.
Downloading the letsencrypt certificates
Importing the downloaded certificates into the database
Notice: Trust flag u is set automatically if the private key is present.
Notice: Trust flag u is set automatically if the private key is present.
Saving the required configuration
Sending ping(IPv4) to letsencrypt.libreswan.org server.
OE Connection established successfully.
006 #6: "private-or-clear#193.110.157.131/32"[3] 100.64.0.1/32=== ...193.110.157.131, type=ESP, add_time=1565020164, inBytes=0, outBytes=336, id='CN=letsencrypt.libreswan.org', lease=100.64.0.1/32
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
Sending ping(IPv4) to letsencrypt.libreswan.org server.
OE Connection established successfully.
006 #2: "private-or-clear#193.110.157.131/32"[1] 100.64.0.1/32=== ...193.110.157.131, type=ESP, add_time=1565020241, inBytes=336, outBytes=336, id='CN=letsencrypt.libreswan.org', lease=100.64.0.1/32
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
Select the appropriate number [1-2] then [enter] (press 'c' to cancel): 2
Renewing an existing certificate

IMPORTANT NOTES:
 - Congratulations! Your certificate and chain have been saved at:
   /etc/letsencrypt/live/letsencrypt.libreswan.org/fullchain.pem
   Your key file has been saved at:
   /etc/letsencrypt/live/letsencrypt.libreswan.org/privkey.pem
   Your cert will expire on 2019-11-03. To obtain a new or tweaked
   version of this certificate in the future, simply run certbot
   again. To non-interactively renew *all* of your certificates, run
   "certbot renew"
 - If you like Certbot, please consider supporting our work by:

   Donating to ISRG / Let's Encrypt:   https://letsencrypt.org/donate
   Donating to EFF:                    https://eff.org/donate-le

Please enter the host name (e.g. letsencrypt.libreswan.org) : letsencrypt.libreswan.org
Enter Export Password:
Verifying - Enter Export Password:
Importing the certificate in database.
Enter password for PKCS12 file:
pk12util: PKCS12 IMPORT SUCCESSFUL

Certificate Nickname                                         Trust Attributes
                                                             SSL,S/MIME,JAR/XPI

isrgrootx1                                                   CT,,
trustid-x3-root                                              CT,,
letsencryptauthorityx3                                       ,,   
lets-encrypt-x3-cross-signed                                 ,,   
letsencrypt.libreswan.org                                    u,u,u
To confirm the success try running 'ipsec letsencrypt -t' on the client
```

4. `certbot renew --deploy-hook 'ipsec letsencrypt -ug hostname'`

For updating the generated certificate (keeping the private key same). This [argument] is used to update the certificate keeping the private key same, and performs the following tasks:
* Updating the certificate using Certbot keeping the private key same.
* Generating #pkcs12 file.
* Downloading the required Intermediate certificate.
* Importing the certificate in nss database.
* Displaying the certificates installed in nss database.

Sample Output -
```
[root@linux]# ipsec letsencrypt -uc
Saving debug log to /var/log/letsencrypt/letsencrypt.log

- - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - -
Processing /etc/letsencrypt/renewal/letsencrypt.libreswan.org.conf
- - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - -
Cert not yet due for renewal

- - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - -

The following certs are not due for renewal yet:
  /etc/letsencrypt/live/letsencrypt.libreswan.org/fullchain.pem expires on 2019-11-03 (skipped)
No renewals were attempted.
- - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - -
Enter Export Password:
Verifying - Enter Export Password:
Importing the certificate in the database.
Enter password for PKCS12 file:
pk12util: PKCS12 IMPORT SUCCESSFUL
Displaying the certificates installed in the database.

Certificate Nickname                                         Trust Attributes
                                                             SSL,S/MIME,JAR/XPI

isrgrootx1                                                   CT,,
trustid-x3-root                                              CT,,
letsencryptauthorityx3                                       ,,   
lets-encrypt-x3-cross-signed                                 ,,   
letsencrypt.libreswan.org                                    u,u,u
To confirm the success try running 'ipsec letsencrypt -t' on the client
```

5. `ipsec letsencrypt -h` OR `ipsec letsencrypt help`

For providing information regarding various {commands} and [arguments].

Sample output -
```
[root@paola libreswan]# ipsec letsencrypt -h
Usage: ipsec letsencrypt [arguments]
Available [arguments]
-client, -server, test, generatecertificate, updatecertificate, help, -t, -gc, -uc, -h

-client,-server :  For initial server/client setup.
usage: 'ipsec letsencrypt -client' OR 'ipsec letsencrypt -server'

test, -t  -  For testing the configuration/connections.
usage: 'ipsec letsencrypt test' OR 'ipsec letsencrypt -t'

generatecertificate, -gc  -  For generating the certificate.
usage: 'ipsec letsencrypt generatecertificate' OR 'ipsec letsencrypt -gc'

For updating the generated certificate (keeping the private key same) use the following command.
usage: 'usage: certbot renew --deploy-hook "ipsec letsencrypt -ug hostname"'
```
