# Ruby on Rails + Ubuntu + Apache with Passenger
> Author: jxuao

### 1.  Make sure you have Ruby and all its development necessities
        sudo apt-get install ruby-full build-essential

### 2.  Then install Rubygems
        cd ~/Download
        wget http://production.cf/rubygems.org/rubygems/rubygems/rubygems-2.4.6.tgz
        tar xvzf rubygems-2.4.6.tgz
        cd rubygems-2.4.6
        sudo ruby setup.rb
        sudo gem update --system

### 3.  Next you need to install Apache (if you do not already have it installed)
        sudo apt-get install apache2 apache2-mpm-prefork apache2-prefork-dev

### 5.  Now you can use gem to install Rails
        sudo gem install rails

### 6.  Install [Phusion Passenger][passenger](an Apache module that lets you run Rails apps easily)
        sudo gem install passenger
        sudo passenger-install-apache2-module
            
> The **<font color='red'>passenger-install-apache2-module</font>** script will guid you though what you need to do to get Passenger working.<font color='red'>**It should tell you copy these lines, example as below, into your** /etc/apache2/apache2.conf</font>

        LoadModule passenger_module /usr/lib/ruby/gems/1.9.1/gems/passenger-4.0.59/buildout/apache2/mod_passenger.so
        <IfModule mod_passenger.c>
            PassengerRoot /usr/lib/ruby/gems/1.9.1/gems/passenger-4.0.59
            PassengerDefaultRuby /usr/bin/ruby1.9.1
        <IfModule> 

### 7.  Enable mod_rewrite for Apache:
        sudo service apache2 restart
        sudo a2enmod rewrite

### 8.  Config the wherami.com. Copy the wherami.com/ folder to /var/www/html.
        cd /etc/apache2/sites-available/
        touch wherami.com.conf
        vim wherami.com.conf

> ##### Insert this to <I><font color='red'>wherami.con.conf</font></I>
        <VirtualHost *:80>
            ServerName wherami.com
            # !!! Be sure to point DocumentRoot to 'public'!
            DocumentRoot /somewhere/public
            <Directory /somewhere/public>
                # This relaxes Apache security settings.
                AllowOverride all
                # MultiViews must be turned off.
                Options -MultiViews
                # Uncomment this if you're on Apache >= 2.4:
                #Require all granted
             </Directory>
        </VirtualHost>

### 9.  Enable the site, wherami.com, and restart Apache
        sudo a2ensite wherami.com
        sudo service apache2 restart
        or
        sudo /etc/init.d/apache2 restart





[passenger]: https://www.phusionpassenger.com/ "Thusion Passenger" 
