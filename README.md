# Link do DockerHub:
https://hub.docker.com/r/ostrowski2000/my-ubuntu lub docker pull ostrowski2000/my-ubuntu

# Użyte polecenia:

mkdir certs

openssl req -newkey rsa:4096 -nodes -sha256 -keyout certs/domain.key -addext "subjectAltName = DNS:localhost" -x509 -days 365 -out certs/domain.crt

docker run -d --restart=always --name registry -v "C:\Users\postr\Desktop\POLLUB\SEMESTR 6\chmura\\certs:/certs" -e REGISTRY_HTTP_ADDR=0.0.0.0:443 -e REGISTRY_HTTP_TLS_CERTIFICATE=/certs/domain.crt -e REGISTRY_HTTP_TLS_KEY=/certs/domain.key -p 443:443 registry:2

docker pull ubuntu:16.04

docker tag ubuntu:16.04 localhost/my-ubuntu:v1

docker push localhost/my-ubuntu:v1

docker pull localhost/my-ubuntu:v1

curl -k https://localhost:443/v2/_catalog
{"repositories":["my-ubuntu"]}

docker tag localhost/my-ubuntu:v1 ostrowski2000/my-ubuntu

docker push ostrowski2000/my-ubuntu