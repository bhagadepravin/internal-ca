#### Auto TLS Use case 3
https://docs.cloudera.com/cdp-private-cloud-base/7.1.3/security-encrypting-data-in-transit/topics/cm-security-use-case-2.html

```bash
# run export script to export certs

mkdir /tmp/auto-tls/
cp /home/intermediate-ca-chain.cert.pem /tmp/auto-tls/ca-certs.pem
cp /home/intermediate-praveen717-1.praveen717.root.hwx.site.cert.pem /tmp/auto-tls/certificate.pem
cp /home/intermediate-praveen717-1.praveen717.root.hwx.site.key.pem /tmp/auto-tls/key.pem
echo "Welcome" > /tmp/auto-tls/key.pwd
echo "Welcome@123" > /tmp/auto-tls/truststore.pwd
chmod 444 /tmp/auto-tls/*

mkdir /opt/cloudera/AutoTLS
chown cloudera-scm:cloudera-scm /opt/cloudera/AutoTLS

# Run curl cmd for Auto-TLS Use Case 3:
https://github.com/bhagadepravin/commands/blob/master/cm.md#auto-tls-using-existing-certificate-use-case-3

service cloudera-scm-server restart
```
