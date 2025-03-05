Самоподписанный сертификат
======

файл v3.ext
```text
authorityKeyIdentifier=keyid,issuer
basicConstraints=CA:FALSE
keyUsage = digitalSignature, nonRepudiation, keyEncipherment, dataEncipherment
subjectAltName = @alt_names

[alt_names]
DNS.1 = %%DOMAIN%%
DNS.2 = *.%%DOMAIN%%
```

Скрипт для генерации самоподписанного сертификата
```bash
set -e
BASE_CERTS_DIR=containers/nginx/certs/
FILE_ROOT_CA_KEY=${BASE_CERTS_DIR}rootCA.key
FILE_ROOT_CA_PEM=${BASE_CERTS_DIR}rootCA.pem
FILE_DEVICE_KEY=${BASE_CERTS_DIR}device.key
FILE_DEVICE_CSR=${BASE_CERTS_DIR}device.csr
FILE_DEVICE_CRT=${BASE_CERTS_DIR}device.crt
FILE_V3=${BASE_CERTS_DIR}v3.ext
FILE_V3_TMP=${BASE_CERTS_DIR}tmp_v3.ext
DOMAIN=${1:-"example.localhost"}
COMMON_NAME=${2:-$DOMAIN}
SUBJECT="/C=CA/ST=None/L=NB/O=None/CN=$COMMON_NAME"
NUM_OF_DAYS=1024
FILE_DOMAIN_CSR=${BASE_CERTS_DIR}$DOMAIN.csr
FILE_DOMAIN_CRT=${BASE_CERTS_DIR}$DOMAIN.crt

if [ ! -f $FILE_ROOT_CA_KEY ]; then
  echo generating $FILE_ROOT_CA_KEY
  openssl genrsa -out $FILE_ROOT_CA_KEY 2048
else
  echo $FILE_ROOT_CA_KEY exists
fi

if [ -f $FILE_ROOT_CA_KEY -a ! -f $FILE_ROOT_CA_PEM ]; then
  echo generating $FILE_ROOT_CA_PEM
  openssl req -x509 -new -nodes -key $FILE_ROOT_CA_KEY -sha256 -days $NUM_OF_DAYS -subj "$SUBJECT" -out $FILE_ROOT_CA_PEM
else
  echo $FILE_ROOT_CA_PEM exists
fi

if [ -f $FILE_DEVICE_KEY ]; then
  KEY_OPT="-key"
else
  KEY_OPT="-keyout"
fi

if [ ! -f $FILE_DEVICE_CSR ]; then
  echo generating $FILE_DEVICE_CSR
  openssl req -new -newkey rsa:2048 -sha256 -nodes $KEY_OPT $FILE_DEVICE_KEY -subj "$SUBJECT" -out $FILE_DEVICE_CSR
else
  echo $FILE_DEVICE_CSR exists
fi

if [ ! -f $FILE_DEVICE_CRT ]; then
  if [ -f $FILE_V3 ]; then
    echo generating $FILE_DEVICE_CRT
    cat $FILE_V3 | sed s/%%DOMAIN%%/$COMMON_NAME/g > $FILE_V3_TMP
    openssl x509 -req -in $FILE_DEVICE_CSR -CA $FILE_ROOT_CA_PEM -CAkey $FILE_ROOT_CA_KEY -CAcreateserial -out $FILE_DEVICE_CRT -days $NUM_OF_DAYS -sha256 -extfile $FILE_V3_TMP
  else
    echo file $FILE_V3 not exists
    exit 1
  fi
else
  echo $FILE_DEVICE_CRT exists
fi

mv $FILE_DEVICE_CSR $FILE_DOMAIN_CSR
mv $FILE_DEVICE_CRT $FILE_DOMAIN_CRT
```

nginx default.conf
```text
server {
    listen 80 default;
    listen              443 ssl;
    server_name _;
    ssl_certificate     /etc/nginx/certs/example.localhost.crt;
    ssl_certificate_key /etc/nginx/certs/device.key;
    ssl_protocols       TLSv1 TLSv1.1 TLSv1.2;
    ssl_ciphers         EECDH+CHACHA20:EECDH+AES128:RSA+AES128:EECDH+AES256:RSA+AES256:EECDH+3DES:RSA+3DES:!MD5;
    ...
}
```