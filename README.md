fauria/letsencrypt
==================

![docker_logo](https://raw.githubusercontent.com/fauria/docker-letsencrypt/master/docker_139x115.png)![docker_fauria_logo](https://raw.githubusercontent.com/fauria/docker-letsencrypt/master/docker_fauria_161x115.png)

This Docker image helps with the creation of [Let’s Encrypt](https://letsencrypt.org) SSL certificates.

It uses the [Certbot](https://certbot.eff.org/) client by the [Electronic Frontier Foundation](https://www.eff.org/) to request and store the certificate and related files.

Installation from [Docker registry hub](https://registry.hub.docker.com/u/fauria/letsencrypt/).
----

Pull the image using the following command:

```bash
docker pull fauria/letsencrypt
```

Exposed volumes
----

The image exposes a volume for `/web`, where a publicly accessible root directory of the website should be linked, and `/etc/letsencrypt/archive`, containing the generetated files. 

The directory strucutre is as follows:

```
example.com (FQDN)
|-- certX.pem (Certificate for example.com)
|-- chainX.pem (Let’s Encrypt intermediate certificate)
|-- fullchainX.pem (Above certificates) 
`-- privkeyX.pem (Private key for example.com)
```

Use cases
----

#### Create a certificate for example.com

###### Note: The root directory of this site is located at `/my/website/directory` and want the certificate to be stored in `/my/certificates/directory`.

```
docker run -v /my/website/directory:/web -v /my/certificates/directory:/etc/letsencrypt/archive fauria/letsencrypt example.com --email example@example.com
```

Remember that the generated certificate will be valid for three months, so you migh want to program the execution of the above command with cron to automatically keep it up to date.