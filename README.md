### Generate TLS Server Cert
```
git clone https://github.com/cloudflare/cfssl.git 
go mod init cfssl
make
export PATH=$PATH:$PWD/bin 
cfssl print-defaults config > ca-config.json
cfssl print-defaults csr > ca-csr.json
```
Generate CA
```
cfssl gencert -initca ca-csr.json | cfssljson -bare ca -
```
You'll get following files:

ca-key.pem
ca.csr
ca.pem
Please keep ca-key.pem file in safe. 
This key allows to create any kind of certificates within your CA.
*.csr files are not used in our example.
```
cfssl print-defaults csr > server.json
```
Edit server.json

cfssl gencert -ca=ca.pem -ca-key=ca-key.pem -config=ca-config.json -profile=server server.json | cfssljson -bare server
You'll get following files:
server-key.pem
server.csr
server.pem


cfssl print-defaults csr > client.json
Edit client.json
You'll get following files:

client-key.pem
client.csr
client.pem



