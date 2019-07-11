ipsec letsencrypt setup --client    <--- resstorecon, client config, get CA installed                                                         |
ipsec letsencrypt setup --server     <----- this should also configure letsencrypt using certbot first, maybe dehydrated later                |
                                                                                                                                              |
ipsec letencrypt test   (ipv4 test to letsencrypt.libreswan.org)                                                                              |
(test using ping -4 and then test for ipsec traffic entry for 193.110.157.131)                                                                |
                                                                                                                                              |
using mktemp                                                                                                                                  |

-   handle updating certs with same key, for now using libreswan restart                                                                      |
-    how does client fix connection after server restart (serer does ipsec restart)                                                           |
-    how does client fix connection after server crash (serer does: killall -9 pluto ; ipsec restart)                                         |
     (use liveness, dpdaction=)                                                                                                               |
                                                                                                                                              |
- does cert bot have a buildin webserver we can use without needing apache or nginx                                                           |
  (digital ocean has standalone mode documented?                                                                                              |
- certbot libreswan plugin ?                                                                                                                  |
  * could update the runtime nss with our own cert ?                                                                                          |
  * should update the nss on disk      
