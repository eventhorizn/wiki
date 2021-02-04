# Digital Ocean LAMP Setup

[Digital Ocean](https://www.digitalocean.com/) is a cloud service provider for deploying web apps

I'm using it for deploying personal web sites for my portfolio

## LAMP

[LAMP Stack](<https://en.wikipedia.org/wiki/LAMP_(software_bundle)>)

1. Linux (Ubuntu)
1. Apache
1. MySql
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

## Setup

DO has a LAMP image on the marketplace, but I opted to manually build my stack

### Generate SSH Key

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
1. When connecting to the server through putty you'll use this key

### Create Droplet

1. I chose the Ubuntu droplet
1. Create a SSH key
   - This is the public key you copied in the previous step
1. Pick whichever settings make sense
   - Size of box, hostname
1. Hit create
