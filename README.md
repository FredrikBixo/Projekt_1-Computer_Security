# Projekt_1-Computer_Security

COMMANDS
1.
openssl req -x509 -newkey rsa:4096 -keyout CAkey.pem -out CAcert.pem -days 365

2.
keytool -import -file CAcert.pem -keystore keystore -trustcacerts

3.
keytool -genkeypair -keyalg rsa -keystore clientkeystore -storepass password
(CN=Filip Kalkan (fi1231ka-s)/Eric Schyllert (mat11esc)/Fredrik Bixo (fr1663bi-s))

4.
keytool -certreq -keystore clientkeystore -keyalg rsa -file client.csr

5. ???
openssl ca -cert CAcert.pem -keyfile CAkey.pem -infiles client.csr -out clientcert.pem
this might work, but need to look into it.
insprired by: https://stackoverflow.com/questions/21297139/how-do-you-sign-a-certificate-signing-request-with-your-certification-authority

QUESTION A
-Create serial number file if it does not exist

QUESTION B
- You add the -extfile command add an extension section in the certificate.

QUESTION C
- Extensions are extra certificate fields that can contain pretty much any type of information.
For example:
authorityKeyIdentifier=keyid,issuer
basicConstraints=CA:FALSE
keyUsage = digitalSignature, nonRepudiation, keyEncipherment, dataEncipherment
