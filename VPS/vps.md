# VPS configuration

## Configuring the host & domain

First, we need to create a symlink between our server and our user (for security purpose) :

```bash
cd /home/user/
mkdir www
mkdir www/_notedusite_
ln -s /home/monuser/www/__monsite__ /var/www/__nomdudossierdevotresite__
chown -hR monuser:users /home/monuser/www/
chmod -R 755 /home/nomuser/www/__monsite__
chown -hR monuser:users /var/www/__nomdudossierdevotresite__
chmod -R 755 /var/www/__nomdudossierdevotresite__
```

Then, let's verify if the symlink has been created :

```bash
ls -al /var/www/__nomdudossierdevotresite__
```

If everything goes right, we should see the symlink :

```bash
lrwxrwxrwx 1 monuser users --Date-- /var/www/__nomdudossierdevotresite__ -> /home/monuser/www/
```

If not, we should restart the process from :

```bash
cd /home/user/
...
```

### Creating the vhost configuration

Time to create the vhost configuration, first, wee need to create the file and
give it a name (mostly like the project) :

```bash
cp /etc/apache2/sites-available/000-default.conf /etc/apache2/sites-available/__monsite.conf__
nano /etc/apache2/sites-available/__monsite.conf__
```

Once the file is created and opened, let's create the configuration for the project :

```bash
<VirtualHost *:80>
    ServerAdmin email@domain.fr
    ServerName website.fr # Used for DNS resolution
    DocumentRoot /var/www/__nomdudossierdevotresite__/ # Could be without the "/" at the end.

    LogLevel warn
    ErrorLog /var/log/apache2/website-error_log.log
    CustomLog /var/log/apache2/website-access.log combined

    DirectoryIndex index.php # The file which contain the launch part of your application
</VirtualHost>
```

Now, let's save it and activate it into Apache, for saving file, use ``Ctrl + X`` then keep the filename ``__nomfichier.conf__`` then choose ``Yes``.

Once the file is saved, let's activate it within Apache :

```bash
a2ensite __monsite.conf__
```

If you have some errors :

```bash
systemctl status apache2.status # Should display the errors lines
nano /etc/apache2/sites-available/__monsite.conf__
```
