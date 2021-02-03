# Projekt_1-Computer_Security

COMMANDS

1.
openssl req -x509 -newkey rsa:4096 -keyout CAkey.pem -out CAcert.pem -days 365

2.
keytool -import -alias CA -file CAcert.pem -keystore clienttruststore


3.
keytool -genkeypair -alias client -keyalg rsa -keystore clientkeystore -storepass password
Filip Kalkan (fi1231ka-s)/Eric Schyllert (mat11esc)/Fredrik Bixo (fr1663bi-s)


4.
keytool -certreq -alias client -keystore clientkeystore -keyalg rsa -file client.csr


5.
openssl x509 -req -days 365 -in ./client.csr -CA CAcert.pem -CAkey CAkey.pem -CAserial ./CAserial -CAcreateserial -out clientcert.pem


6.
keytool -import -trustcacerts -alias CA -file CAcert.pem -keystore clientkeystore
keytool -import -alias client -file clientcert.pem -keystore clientkeystore


7. (NOT NEEDED) Delete the default key which was created together with the keystore
keytool -delete -alias mykey -storepass password -keystore clientkeystore


9.
navigate to server

keytool -genkeypair -alias server -keyalg rsa -keystore serverkeystore -storepass password
CN=MyServer

keytool -certreq -alias server -keystore serverkeystore -keyalg rsa -file server.csr

openssl x509 -req -days 365 -in ./server.csr -CA ../CA/CAcert.pem -CAkey ../CA/CAkey.pem -CAserial ../CA/CAserial -out servercert.pem

keytool -import -trustcacerts -alias CA -file ../CA/CAcert.pem -keystore serverkeystore

10.
Copy clienttruststore to server and rename to servertruststore. Password is preserved.



QUESTION A
-Create serial number file if it does not exist

QUESTION B
-use the -ext option when using -certreq

QUESTION C
ISSUER UNIQUE IDENTIFIER: Unique ID of CA in case another CA has same name (optional)
SUBJECT UNIQUE IDENTIFIER: Unique ID of subject in case another subject has same name (optional)
EXTENSIONS: Additional information, such as max length of chain, alternative name of subject etc (optional)

QUESTION D
It is possible to copy the truststore to the server since it only contains the CA certificate. Both the server and the client trust the CA. The truststore is only for storing which certificates are trusted. Since both client and server share the same trusted actor, and client/server certificates are both signed by the CA they know they can trust eachother.

QUESTION E
@TODO
