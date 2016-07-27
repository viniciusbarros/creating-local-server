# Creating local environment
Tutorial to help you cloning a project and setup it in a local environment

### Requisites
* To have your a SHH key previously generated on your machine and uploaded to your git server (i.e GitHub);
* Know the project *.git* url to clone.

## Step 1 - Cloning the project to your machine

Lets use this project URL as an example:

    git@github.com:viniciusbarros/learning-web.git

Here I am navigating to my Webserver folder where I want to place my project:

	cd /Users/Vinicius/WebServer/

After knowing where you want the project to be placed, lets run the *git clone* command:


	git clone git@github.com:viniciusbarros/learning-web.git {OPTIONAL FOLDER NAME}

If you specify and *OPTIONAL FOLDER NAME* right after the *git clone* command, the code will be downloaded into that specific folder. Otherwise it will create a folder with the name of the project, in this case "learning-web".

## Step 2 - Creating a local visible URL

In order to do that you will have to edit the **hosts** file on your machine.
On a Apple computer, it should be in:

	/etc/hosts

On a Windows machine:

	C:\Windows\System32\drivers\etc\hosts

Edit the file by adding the following piece of text:

	127.0.0.1 my-project-url.local

It is completely optional to have the *.local* at the end, but I prefer to have it so I can easily identify that it is a local server.

**Tip:** To check if it is working, try pinging the recente created url:

	ping my-project-url.local

## Step 3 - Pointing the local URL to the project folder

Now you just need to run the final step that is pointing the url you have just created to the project folder.

Now you need to find where is your Virtual Hosts file (according to your local server). In my case, I use XAMPP, so my file sits in:

	/Applications/XAMPP/etc/extra/httpd-vhosts.conf

Add the following content:

```bash
<VirtualHost *:80>
    DocumentRoot "/Users/Vinicius/WebServer/learning-web"
  <Directory "/Users/Vinicius/WebServer/learning-web">
	  Options Indexes FollowSymLinks Includes execCGI
	  AllowOverride All
	  Require all granted
  </Directory>
	ServerName my-project-url.local
	ServerAlias *.my-project-url.local
	RewriteEngine On
</VirtualHost>
 ```

## Step 4 - Restart and Run!
Restart your apache and try accesing the url http://my-project-url.local.

**Note:** Sometimes you need to add the **http://** in the url in order to reach your local server.
