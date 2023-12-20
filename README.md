# Final Project Sistem Pertahanan Jaringan

# SPJ-BabayoGank
Anggota:
1. Rizqy M Raihan (22.83.0797)
2. Ahmad Sri Bintang (22.83.0796)
3. Fayi' Subhi T (22.83.0808)
4. Egar Athwal M (22.83.0781)

# Latar Belakang
Kemajuan teknologi telah meningkatkan risiko keamanan online, termasuk serangan peretas (hackers), malware, dan serangan siber lainnya.
Web server merupakan target yang umum bagi para peretas karena berisi data berharga dan dapat memberikan akses ke sistem internal.

# Alat Yang Disiapkan
1. File ISO Ubuntu Server 22.04 LTS
2. VirtualBox

# Service Yang Diinstall
1. SSH
````
sudo apt install sshd
````
2. Cockpit
````
sudo apt install cockpit
````
# Konfigurasi OwnCloud
1. Create the occ helper script.
   
```
#!/bin/bash
 -u www-data php /var/www/owncloud/occ "$@"
````
```
sudo chmod +x occ
```

2. Install the required packages
````
sudo apt install apache2 php7.4 libapache2-mod-php7.4 php-mbstring php-xml php-mysql
````

3. Create a database for ownCloud.
````
sudo mysql -u root
CREATE DATABASE owncloud;
CREATE USER owncloud@localhost IDENTIFIED BY 'your_password';
GRANT ALL PRIVILEGES ON owncloud.* TO owncloud@localhost;
FLUSH PRIVILEGES;
exit
````

4. Download the ownCloud package.
````
wget https://download.owncloud.org/server/stable/owncloud-latest.tar.gz
````

5. Extract the package and copy it to the web root directory.
````
tar -zxvf owncloud-latest.tar.gz
sudo mv owncloud /var/www/owncloud
````

6. Set the ownership of the ownCloud directory to the web server user.
````
sudo chown -R www-data:www-data /var/www/owncloud
````

7. setting apache2 untuk berjalan port 80
````
sudo nano /etc/apache2/sites-available/owncloud.conf
<VirtualHost *:80>
  ServerName your_domain_name
  DocumentRoot /var/www/owncloud
  <Directory /var/www/owncloud>
    Options FollowSymLinks MultiViews
    AllowOverride All
    Order allow,deny
    allow from all
  </Directory>
</VirtualHost>
sudo a2ensite owncloud.conf
sudo systemctl restart apache2
````

# Konfigurasi Firewall
1. Aktifkan Firewall
````
ufw enable
````

2. Ijinkan Port Berjalan Di Ubuntu
````
ufw allow 'apache2'
ufw allow 'ssh'
ufw allow 9090
````


