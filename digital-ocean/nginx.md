1. [Installing ngnix on Ubuntu](https://www.digitalocean.com/community/tutorials/how-to-install-nginx-on-ubuntu-20-04)
   - Sets up server blocks (same as apache virtual hosts)
1. [Securing Ngnix with Let's Encrypt](https://www.digitalocean.com/community/tutorials/how-to-secure-nginx-with-let-s-encrypt-on-ubuntu-20-04)
1. [Installing node.js](https://www.digitalocean.com/community/tutorials/how-to-set-up-a-node-js-application-for-production-on-ubuntu-16-04)
1. Bring code over to server
   - npm install where package is located
   ```
   pm2 start /var/www/site/app.js
   ```
1. Having trouble accessing mongo atlas, so installing mongodb manually
   - [Installation](https://www.digitalocean.com/community/tutorials/how-to-install-mongodb-from-the-default-apt-repositories-on-ubuntu-20-04)
   - [Integrating w/ Node](https://www.digitalocean.com/community/tutorials/how-to-integrate-mongodb-with-your-node-application)
   - Actually this was super smooth
1. I'm using sendgrid, so just need to add ips to that for it to work
   - Probably for swipe as well
