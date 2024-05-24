# Extend K3S services ssl certificate expiry
K3s client and server certificates are valid for 365 days from their date of issuance. Any certificates that are expired, or within 90 days of expiring, are automatically renewed every time K3s starts. But, in my case it did not automatically renewed.
The impact of this is many services were in error condition. So, it will be good if the SSL certificate can be extended to 5 or ten years. In this documentation I extend the certificate for ten years.
1. Stop K3S service in all master nodes because I use HA K3S cluster with 3 nodes
   ```shell
   systemctl stop k3s
   ```
3. Add CATTLE_NEW_SIGNED_CERT_EXPIRATION_DAYS into K3S runtime environment file at /etc/systemd/system/k3s.service.env here is my example:
     ```shell
     CATTLE_NEW_SIGNED_CERT_EXPIRATION_DAYS=3650
     K3S_DATASTORE_CAFILE='/etc/etcd/etcd-ca.crt'
     K3S_DATASTORE_CERTFILE='/etc/etcd/server.crt'
     K3S_DATASTORE_ENDPOINT='https://10.10.10.2:2379,https://10.10.10.3:2379,https://10.10.10.4:2379'
     K3S_DATASTORE_KEYFILE='/etc/etcd/server.key'
     K3S_TOKEN='xxxxxxxxxx30534ef739b2cb455ab17f75e814fe54e9e56c841d5ce4395xxxxxxx::server:xxxxxxxxxxxx50bd4d2346b29dda'
     ```
     
