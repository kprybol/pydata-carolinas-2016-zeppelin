# pydata-carolinas-2016-zeppelin

![PyData Carolinas 2016 Logo](http://pydata.org/carolinas2016/static/images/pydata-logo-carolinas-2016.png)

Resources to accompany my PyData Carolinas 2016 talk on PySpark 2.0 and Zeppelin Notebooks

![Zeppelin Logo](http://zeppelin-project.org/assets/themes/nflabs-sb/img/zeppelin-logo.svg)

**Apache Github Mirror: [Readme File](https://github.com/apache/zeppelin/blob/master/README.md)**

**Mailing Lists: [User and Dev mailing list](http://zeppelin.apache.org/community.html)**

# Want to Follow Along?
#### If you would like to follow along during my talk, you can do so by building your own Zeppelin/PySpark instance.



- Download and install [vagrant](http://www.vagrantup.com/downloads.html "vagrant")
- Download and install [Virtual Box](https://www.virtualbox.org/ "Virtual Box")
- pip install [ansible](http://docs.ansible.com/ansible/intro_installation.html#latest-releases-via-pip "ansible")
```
	sudo easy_install pip
	sudo pip install ansible
	ansible --version
```
- Unzip the Zeppelin source contained in this repo (zeppelin-0.6.1.zip)
- **Note: It's important that you use this .zip as there is an unfixed issue within the official Apache mirrors that will cause the build to fail**
- `cd` to `~/zeppelin-0.6.1/scripts/vagrant`
- Start vagrant and build the VM (this will take about 15 minutes) by runnin `vagrant up` within the vagrant directory. 

# What's in this VM?
The virtual machine consists of:
- Ubuntu Server 14.04 LTS
- Node.js 0.12.7
- npm 2.11.3
- ruby 1.9.3 + rake, make and bundler (only required if building jekyll documentation)
- Maven 3.3.9 (change from official repo which unsuccessfully attempts to install 3.3.3)
- Git
- Unzip
- libfontconfig to avoid phatomJs missing dependency issues
- openjdk-7-jdk
- Python addons: pip, matplotlib, scipy, numpy, pandas
- R and R Packages required to run the R Interpreter and the related R tutorial notebook, including: Knitr, devtools, repr, rCharts, ggplot2, googleVis, mplot, htmltools, base64enc, data.table

# Time to Build Zeppelin
- This is going to take a while - my latest build took `Total time: 53:33 min`
- Post running `vagrant up`, git clone the zeppelin branch into this directory from your host machine
`git clone git://git.apache.org/zeppelin.git` (Safe to use the official repo here as we have already installed maven)
-  **Note: Cloning the project again may seem counter intuitive, since this script originated from the project repository.  Consider copying just the vagrant/zeppelin-dev script from the zeppelin project as a stand alone directory, then once again clone the specific branch you wish to build.**
- Run the `vagrant up` command one more time
- Run `vagrant ssh`
- Once inside the VM, `cd /vagrant/zeppelin`
- Now it's time to finally build Zeppelin along with all of the necessary components. We will be using Spark 2.0, Hadoop 2.6 with the PySpark, and SparkR interpreters.
- Run `mvn clean package -Pspark-2.0 -Ppyspark -Phadoop-2.6 -Psparkr -DskipTests` and then find something to do for about an hour.

# Run Zeppelin
- After Zeppelin, Spark, Hadoop, etc. have finished building, you can start Zeppelin by running `./bin/zeppelin-daemon.sh start` from within the VM
- You can connect to your Zeppelin instance by directing the web browser on your host machine to: `http://localhost:8080/`
- You can stop the Zeppelin instance later by running `bin/zeppelin-daemon.sh stop`

# Tweaking the VM
- If you need to use a specific IP address or host, or if you wish to disable port forwarding, you can do so from within the vagrantfile by commenting/uncommenting out the appropriate lines.
```
	#config.vm.network "forwarded_port", guest: 8080, host: 8080
	config.vm.network "private_network", ip: "192.168.51.52"
```



