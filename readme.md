Letsencrypt cert generation testing with Docker and NGINX
---------------

Mainly done using instructions from https://www.humankode.com/ssl/how-to-set-up-free-ssl-certificates-from-lets-encrypt-using-docker-and-nginx

Staging command to test asking for the certs:

```sh
docker run -it --rm \
	-v $(pwd)/tmp-volumes/etc/letsencrypt:/etc/letsencrypt \
	-v $(pwd)/tmp-volumes/var/lib/letsencrypt:/var/lib/letsencrypt \
	-v $(pwd)/site:/data/letsencrypt \
	-v $(pwd)/tmp-volumes/var/log/letsencrypt:/var/log/letsencrypt \
	certbot/certbot \
	certonly --webroot \
	--register-unsafely-without-email --agree-tos \
	--webroot-path=/data/letsencrypt \
	--staging \
	-d *.kjaanson.ee
```

Actual cert generation command

```
docker run -it --rm \
	-v $(pwd)/tmp-volumes/etc/letsencrypt:/etc/letsencrypt \
	-v $(pwd)/tmp-volumes/var/lib/letsencrypt:/var/lib/letsencrypt \
	-v $(pwd)/site:/data/letsencrypt \
	-v $(pwd)/tmp-volumes/var/log/letsencrypt:/var/log/letsencrypt \
	certbot/certbot \
	certonly --webroot \
	--email kjaanson@gmail.com --agree-tos --no-eff-email \
	--webroot-path=/data/letsencrypt \
	-d kjaanson.ee -d www.kjaanson.ee
```

