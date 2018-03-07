Java

## Certificate Errors

It can happen if you want to access a host with an invalid certificate.

#### Exceptions

Spring Top-Level:

``````
org.springframework.web.client.ResourceAccessException: I/O error on GET request for x
``````

Stack:

``````
javax.net.ssl.SSLHandshakeException: sun.security.validator.ValidatorException: PKIX path building failed: sun.security.provider.certpath.SunCertPathBuilderException: unable to find valid certification path to requested target
``````

``````
sun.security.validator.ValidatorException: PKIX path building failed: sun.security.provider.certpath.SunCertPathBuilderException: unable to find valid certification path to requested target
``````

``````
sun.security.provider.certpath.SunCertPathBuilderException: unable to find valid certification path to requested target
``````



### Problem Causes

- Host to access uses invalid certificate for its domain

### How to fix / What to do

1. Load the affected domain in any browser (tried with Firefox).

2. Click the SSL icon (green lock) and 'More Information...' > 'View Certificate' > 'Details' > 'Export...'

3. Save the certificate. The X.509 Certificate `.crt` from Firefox worked for me, maybe the chain variant may also be useful for some domains.

4. Go to JDK (check in IDE) folder and find `jre/lib/security`

5. Create backup of `cacerts`-file

6. Go to `jre/bin` and execute:

   ``````
   keytool -import -v -trustcacerts -alias <DOMAIN> -file <PATH_TO_CERT>\<DOMAIN>.crt -keystore ../lib/security/cacerts -keypass changeit -storepass changeit
   ``````

   _Note: ONLY change strings in <>_

7. This should now work without restarting the JVM.

### Further information

To list all certificates allowed in the JRE, use `keytool -list -v -keystore ../lib/cacerts`.

#### Helpful resources

- https://stackoverflow.com/a/373307/2740014
