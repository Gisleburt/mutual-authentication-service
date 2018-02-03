Mutual Authentication Service 
=============================

This project is in development. Work on the client can be found here: [Mutual Authentication Service Client]

What is Mutual Authentical?
---------------------------

[Mutual Authentication] is provided when two parties who wish to talk to each other can both provide a certificate
signed by a trusted third party.

When you connect to a serivce over https, the service will provide a certificate to prove who it is, but usually you
do not do the same.
It is perfectly possible to do Mutual Authentication over https however, and it can be highly
desirable.
For example, you might have an "admin" section of your website, that you only want your employees to access.
Traditionally, this is done by only IP whitelisting your own network, and if an employee is off site, they must
connect via a VPN to your network before gaining acces.

The problem
-----------

There are two downsides to IP whitelisting:

1. you may not have a dedicated IP on your network
2. just because someone is on your network, does not mean they are an employee

Mutual Authentication solves this, as it authorises users on a one by one basis.
So why don't people do this?
Encryption is hard.
In order to get a signed certificate, the user must:

1. create a private key
2. use the key to create a CSR
3. send the CSR to a Certificate Authority trusted by the service they want to access
4. combine the certificate they recieve together with their original key
5. import the combined key and certificate into their browser

It is absurd to expect any normal user to do this.

A proposed solution
-------------------

The mutual authentication service is two pieces of software that work together to simplify the process without
negating the security.

A client side app generates a cryptographic key and CSR on the users behalf
The CSR is sent to a secure server which requests an administrator authorise the minting of a certificate
The certificate is sent back to the user and installed into their browser

[Mutual Authentication]: https://en.wikipedia.org/wiki/Mutual_authentication
[Mutual Authentication Service Client]: https://github.com/Gisleburt/mutual-authentication-service-client
