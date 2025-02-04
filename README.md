# <b>Faveo Helpdesk Docker</b>

A pretty simplified Docker Compose workflow that sets up a network of containers for Faveo Helpdesk.

All the Faveo Helpdesk editions are supported except the community edition.

## <b>Usage</b>
___

To get started, make sure you have Docker and Docker-Compose installed on your system, and then clone the below Git-Hub repository with the below link.

```sh
git clone https://github.com/vvitsivakumar/faveo_dockerscript_installation.git
```

---
Next, navigate in your terminal to the directory you cloned this, and give the executable permissions to bash scripts.

#### For all Faveo Editions (except community edition).

```sh
chmod +x faveo-run.sh
```

#### For Faveo Community Edition.

```sh
chmod +x faveo-community-run.sh
```
---

### <b>Prerequisites To run the script:</b>

1. A valid domain name fully propagated to your Server's IP.
2. Sudo Privilege.
3. Faveo license and Order number. (this can be obtained from billing https://billing.faveohelpdesk.com).<b> (This is not required for Community Edition)</b>
4. Unreserved ports 80 and 443. (If it is reserved feel free to edit and change the ports of your choice in docker-copompose.yml)
5. Operating Systems Centos 7,8 or above and Ubuntu 16,18,20,22.
6. SSL Certificate (For Paid SSL Users), If you're using a paid SSL, have the SSL certificate files ready before installation.

### <b>Complete the below steps to get the Containers up.</b>

---

#### <b>For all Faveo Editons (except community edition).</b>

<b>Run the script "faveo-run.sh" by passing the necessary arguments.</b>

Note- You should have a Valid domain name pointing to your public IP. This domain name is used to obtain SSL certificates, and the mail is used for the same purpose. The license code and Order Number can be obtained from your Faveo Helpdesk Billing portal, and make sure not to include the '#' character in the Order Number.

SSL Certificate Options: (Pass the option based on your SSL requirement)

- Option A: Let’s Encrypt (Free SSL)

- Option B: Self-Signed SSL

- Option C: Paid SSL (Ensure your SSL files are ready in your system) If you choose Option C (Paid SSL), you must specify the paths of the SSL certificate files:
SSL Certificate Path: /path/to/certificate.crt
SSL Key Path: /path/to/private.key
SSL CA Bundle : /path/to/ca_bundle.crt

Usage:
```sh
 ./faveo-run.sh -domainname <your domainname> -email <example@email.com> -license <faveo license code> -orderno <faveo order number> -ssl <SSL Option>
```
Example: It should look something like this.
```sh
 ./faveo-run.sh -domainname berserker.tk -email berserkertest@gmail.com -license 5H876********** -orderno 8123****** -ssl <A|B|C>
```
#### <b>For Faveo Community Edition.</b>

<b>Run the script "faveo-communtiy-run.sh" by passing the necessary arguments.</b>

Note- You should have a Valid domain name pointing to your public IP. This domain name is used to obtain SSL certificates, and the mail is used for the same purpose.


SSL Certificate Options: (Pass the option based on your SSL requirement)

- Option A: Let’s Encrypt (Free SSL)

- Option B: Self-Signed SSL

- Option C: Paid SSL (Ensure your SSL files are ready in your system) If you choose Option C (Paid SSL), you must specify the paths of the SSL certificate files:
SSL Certificate Path: /path/to/certificate.crt
SSL Key Path: /path/to/private.key
SSL CA Bundle : /path/to/ca_bundle.crt


Usage:
```sh
 ./faveo-community-run.sh -domainname <your domainname> -email <example@email.com> -ssl <SSL Option>
```
Example: It should look something like this.
```sh
 ./faveo-community-run.sh -domainname berserker.tk -email berserkertest@gmail.com -ssl <A|B|C>
```
---
After the docker installation is completed you will be prompted with Database Credentials and Credentials are saved in filename "" them somewhere safe and a cronjob will be set to auto-renew SSL certificates from Letsencrypt

Visit https://yourdomainname complete the readiness probe, input the Database Details when prompted, and complete the installation.

There is one final step that needs to be done to complete the installation. You have to edit the .env file which is generated under the Faveo root directory after completing the installation in the browser. Open the terminal and navigate to the faveo-docker directory here you will find the directory "faveo" which is downloaded while running the script this directory contains all the Helpdesk codebase, inside it, you need to edit the ".env" file and add REDIS_HOST=faveo-redis. The "faveo-redis" is the DNS name of the Redis container. Finally, run the below command for changes to take effect.

For LetsEncrypt SSL & Paid SSL

```sh
  docker compose down && docker compose up -d
```

Only For Self-Signed SSL

```sh
chmod +x composedownup.sh
./composedownup.sh*
```
---
---

<p class="notice--warning">
Note: At this point, the helpdesk interface will not load in the browser. To finalize the installation, you need to remove specific entries from the database.
</p>

- Access your MariaDB container using the following command:

```
docker exec -it YourDomain-mariadb /bin/bash
```
Replace <code><b>YourDomain</b></code> by the actual domain name.

- Enter the database by executing:

```
mysql -u root -pYourPassword
use faveo;
```

- Remove the necessary entry from the plugins table:

```
DELETE FROM plugins WHERE name = '';
```

Once the entry is removed, you can access the helpdesk via the browser and continue using it.

---
---

































## Faveo Helpdesk Docker

A pretty simplified Docker Compose workflow set up a network of containers for the Faveo Helpdesk.
All the Faveo Helpdesk editions are supported.

## Usage
___

Before getting started, make sure you have Docker and docker-compose installed on your system, and then clone this repository.


```sh
git clone https://github.com/ladybirdweb/faveo-helpdesk-docker-v2.git
```
---

Next, navigate to your terminal to the directory you cloned this, and give the executable permission to bash scripts.

### For all Faveo Edition (excpet community edition):

```sh
chmod +x faveo-run.sh
```

### For Faveo Community Edition:

```sh
chmod +x faveo-community-run.sh
```
---
## Prerequisites to run the script:

A valid domain name wholly propagated to your Server's IP.
Sudo Privilege.
Faveo license and Order number.
Unreserved ports 80 and 443. (If it is reserved, feel free to edit and change the ports of your choice in docker-copompose.yml)
Operating Systems Centos 7,8 or above, and Ubuntu 16,18,20.

## To get the Containers up and running, follow the instructions below.
---
### Run the script "faveo-run.sh" by passing the necessary arguments for Faveo Editions (except Faveo Community Edition).

Note- You should have a Valid domain name pointing to your public IP. This domain name is used to obtain SSL certificates from Let's Encrypt CA, and the mail is used for the same purpose. The license code and Order Number can be obtained from your Faveo Helpdesk Billing portal, and make sure not to include the '#' character in the Order Number.

Usage:
```sh
 ./faveo-run.sh -domainname <your domainname> -email <example@email.com> -license <faveo license code> -orderno <faveo order number>
```
Example: It should look something like this.
```sh
 ./faveo-run.sh -domainname berserker.tk -email berserkertest@gmail.com -license 5H876********** -orderno 8123******
```
### Run the script "faveo-communtiy-run.sh" by passing the necessary arguments for Faveo Community Edition.

Note- You should have a Valid domain name pointing to your public IP. This domain name is used to obtain SSL certificates from Let's Encrypt CA, and the mail is used for the same purpose.

Usage:
```sh
 ./faveo-community-run.sh -domainname <your domainname> -email <example@email.com> 
```
Example: It should look something like this.
```sh
 ./faveo-community-run.sh -domainname berserker.tk -email berserkertest@gmail.com
```
---
After completing the Docker installation, you will be prompted with Database Credentials, which you should copy and keep somewhere secure, and a cron job to automatically renew SSL certificates from Let's encrypt. 

Visit https://yourdomainname complete the readiness probe, enter the Database information when prompted, and finish the installation.

One final step has to be done before the installation is complete. You have to edit the .env file which is generated under the Faveo root directory, after completing the installation process in the browser. Open a terminal and navigate to the faveo-docker directory. Here, you will find the directory "faveo" which is downloaded, while running the script. This directory contains all the Helpdesk codebase inside it. You need to edit the ".env" file and add REDIS_HOST=faveo-Redis. The "faveo-redis" is the DNS name of the Redis container. Finally, run the below command for changes to take effect.

```sh
	docker compose down && docker compose up -d
```
	



