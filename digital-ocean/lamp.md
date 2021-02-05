# Digital Ocean LAMP Setup

[Digital Ocean](https://www.digitalocean.com/) is a cloud service provider for deploying web apps

I'm using it for deploying personal web sites for my portfolio

## LAMP

[LAMP Stack](<https://en.wikipedia.org/wiki/LAMP_(software_bundle)>)

1. Linux (Ubuntu)
1. Apache
1. MySql
   - phpMyAdmin Client
1. PHP

I've been getting interested in PHP, so my first foray into DO droplets was in setting up a lamp stack

## Recommended Software

1. [PuTTYGen](https://www.putty.org/)
   - Generating ssh keys
1. [PuTTY](https://www.putty.org/)
   - ssh into server once it's created
1. [WinSCP](https://winscp.net/eng/download.php)
   - Editing on server
   - Copying code to server

# Setup

DO has a LAMP image on the marketplace, but I opted to manually build my stack

## Generate SSH Key

[DO Walkthrough](https://www.digitalocean.com/docs/droplets/how-to/add-ssh-keys/create-with-putty/)

1. Open PuttyGen
   - ![](images/putty-gen.png)
1. RSA is default and fine for our purposes
1. Click Generate (and move the mouse when prompted)
1. Public key will be generated
   - This is what you will copy and use in DO
1. You'll be prompted for a passphrase
   - You'll be prompted when accessing server
1. Save the private key after
   - Public key is what you pasted to DO
1. When connecting to the server through putty you'll use this key

## Create Droplet

1. I chose the Ubuntu droplet
1. Create a SSH key
   - This is the public key you copied in the previous step
1. Pick whichever settings make sense
   - Size of box, hostname
1. Hit create
1. So, I never get emailed the inital root password to the linux box
   - Manually reset the password
   - It will then email you the new temp password
     ![](images/droplet-pwd-reset.png)

## Connect Putty to Linux Box

- Digital Ocean does have a built in console
  - It tends to go dead quickly

[DO Documentation](https://www.digitalocean.com/docs/droplets/how-to/connect-with-ssh/putty/)

1. Fill in host name on putty configuration
   - Port 22
1. Verify SSH Protocol
   - Left nav, SSH
   - Make sure 2 is selected for ssh protocol version
1. Specify an SSH key
   - Under SSH Key, there's an Auth section
   - Browse for the private key (ends in .ppk)
1. Add Username
   - 'root' to start
   - After you've logged in, you'll create a non root sudo user, update this after
   - Bad form to use root all the time
1. Save the Session!
   - Pain in the ass if you don't
1. First time connecting
   - Putty will ask to confirm you trust the server (say yes)
1. You're in!
   - Refer to DO Documentation if you ran into problems

## Initial Server Setup

[DO Documentation](https://www.digitalocean.com/community/tutorials/initial-server-setup-with-ubuntu-20-04)

1. Create a new user
   ```bash
   adduser gary
   ```
   - You will be asked questions about the user (name, etc)
1. Grant Admin Privileges
   ```bash
   usermod -aG sudo gary
   ```
1. Set up basic firewall
   - Ubuntu servers can use the UFW firewall to make sure only connections to certain services are allowed
   ```bash
   ufw app list
   ```
   - This shows that we only have OpenSSH available, but not enabled
   ```bash
   ufw allow OpenSSH
   ufw enable
   ufw status
   ```
   - Only SSH connections are allowed. We will add more as we need them
1. Enable external access for your regular user

   - We are using ssh authentication
   - We are going to copy the root user's ssh directory to our created user

   ```bash
   rsync --archive --chown=gary:gary ~/.ssh /home/gary
   ```

   - You'll have to `sudo` everything, and will be prompted occasionally for your password
     - Safer this way!

## LAMP Stack

[DO Documentation](https://www.digitalocean.com/community/tutorials/how-to-install-linux-apache-mysql-php-lamp-stack-on-ubuntu-20-04)

### Apache

1. Important, do all of this as your non root user
   - It's a big no-no to run everything as root
1. Install Apache
   ```bash
   sudo apt update
   sudo apt install apache2
   ```
1. Update firewall to allow apache
   ```bash
   sudo ufw app list
   ```
   - You'll see Apache, Apache Full, Apache Secure available
   - Walkthrough above has you just install Apache, we're gonna eventually want ssl, so do full
   ```
   sudo ufw allow in "Apache Full"
   ```
1. Go to `http://your_server_ip`
   - ip address is available on DigitalOcean
   - We will do DNS links later
     ![](images/apache-default.png)

### Install MySql

1. Initial install
   ```bash
   sudo apt install mysql-server
   ```
1. Once finished, run a security script that comes pre-installed
   ```bash
   sudo mysql_secure_installation
   ```
   - This will ask if you want to configure the VALIDATE PASSWORD PLUGIN
   - I vote no, it causes issues w/ phpMyAdmin later
   - Press Y and enter at each prompt
     - Removes anonymous users and the test db

## Install PHPMyAdmin

[DO Documentation](https://www.digitalocean.com/community/tutorials/how-to-install-and-secure-phpmyadmin-on-ubuntu-20-04)

1. Once the dabase is installed, I recommend a sql client to manage it
   - Command line sql is no fun
1. Install phpMyAdmin

   ```bash
   sudo apt update

   sudo apt install phpmyadmin php-mbstring php-zip php-gd php-json php-curl
   ```

1. VERY IMPORTANT
   - When the first prompt appears, apache2 is highlighted, but not selected
   - If you do not hit "SPACE" to select Apache, the installer will not move the necessary files during installation
   - Hit "SPACE", "TAB", and then "ENTER" to select Apache.
1. If you mess that up, no worries, run the below commands
   ```bash
   sudo ln -s /etc/phpmyadmin/apache.conf /etc/apache2/conf-available/phpmyadmin.conf
   sudo a2enconf phpmyadmin
   sudo /etc/init.d/apache2 reload
   ```
1. If you set up a non root user during MySql setup, you can use that use to log into phpMyAdmin
1. If you are using root, you need to configure the password

   ```bash
   sudo mysql
   ```

   ```sql
   SELECT user,authentication_string,plugin,host FROM mysql.user;
   ```

   - Notice how the admin is using the 'auth_socket'
   - We need to change that to `mysql_native_password`

   ```sql
   ALTER USER 'root'@'localhost' IDENTIFIED WITH mysql_native_password BY 'password';
   ```

1. It's recommended to further protect your phpMyAdmin instance by requiring it's own password to access

   - First enable use of .htaccess file overrides by editing the config file
   - Use WinSCP (or edit in bash) `/etc/apache2/conf-available/phpmyadmin.conf`
   - Edit the `/etc/phpmyadmin/apache.conf` if you went the symbolic link route
   - Add `AllowOverride All`

   ```conf
   <Directory /usr/share/phpmyadmin>
    Options SymLinksIfOwnerMatch
    DirectoryIndex index.php
    AllowOverride All
    . . .
   ```

   - Restart apache

   ```
   sudo systemctl restart apache2
   ```

   - Edit `/usr/share/phpmyadmin/.htaccess`

   ```conf
   AuthType Basic
   AuthName "Restricted Files"
   AuthUserFile /etc/phpmyadmin/.htpasswd
   Require valid-user
   ```

   - Create a password file

   ```bash
   sudo htpasswd -c /etc/phpmyadmin/.htpasswd username
   ```

   - You will be prompted to select and confirm a password
   - Create a user

   ```bash
   sudo htpasswd /etc/phpmyadmin/.htpasswd additionaluser
   ```

   - Restart apache `sudo systemctl restart apache2`

1. Now when you access phpMyAdmin it will prompt you for a username and password
   - I didn't end up doing this step, as signing in as the db user is enough for my purposes
