# Server installation/configuration

**We assume that you have installed the operating system and you've aware of the basic commands**

This document describe the "basic" configuration of a new server using both "classical" approach and Docker approach.

## Creation of a new user

```bash
adduser newuser
ls -l /home/newuser
```

**_If the root rights are needed_**

```bash
su root _command_
```

- If the password need to be redefined :

```bash
passwd concernedUser
```

**For security purpose, be sure to connect with this user instead of root !**

## CRON tasks

**If needed, a online configurator is available for building the schedule of the task** :

[Crontab generator](https://crontab-generator.org/)

Once the periodicity define, create a new file :

```bash
touch /usr/bin/named_file.sh
chmod a+x /usr/bin/named_file.sh
nano named_file.sh # For example
```

- Example for apt-get update & upgrade commands ([Example file](CRON/update.sh)):

Copy the content needed into the file and save.

```bash
crontab –e
```

If needed, define the editor to nano or vim, once the cron task added/copied, save the file.
The console should display :

```bash
crontab: installing new crontab
```

## Git

```bash
apt-get install git -y
git --version # For verification purpose.
```

## Nginx

```bash
apt-get update -y && apt-get upgrade -y
apt-get install -y nginx
```

- Open the ipadress/ and check that Nginx homepage is visible.

## Apache

```bash
apt-get update -y && apt-get upgrade -y
apt-get install apache2 -y
```
- Open the ipaddress/ or www.domain.extension/ in browser

Should show the debian webpage.

# Cerbot (SSL certificate)

```bash
wget https://dl.eff.org/certbot-auto
chmod a+x certbot-auto
mv certbot-auto /usr/bin/certbot
certbot --apache (or --nginx)
```

- Open an www.domain.extension endpoint pointing into the server and make sure that the https:// endpoint is available.

- Define a CRON task for auto renew (Every 30 days here) :

```bash
crontab -e
```

```bash
0 0 30 * * /usr/bin/certbot renew >/dev/null 2>&1 # Adapt according to your installation.
```

Save the file and check that the success message is visible.

## DNS

```bash
apt-get update -y && apt-get upgrade -y
apt-get install bind9 -y
apt-get install bind9-doc -y # For evolution purpose
```

- If configuration :

```bash
cp /etc/bind/named.conf /etc/bind/named.conf.backup
/etc/init.d/bind9 restart
```

## Postfix (email sender)

```bash
apt-get install postfix -y
```

During the installation, choose "Internet website" and enter the desired email "placeholder".

## PostgreSQL

```bash
apt-get update && apt-get upgrade
apt-get install postgresql postgresql-client
su -u postgres psql
```

Once in the Postgres CLI :

```bash
\ password
```
Enter the desired password & repeat him.

- If you need to quit :

```bash
\ q
```

## MySQL

```bash
apt-get install mysql-server mysql-client -y
```

- Try to connect to the instance :

```bash
mysql -p userdefined -u passwordlinked
exit # If you need to close the CLI
```

# Server installation/configuration - DevOps

## Classical (Can be use inside a CRON task)

```bash
apt-get update -y && apt-get upgrade -y
```

## Docker + Docker-Compose + Docker Swarm

```bash
sudo apt-get install \ apt-transport-https \ ca-certificates \ curl \ gnupg2 \ software-properties-common -y
curl -fsSL https://download.docker.com/linux/debian/gpg | sudo apt-key add -
sudo add-apt-repository \ "deb [arch=amd64] https://download.docker.com/linux/debian \ $(lsb_release -cs) \ stable"
apt-get update -y && apt-get upgrade -y
apt-get install docker-ce -y
```

### Docker-Compose

[Documentation]('https://docs.docker.com/compose/install/')

### Docker Swarm

```bash
docker -v
docker swarm init
```

**_The Docker compose version is defined in the [Docker repository](https://github.com/docker/compose/releases), be sure top use the latest_**

**_For simplicity, the Swarm mode is activated in order to achieve the service approach_**

## Gitlab - Enterprise Edition
