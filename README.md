# SIWECOS-TLS-Scanner
SIWECOS-TLS-Scanner is a Webservice created by the Chair for Network and Data Security from the Ruhr-University Bochum for the integration of the [TLS-Scanner](https://github.com/RUB-NDS/TLS-Scanner) in the SIWECOS Project. The Webservice scans a provided URL for various TLS misconfigurations and responds with a JSON report.

# Compiling
In order to compile and use SIWECOS-TLS-Scanner, you need to have Java installed, as well as [TLS-Attacker](https://github.com/RUB-NDS/TLS-Attacker), [ModifiableVariables](https://github.com/RUB-NDS/ModifiableVariable) and the [TLS-Scanner](https://github.com/RUB-NDS/TLS-Scanner)

```bash
$ cd TLS-Scanner
$ ./mvnw clean package

```

For hints on installing the required libraries checkout the corresponding GitHub repositories.

**Please note:**  *In order to run this tool you need TLS-Attacker version 2.0Beta4*

# Running
In order to run SIWECOS-TLS-Scanner you need to deploy the .war file from the target/ folder to your favourite java application server (eg. Glassfish, Tomcat ...). After that the webservice should be up and running and can be called with:

```
http://127.0.0.1:8080/SIWECOS-TLS-Scanner-1.1/SIWECOS-TLS-Scanner/127.0.0.1:4433
```

or 

```
http://127.0.0.1:8080/SIWECOS-TLS-Scanner/127.0.0.1:4433
```
This depends on your used server.

If you do not specify a port number port 443 will be used.

# Results
TLS-Scanner uses the concept of "checks" which are performed after it collected configuration information. A check which results in "true" is consideres a non optimal choice and is an indicator for a pentester for a possible problem.

An example output may look like this:
```json

{
    "checks":{
        "CERTIFICATE_NOT_SENT_BY_SERVER":{
            "result":false,
            "risk":0
        },
        "CERTIFICATE_EXPIRED":{
            "result":false,
            "risk":0
        },
        "CERTIFICATE_NOT_VALID_YET":{
            "result":false,
            "risk":0
        },
        "CERTIFICATE_WEAK_HASH_FUNCTION":{
            "result":true,
            "risk":7
        },
        "CERTIFICATE_WEAK_SIGN_ALGORITHM":{
            "result":false,
            "risk":0
        },
        "PROTOCOLVERSION_SSL2":{
            "result":false,
            "risk":0
        },
        "PROTOCOLVERSION_SSL3":{
            "result":false,
            "risk":0
        },
        "CIPHERSUITE_ANON":{
            "result":false,
            "risk":0
        },
        "CIPHERSUITE_CBC":{
            "result":true,
            "risk":4
        },
        "CIPHERSUITE_EXPORT":{
            "result":false,
            "risk":0
        },
        "CIPHERSUITE_NULL":{
            "result":false,
            "risk":0
        },
        "CIPHERSUITE_RC4":{
            "result":false,
            "risk":0
        },
        "CIPHERSUITEORDER_ENFORCED":{
            "result":false,
            "risk":0
        }
    }
}
```

For more information on the interpretation of this output checkout the [TLS-Scanner](https://github.com/RUB-NDS/TLS-Scanner) repository.

**Please note:**  *A check with a _result_ of true is considered non optimal*

