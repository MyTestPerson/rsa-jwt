**Creating a sample CA certificate**

openssl.exe req -config openssl.cnf -new -x509 -keyout private.pem -out certificate.pem -days 365


**Create a kestore named keystore**

keytool –keystore keystore –genkey –alias client -keyalg rsa


**Generate certificate signing request**

keytool –keystore keystore –certreq –alias client –keyalg rsa –file client.csr


**Generate signed certificate for associated CSR**

openssl.exe x509 -req -CA certificate.pem -CAkey private.pem -in client.csr -out client.cer -days 365 -CAcreateserial


**Import CA certificate into keystore**

keytool -import -keystore keystore -file certificate.pem -alias theCARoot


**Import signed certificate for associated alias in the keystore**

keytool –import –keystore keystore –file client.cer –alias client