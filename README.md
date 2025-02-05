# SSL-apache2
This repository explains how to install apache2 with SSL.
Install apache2 by using apt command:
<pre>
$ sudo apt install apache2 apache2-utils
</pre>
Install certbot in order to generate SSL three certificates (cert.pem, privkey.pem, chain.pem)
<pre>
$ sudo apt update
$ sudo apt upgrade
$ sudo apt install certbot
</pre>
Run the following command to generate SSL three certificates where neuro.dob.jp is the SSL apache server:
<pre>
$ sudo certbot certonly --webroot -w /var/www/html -d neuro.dob.jp
</pre>
SSL three certificates (cert.pem, privkey.pem, chain.pem) will be generated at /etc/letsencrypt/live/neuro.dob.jp/ folder. 
Therefore, we must make sure that /etc/apache2/sites-available/default-ssl.conf file must be modified or added as follows:
<pre>
SSLCertificateFile      /etc/letsencrypt/live/neuro.dob.jp/cert.pem
SSLCertificateKeyFile   /etc/letsencrypt/live/neuro.dob.jp/privkey.pem
SSLCertificateChainFile /etc/letsencrypt/live/neuro.dob.jp/chain.pem
</pre>
We must run the following commands to run SSL-apache2.
<pre>
$ sudo a2enmod ssl
$ sudo a2ensite default-ssl
In order to activate a private site of ~/public_html directory, 
 run the following command:
$ sudo a2enmod userdir
 For example, make your home directory readable
$ chmod 755 /home/takefuji 
$ sudo systemctl restart apache2
</pre>
