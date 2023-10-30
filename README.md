# How to Install an Nginx SSL Certificate: An Initial Checklist
Before getting started with the installation steps, please ensure that the following prerequisites are met:

## Purchase or renew your SSL certificate.
1. Generate and submit the certificate signing request (CSR).
1. Save the private key on your server.
1. Complete the order for SSL certificate issuance and submit all relevant documents.
1. Save your server certificate file and your intermediate certificates.

## How to Install an Nginx SSL Certificate: A Step-by-Step Guide
Once you have everything on the initial checklist, you can follow the steps below that describe how to install Sectigo SSL to Nginx.

### Link Your Files.
Concatenate the CA bundle zip file and the certificate file, which were sent to your registered email by Sectigo (or your certificate authority) using the following command.

`cat domain_com.crt domain_com.ca-bundle > ssl-bundle.crt`

Note for Sectigo “Certificate Manager” customers — ensure that you download the x.509 base64 encoded “Certificate Only” along with the Root/Intermediate “Certificate only” files. To complete the process above, you can change the .cer formatted files to .crt file extension.

### Copy the Certificate Files.
Store the bundle under the proper folder where Nginx can read it.


```
mkdir -p /etc/nginx/ssl/example_com/

mv ssl-bundle.crt /etc/nginx/ssl/example_com/
```


### Copy Your Private Key.
Be sure to also place your private key under the correct location.

`mv example_com.key /etc/nginx/ssl/example_com/`

### Edit Your Nginx Virtual Host Config File.
Ensure that the Nginx configuration file points to the correct location of your private key and cert file.


```
server {

listen 443;

server_name domainname.com;

ssl on;

ssl_certificate /etc/ssl/certs/ssl-bundle.crt;

ssl_certificate_key /etc/ssl/private/domainname.key;

ssl_prefer_server_ciphers on;

}
```
