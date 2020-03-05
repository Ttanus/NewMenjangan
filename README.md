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
7. Register in cronjob to execute at start:
    1. Type `crontab -e`
    2. Add this line: `@reboot /home/pascal/NewMenjangan/dist/NewMenjangan.sh` (change my name with your username)
