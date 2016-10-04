# WordPress Workshop Walkthrough

## WordPress Development using Vagrant

1. Install Vagrant from [Vagrant](https://www.vagrantup.com/) and [VirtualBox](https://www.virtualbox.org/) for both Mac and Windows user.
1. Download `vagrant-wordpress.box` from [https://www.dropbox.com/s/398ilwuw95kmddm/Wordpress-Workshop.zip?dl=0](https://www.dropbox.com/s/398ilwuw95kmddm/Wordpress-Workshop.zip?dl=0) to your local folder, for example, inside `phpwomen` folder. Thanks Vanessa for provisioning it. You can learn more about Vagrant from her talk [here](https://engineers.sg/video/taming-your-dev-environment-with-vagrant-singapore-php-user-group--1130).
1. Open Terminal `cd /path/to/phpwomen`
1. Run `vagrant box add vagrant-wordpress vagrant-wordpress.box`
1. `mkdir vagrant-wordpress`
1. `cd vagrant-wordpress`
1. `vagrant init vagrant-wordpress`
1. `vi /etc/hosts` and add this line: `192.168.33.44	wordpress.local.com`
1. Type `vagrant up`


Notes for Windows user:

2. After downloading the `vagrant-wordpress.box`, use Windows Command Prompt to run the Vagrant command line
3. Download Putty from [http://www.putty.org/](http://www.putty.org/)
3. Your hosts file might be located at `C:\Windows\System32\Drivers\etc\hosts`. Open as Administrator, add this line: `192.168.33.44	wordpress.local.com` and save it.

### Other useful commands for Vagrant

- To access the machine, run `vagrant ssh`
- To see the status of your vagrant box, run `vagrant global-status`. You should see something like this. *daab7d5* is your vagrant id number.

```
daab7d5  default virtualbox running  /path/to/phpwomen/Wordpress-Workshop/vagrant-wordpress
```

- To power off the vagrant box, run `vagrant halt daab7d5` (`vagrant halt vagrant-id`)
- To delete the vagrant box, run `vagrant destroy daab7d5` (`vagrant destroy vagrant-id`)

## WordPress Info

When Vagrant is up and running, you should be able to go to the installed WordPress using browser and point it to url [http://wordpress.local.com](http://wordpress.local.com).

If you can't, try [http://192.158.33.44](http://192.158.33.44)

### WP Admin

URL: [http://wordpress.local.com/wp-admin](http://wordpress.local.com/wp-admin)

Username: `wp-user-workshop`

Password: `password123`

## Theme

North by SiteOrigin. Download from [https://siteorigin.com/theme/north/](https://siteorigin.com/theme/north/). 


## Plugins

- PageBuilder by SiteOrigin. [Download link](https://siteorigin.com/page-builder/)
- SiteOrigin Widgets Bundle. [Download link](https://wordpress.org/plugins/so-widgets-bundle/)

## Images

Download image set that we will use for today from [here](https://dl.dropboxusercontent.com/u/28350025/WP%20Workshop%20Images.zip).

## Other Links

- Coffee Ipsum [link](http://coffeeipsum.com/). Helps you generate dummy text.

## WP Database

Just in case you want to peek at the database...

Database URL: [http://192.168.33.44:8888](http://192.168.33.44:8888)

Username: `root`

Password: `password123`

## Additional Info

### Vagrant SSH access

```
Username: vagrant
Password: vagrant
```

### SMTP Email

```
-- Gmail --
Username: wpuserworkshop@gmail.com
Password: password#123

```

### 
 

# WordPress Workshop Info Part 2

## Plugins

- WooCommerce. Search and install from WP Dashboard.

## Products

- Take image for each product from the image set


# Helper Links

- Coffee Ipsum [link](http://coffeeipsum.com/)
- SiteOrigin Page Builder Plugin [link](https://siteorigin.com/page-builder/)
- SiteOrigin North Theme [link](https://siteorigin.com/theme/north/)
- SiteOrigin North Theme documentation [link](https://siteorigin.com/north-documentation/)
- WooCommerce plugin page [link](https://wordpress.org/plugins/woocommerce/)
- WooCommerce Shortcode [link](https://docs.woocommerce.com/document/woocommerce-shortcodes/)

# Troubleshooting

## 413 (Request Entity Too Large)

If you experience this error, do these steps.

1. First, `vagrant ssh` from Terminal. 
1. Edit configuration by typing `sudo nano /etc/nginx/sites-available/wordpress`. You will see an editor.
1. Add this line `client_max_body_size 5M;` within the `server` curly braces. Exit by pressing `Control+X` and yes to save it.
1. Edit `php.ini` configuration by typing `sudo nano /etc/php5/fpm/php.ini`. In the editor, press `Control+W` to search for text "upload" and then press enter. Around there, you should see a line that contains `upload_max_filesize`. We need to increase it from the current 2M to let's say 10M. Exit and save it.
1. Lastly, type `sudo service nginx restart` to restart Nginx service.


Your `/etc/nginx/sites-available/wordpress` should now look like this:

```
server {
        #listen   80; ## listen for ipv4; this line is default and implied
        #listen   [::]:80 default ipv6only=on; ## listen for ipv6
        listen                192.168.33.44:80;
        server_name           wordpress.local.com;
        client_max_body_size 5M;
        
        ...
}
```
