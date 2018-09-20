---
description: >-
  This is a step by step instruction of how to setup and run an elastic node on
  a dedicated server, or VPS including Ubuntu 16.04.
---

# Linux - tutorial

## Preparing a Server for Client installation

How to connect to your new server?

If you are using Windows, download the latest [**Putty**](https://www.chiark.greenend.org.uk/~sgtatham/putty/latest.html) Client and use these  instructions to connect to your server:

{% code-tabs %}
{% code-tabs-item title="\#putty\_guide" %}
```http
https://mediatemple.net/community/products/dv/204404604/using-ssh-in-putty-
```
{% endcode-tabs-item %}
{% endcode-tabs %}

If you are using Linux, start your console \(Alt+Ctrl+T\) and type:

{% code-tabs %}
{% code-tabs-item title="\#run" %}
```bash
ssh username@youriporhostname.xyz
```
{% endcode-tabs-item %}
{% endcode-tabs %}

 Once you are logged in you will start the installation of dependencies for your Elastic node to compile

{% code-tabs %}
{% code-tabs-item title="\#run" %}
```bash
sudo apt update && sudo apt upgrade && sudo apt dist-upgrade
```
{% endcode-tabs-item %}
{% endcode-tabs %}

\(at this point, if you don’t have sudo installed and you are using a root account, just remove sudo from all the commands that will be shown in this tutorial\)

 Install some basic packages

{% code-tabs %}
{% code-tabs-item title="\#run" %}
```bash
sudo apt install mc ntp fail2ban htop screen nano -y
```
{% endcode-tabs-item %}
{% endcode-tabs %}

 Install Java

{% code-tabs %}
{% code-tabs-item title="\#run" %}
```bash
sudo apt install software-properties-common -y

sudo add-apt-repository ppa:webupd8team/java

sudo apt update

sudo apt install oracle-java8-installer -y
```
{% endcode-tabs-item %}
{% endcode-tabs %}

\(You’ll be prompt here to accept some TOS/License.\)

 After that, verify that your Java is installed in the right version

{% code-tabs %}
{% code-tabs-item title="\#run" %}
```bash
java -version
```
{% endcode-tabs-item %}
{% endcode-tabs %}

 You should see something like this:

{% code-tabs %}
{% code-tabs-item title="\#output" %}
```bash
Java version "1.8.0_121"

Java(TM) SE Runtime Environment (build 1.8.0_121-b13)

Java HotSpot(TM) 64-Bit Server VM (build 25.121-b13, mixed mode)
```
{% endcode-tabs-item %}
{% endcode-tabs %}

\(Make sure Java is at 1.8.x because it’s currently supported by Elastic.\)

## Installing elastic client

{% hint style="info" %}
Remember not to run Elastic as root user! 
{% endhint %}

If at this point you are logged in as root user, create a new account and do the rest of the command with this new user. You can skip this step if you have access to a normal user.

{% code-tabs %}
{% code-tabs-item title="\#run" %}
```bash
adduser elastic
```
{% endcode-tabs-item %}
{% endcode-tabs %}

You’ll be asked some questions about the user. Just drop some data. Then set a password for the new user. Remember that the password needs to be strong \(min 16 chars, min one upper case letter, min one lower case letter, min one number\). Use a password generator if you don’t want to burn your brain, but remember to keep that password in some safe place.

{% code-tabs %}
{% code-tabs-item title="\#run" %}
```bash
passwd elastic
```
{% endcode-tabs-item %}
{% endcode-tabs %}

Logout from root account. We don’t need it anymore. 

{% hint style="info" %}
Remember not to login to root account anymore! 
{% endhint %}

If by accident you’ll login to your root account and run for example Elastic from it, some file permission will change and you’ll not be able to run Elastic with this newly created user anymore.

{% code-tabs %}
{% code-tabs-item title="\#run" %}
```bash
exit
```
{% endcode-tabs-item %}
{% endcode-tabs %}

Login as elastic this time typing your newly created password. You should be in your home directory now. Check it by typing

{% code-tabs %}
{% code-tabs-item title="\#run" %}
```bash
pwd
```
{% endcode-tabs-item %}
{% endcode-tabs %}

You should see

{% code-tabs %}
{% code-tabs-item title="\#output" %}
```bash
/home/elastic
```
{% endcode-tabs-item %}
{% endcode-tabs %}

Launch MC and hit F7 to create a new directory. Name it ‘elastic’ as well \(without quotes of course\). Go to this directory and minimize MC \(Ctrl + O\).

Paste/type

{% code-tabs %}
{% code-tabs-item title="\#run" %}
```bash
git clone https://github.com/xel-software/Litewallet-Mainnet.git 
```
{% endcode-tabs-item %}
{% endcode-tabs %}

Maximize MC \(Ctrl + O\) and go to the Litewallet-Mainnet directory. Minimize and

{% code-tabs %}
{% code-tabs-item title="\#run" %}
```bash
./compile.sh
```
{% endcode-tabs-item %}
{% endcode-tabs %}

Maximize, and this time you have to exit MC \(F10\). You need to go to the Litewallet-Mainnet directory manually because you will need to launch it in screen. So if you have directory structure like mentioned before, you can type:

{% code-tabs %}
{% code-tabs-item title="\#run" %}
```bash
cd /home/elastic/elastic/Litewallet-Mainnet
```
{% endcode-tabs-item %}
{% endcode-tabs %}

And you should be in Litewallet-Mainnet directory. If your username is different \(i.e ubuntu\) type:

{% code-tabs %}
{% code-tabs-item title="\#run" %}
```bash
cd /home/ubuntu/elastic/Litewallet-Mainnet
```
{% endcode-tabs-item %}
{% endcode-tabs %}

Hope you get the idea. If you for some reason lost, read about ‘ls’ command it will help navigate listing files and directories in directory you currently are.

If you’re in Litewallet-Mainnet directory type

{% code-tabs %}
{% code-tabs-item title="\#run" %}
```bash
screen ./run.sh
```
{% endcode-tabs-item %}
{% endcode-tabs %}

What this command do it’ll pull latest changes from github, compile it with maven and launch Elastic. Check if everything launch as it should.

{% hint style="info" %}
If you want to go back from screen to your server console **LEAVING Elastic running in background** hit Ctrl \(hold it\), now hit A key **and release it** and hit D key. 
{% endhint %}

You should be back in console and Elastic is running in background so if you exit your server Elastic will be still running.  
If you want to go back to Elastic \(for example to shutdown it\) type

{% code-tabs %}
{% code-tabs-item title="\#run" %}
```bash
screen -r
```
{% endcode-tabs-item %}
{% endcode-tabs %}

This command should bring your screen instance of elastic \(even if you login to your node next time\)  
If you want to shutdown elastic hit Ctrl + C. elastic and screen itself should exit.

Now \(once Elastic is down\) i.e. you can update Elastic to the newest version and launch it again

{% code-tabs %}
{% code-tabs-item title="\#run" %}
```bash
cd /home/elastic/elastic/Litewallet-Mainnet

git pull

./compile.sh

screen ./run.sh
```
{% endcode-tabs-item %}
{% endcode-tabs %}

At this point you have full relay node up and runnig! You are already helping the network, you don’t need to know anything more if you just wanted to help with relay blocks/txs. Just remember to update your node when a new version will show up.

But you might also want to login to your wallet with the browser to start forging for example \(or just see if it work as it should, see blocks, txs etc\).  
You’ll also need to create an SSL cert to protect yourself against Main-In-The-Middle attack.

First, you need to stop your Elastic node \(see above\) and do some config change in order to be able to access it remotely.

Next, we need to generate an SSL certificate

{% code-tabs %}
{% code-tabs-item title="\#run" %}
```bash
cd /home/elastic/elastic/Litewallet-Mainnet
```
{% endcode-tabs-item %}
{% endcode-tabs %}

{% code-tabs %}
{% code-tabs-item title="\#run" %}
```bash
keytool -genkeypair -keyalg RSA -keysize 2048 -validity 3650 -keystore keystore
```
{% endcode-tabs-item %}
{% endcode-tabs %}

You’ll be asked here for some basic info about your certificate \(fill it all with Elastic word\) AND for passphrase. Remember to set here some strong password \(min 32 random chars, best use password generator\), paste here and keep it safe. You’ll need that password in a minute.  
Launch mc and go to your Elastic-XEL-Litewallet/conf directory. When you’re in conf directory minimize MC \(Ctrl + O\) Type

{% code-tabs %}
{% code-tabs-item title="\#run" %}
```bash
touch nxt.properties
```
{% endcode-tabs-item %}
{% endcode-tabs %}

This will be the file where you customize any default properties elastic has. If you want to see all of that properties there are in nxt-default.properties file. You can go to this directory with mc, mark that file and hit F4 to see it contents \(you’ll be asked here to choose default editor, nano is quite easy\). When you stop reading and want to exit nano hit Ctrl + X \(and hit N to not save any changes\). **Remember, you can’t change content of nxt-default.properties** because everything you’ll change there will be overwritten next time you’ll update your elastic. Thats why we created a new file in conf directory.  
So, go back to conf/nxt.properties, highlight that file in MC, and edit it \(F4\). You’ll see an empty file. Paste the following lines there:

{% code-tabs %}
{% code-tabs-item title="\#nxt.properties" %}
```javascript
# Hosts from which to allow http/json API requests, if enabled. Set to * to

# allow all. Can also specify networks in CIDR notation, e.g. 192.168.1.0/24.

nxt.allowedBotHosts=*

# Host interface on which to listen for http/json API request, default localhost

# only. Set to 0.0.0.0 to allow the API server to accept requests from all

# network interfaces, including IPv6.

nxt.apiServerHost=0.0.0.0

# Password that should be provided when executing protected (administrative) API

# requests.

# Please choose a decent password here. Preferably, use a password generator.

# Password protection is disabled and password is not needed when the API server

# only listens on the localhost interface, i.e. when 

# nxt.apiServerHost=127.0.0.1.

nxt.adminPassword=generateSomeAdminAPIPasswordAndPasteHere

# Enable SSL for the API server (also need to set nxt.keyStorePath and

# nxt.keyStorePassword).

# Non-SSL connections will be disabled if nxt.apiServerSSLPort is equal to

# nxt.apiServerPort.

# Otherwise, both SSL and non-SSL connections will be accepted.

nxt.apiSSL=true

# keystore file and password, required if uiSSL or apiSSL are enabled.

nxt.keyStorePath=keystore

nxt.keyStorePassword=passwordYouProvidedDuringSSLCertGeneration
```
{% endcode-tabs-item %}
{% endcode-tabs %}

As you can see, adminPassword is “generateSomeAdminAPIPasswordAndPasteHere”. Again, generate yet another password here. You don’t need to save this password anywhere because you don’t need it. It just has to be set when you are opening your node to the world.

keyStorePassword is “passwordYouProvidedDuringSSLCertGeneration”. Replace it with password you generated during the SSL step.

Save your changes by hitting Ctrl + X \(you’ll be asked if you want to save, hit Y or if you have Ubuntu installed in different language, it might be a key corresponding to “Yes” word in your language\) and you should be back in MC. Exit from mc \(F10\):

## Running the node

{% code-tabs %}
{% code-tabs-item title="\#run" %}
```bash
cd /home/elastic/elastic/Litewallet-Mainnet
```
{% endcode-tabs-item %}
{% endcode-tabs %}

{% code-tabs %}
{% code-tabs-item title="\#run" %}
```bash
screen ./run.sh
```
{% endcode-tabs-item %}
{% endcode-tabs %}

{% hint style="info" %}
If you want to go back from screen to your server console **LEAVING Elastic running in background** hit Ctrl \(hold it\), now hit A key **and release it** and hit D key. 
{% endhint %}

To access ur wallet open ur browser and go to

{% code-tabs %}
{% code-tabs-item title="\#access" %}
```http
https://your_server_ip_address_or_hostname:17876
```
{% endcode-tabs-item %}
{% endcode-tabs %}

{% page-ref page="../xeline\_wallet/" %}

>

