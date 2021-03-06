* Install [odoo](http://www.odoo.com/documentation/10.0/setup/install.html)
  * set locale before doing anything (```export LC_ALL="en_US.UTF-8"```)
  * ```sudo wget -O - https://nightly.odoo.com/odoo.key | apt-key add -```
  * ```sudo echo "deb http://nightly.odoo.com/10.0/nightly/deb/ ./" >> /etc/apt/sources.list.d/odoo.list```
    * if last command didn't work do it manually using vim
  * ```sudo apt-get update```
  * ```sudo apt-get install odoo```
  * ```sudo apt-get install wkhtmltopdf```
  * ```sudo apt-get remove wkhtmltopdf``` to get dependancies 
  * do this to get wkhtmltopdf to work [link](https://github.com/odoo/odoo/wiki/Wkhtmltopdf)
   * user ```sudo dpkg -i file.deb``` 
  * ```sudo service odoo start```


* to get odoo running on port 80 reroute 80 to 8069
  * edit ```/etc/rc.local``` include ```iptables -t nat -A PREROUTING -p tcp --dport 80 -j REDIRECT --to-port 8069``` then reboot
* to check logs ``` sudo more /var/log/odoo/odoo-server.log```

My options in /etc/odoo/odoo.conf
use deafult settings these are unstable
```
[options]
; This is the password that allows database operations:
; admin_passwd = admin
db_host = False
db_port = False
db_user = odoo
db_password = False
addons_path = /usr/lib/python2.7/dist-packages/odoo/addons
workers = 3
limit_memory_hard = 943718400
limit_memory_soft = 838860800
```

workers = (#CPU * 2) + 1
Needed RAM = #worker * ( (light_worker_ratio * light_worker_ram_estimation) + (heavy_worker_ratio * heavy_worker_ram_estimation) )
i put 800 MB and 900MB we have 1 GB ram

* to run postgres commands switch user ```sudo su - postgres```

optional stuff
* Odoo [server config](https://www.linode.com/docs/websites/cms/install-odoo-9-erp-on-ubuntu-14-04)
* odoo [optimizing](https://www.odoo.com/documentation/10.0/setup/deploy.html)
* another optimizing [link](https://www.rosehosting.com/blog/how-to-speed-up-odoo/)
* to find config file run ```ps ax| grep odoo```
  * add this to change port 
    * backup odoo config file
* restart odoo after that

* setup database backup
  * manually backup use zip always other (dump) doesn't work


  
  
