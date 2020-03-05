**[Donate :moneybag: with PayPal](https://www.paypal.com/cgi-bin/webscr?cmd=_s-xclick&hosted_button_id=WKWS26A57WHJG)**
_keeps the KIRI server alive and some coffee for the maintainers_

# New Menjangan #

## Installation Guide ##

All guides in Ubuntu.

1. Prepare one user and add to `sudo` group. Then login as that user.
2. Install Java 8 (`sudo apt install openjdk-8-jre openjdk-8-jdk`)
3. Install Git (`sudo apt-get install git`)
4. Clone repository (`git clone https://github.com/projectkiri/NewMenjangan.git`)
5. Configure database parameter: set appropriate values in `~/NewMenjangan/dist/etc/mysql.properties`
6. Test NewMenjangan that it is capable to run:
    1. Update `dist/NewMenjangan.sh`, set the value of `NEWMJNSERVE_HOME` part into your own directory (Basically that's where your `NewMenjangan.sh` resides)
    2. In `dist/`, type `./NewMenjangan.sh`
    3. Type `Ctrl+C` to exit
7. Register in cronjob to execute at start

## MySQL Server Installation ##

Reference from http://azure.microsoft.com/blog/2014/09/02/create-your-own-dedicated-mysql-server-for-your-azure-websites/

1. Install Server `sudo apt-get install mysql-server mysql-client`
2. Check service `sudo service mysql status`
3. Open port 3306 `sudo iptables -A INPUT -i eth0 -p tcp -m tcp --dport 3306 -j ACCEPT`
4. Check port `sudo netstat -anltp|grep :3306`
5. Create SSH tunnel `sudo ssh -fNg -L 3307:127.0.0.1:3306 pascal@newmenjangan.cloudapp.net`
6. Create an endpoint for the port 3307 in the dashboard of the VM in Azure
7. Connect to mysql `mysql -u root -p`
    * Create user `CREATE USER 'tirtayasa'@'%' IDENTIFIED BY '***';`
    * Create database `CREATE DATABASE tirtayasa`
    * Grant privileges `GRANT ALL PRIVILEGES ON tirtayasa.* TO 'tirtayasa'@'%';`
    * Flush privileges `FLUSH PRIVILEGES;`
8. Fill tables using phpmyadmin

## Troubleshooting Guide ##

### Failed to refresh data: javax.net.ssl.SSLHandshakeException ###

This app pulls data from <https://angkot.web.id>. Unfortunately in some evnironment, this app is unable to verify certificate authenticity. For a workaround (you may also not do this if there's no problem at all):

1. Open <https://angkot.web.id> in your browser, and look for the certificate path.
2. Export "GlobalSign Domain Validation CA" certificate (or whatever between root and angkot.web.id)
3. Import this certificate to java runtime, for example `sudo keytool -import -alias globalsigndomain -file ~/globalsigndomain.cer -keystore /usr/lib/jvm/java-7-openjdk-amd64/jre/lib/security/cacerts`
