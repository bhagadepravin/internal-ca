# Getting started
####  Optionally clear the CA folder:

```
sudo rm -rf /root/ca
```
Grab the scripts:

```bash
cd
rm -rf ~/internal-ca
git clone https://github.com/bhagadepravin/internal-ca.git
cd ~/internal-ca
chmod +x *.sh
```

Customize **openssl.cnf** files as needed or keep default values.

You can now create your certs. As an example, to create certs as per the diagram above:

```bash
cd ~/internal-ca
sudo ./create_root.sh

sudo ./create_int.sh intermediate
sudo ./create_server.sh intermediate c474-node1.coelab.cloudera.com

sudo ./create_int.sh int3  
sudo ./create_client.sh int3 deviceA  
export certs
```

## All the certificates are stored in /root/ca. To export them into a given folder:

```bash
Usage: ./export.sh -i <intermediate-name> -c <certificate-name> -d <dest-folder> [-k] [-h]
  -h  Display help
  -i  name of the intermediate  
      (it's the /root/ca/<intermediate-name>)
  -c  name of the certificate ("intermediate" or client/server name) 
      (it's /root/ca/<intermediate-name>/certs/<CERT_NAME>.cert.pem and /root/ca/<intermediate-name>/private/<CERT_NAME>.cert.pem)
  -d  destination folder
  -k  exports the private key

Examples:

  to extract the intermediate "intermediate" (including private key) into ~/exported:
    ./export.sh -i intermediate -c intermediate -d ~/exported -k

  to extract the server "c474-node1.coelab.cloudera.com" (including private key) into ~/exported:
    ./export.sh -i intermediate -c c474-node1.coelab.cloudera.com -d ~/exported -k

  to extract the client "device3" (including private key) into ~/exported:
    ./export.sh -i intermediate -c device3 -d ~/exported -k

```

## View and verify certs
To optionally view the ROOT certificate:

```bash
sudo openssl x509 -noout -in /root/ca/certs/ca.cert.pem -noout -subject -issuer
```
To view the INTERMEDIATE certificates:

```bash
# NOTE: replace `<INTERMEDIATE>` with the intermediate name

sudo openssl x509 -noout -in <INTERMEDIATE>/certs/intermediate.cert.pem -noout -subject -issuer
```

To verify INTERMEDIATE against ROOT:
```bash
# NOTE: replace `<INTERMEDIATE>` with the intermediate name
sudo openssl verify -CAfile /root/CA/certs/ca.cert.pem /root/CA/<INTERMEDIATE>/certs/intermediate.cert.pem
```
