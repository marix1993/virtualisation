Monolith deployment
-

### Provision VM to have app folder and nginx on start up:
1. First we need to make a script which will allow Nginx to run on start up:

![script_2.png](files%2Fscript_2.png)

2. In our "Vagrantfile" we need to add provision:

![provision.png](files%2Fprovision.png)

3. Next we need to sync app folders. (download necessary folders and
extract them info our "Virtualisation"). If everything is right
they should appear on our VS code app.

![files_added.png](files%2Ffiles_added.png)

4. Next wee need to sync the app folder. To do that we need
to add new command in our VS Code

![syncing.png](files%2Fsyncing.png)

5. To check if everything works:
- first in VS code terminal use `vagrant up`
- next we need to use `vagrant ssh` in GitBash (make sure that you're in virtualisation file).

![vagrant_ssh.png](files%2Fvagrant_ssh.png)

- now we can check if our app folder is synced by using `ls` command.

6. Next step in VS code terminal we need to navigate to environment folder 
`cd environment` and next `cd spec-tests`
7. To run tests we need to install bundle. Type in `gem install bundle`.

![gem_installed.png](files%2Fgem_installed.png)

8. Next we can use command `bundle` to bundle up all the tests.
9. Next command is `rake spec` to run all the tests.

![rake_spec.png](files%2Frake_spec.png)

10. After checking all the test few of them are failed. To fix it we need to
install all the missing packages: nodejs/pm2.
11. To do that in GitBash we need to navigate to our main Vagrantfile by using `cd`.
12. Next we need to install NodeJS by using `sudo apt-get install nodejs -y`.
13. Next we need to install python software properties by using `sudo apt-get install python-software-properties -y`.
14. Next we need to install specific version that we want to install `curl -sL https://deb.nodesource.com/setup_6.x | sudo -E bash –`
to make sure that it's nodejs version 6.x.
15. Next command is again `sudo apt-get install nodejs -y` and to check everythin  `nodejs --version`.
16. The last Package that we need to install is "pm2" (package manager for Node - we need it to actualy unpackage the app).
To do that run `sudo npm install pm2 -g`.
17. In VS Code terminal we can run `rake spec` and it will show if all the tests passed.

![tests_passed.png](files%2Ftests_passed.png)

18. Next we need to go back to GitBash, go into app folder by using `cd app`.
19. One of the last steps is to install the app by using `npm install`.
20. Next use `node app.js` and if everything works fine this should pop up:

![port_3000.png](files%2Fport_3000.png)

21. To check if everything works in web browser paste the IP `http://192.168.10.100` plus add `:3000`.

### Welcome to Sparta App

![welcome.png](files%2Fwelcome.png)


How to provision Sparta App in steps?
-

1. To do that in `script.sh` file we need to add few lines:
* `sudo apt-get install python-software-properties -y` to install dependencies.
* `curl -sL https://deb.nodesource.com/setup_6.x | sudo -E bash -` it "grabs" exact distribution of software -in this case NodeJS version 6.x that we want.
* `sudo apt-get install nodejs -y` to use that version that we just "grabbed" and put it into effect.
* `sudo npm install pm2 -g` to install pm2.

* `cd app` to navigate to app folder where we want to install npm.

* `npm install` it use pm2 dependency to install npm.
* `node app.js` to run the application.

![new_provision.png](files%2Fnew_provision.png)

2. Next in VS Code terminal use `vagrant up` command and after a while we can check if
our "Sparta app" works again.

![works_again.png](files%2Fworks_again.png)

How to provision MongoDB in steps?
-

1. First we need to create our `scriptdb.sh` (we can leave the same name as previous shell script file
but it's better to put it somewhere else and include the `path` in our code).

![patch_changed.png](files%2Fpatch_changed.png)

Now in our `scriptdb.sh` file:

* `sudo apt update -y` - update the sources list.
* `sudo apt upgrade -y` - upgrade any packages available.


* `sudo apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv D68FA50FEA312927` - import the MongoDB public key.


* `echo "deb https://repo.mongodb.org/apt/ubuntu xenial/mongodb-org/3.2 multiverse" | sudo tee /etc/apt/sources.list.d/mongodb-org-3.2.list` - 
generate a file with the MongoDB repository url, verifies that key.


We need to grab update and upgrade - now it knows about MongoDB so we need to redo it – it has to add new packages
* `sudo apt update -y`
* `sudo apt upgrade -y`


* `sudo apt-get install -y mongodb-org=3.2.20 mongodb-org-server=3.2.20 mongodb-org-shell=3.2.20 mongodb-org-mongos=3.2.20 mongodb-org-tools=3.2.20` - 
to install MongoDB on our Virtual Machine.


* `sudo systemctl start mongod` - to install downloaded app.

2. To check if everything works in VS Code terminal use: `vagrant up db`.
3. In GitBash terminal (in our virtualisation folder) use: `vagrant ssh db`.
4. And use command `sudo systemctl status mongod`.


![mongo_check.png](files%2Fmongo_check.png)

How to connect our "App" with "Database" using `environmental variable`?
-

1. First we need to make sure that our "App" provision shell script 
won't allow NodeJS app to run in the background. (That's how
provision for app should look like).

![provision_app.png](files%2Ffiles_db_app_connection%2Fprovision_app.png)

2. Next we need to set up our VMs, so in VS Code terminal use: `vagrant up`.
3. Next in two Gitbash terminals use `vagrant ssh app` % `vagrant ssh db`.

![ssh_app_db.png](files%2Ffiles_db_app_connection%2Fssh_app_db.png)

4. Next we need to change few settings with our MongoDB:
- `sudo nano /etc/mongod.conf` , scroll down and change `bindIP:` to 0.0.0.0 (we are changing it so
anyone can access it, make sure not to do it on production)

![db_change.png](files%2Ffiles_db_app_connection%2Fdb_change.png)

- `ctrl + s` to save and `ctrl + x` to exit
- `sudo systemctl restart mongod` - to restart our MongoDB
- `sudo systemctl enable mongod` - to apply our changes and start MongoDB
- `sudo systemctl status mongod` - to check if it works

5. Next we need to make few changes in our App (we need to connect App with DB by using environmental variable):
- `sudo nano .bashrc` - to make connect our env variable and make it persistent

![bashrc_change.png](files%2Ffiles_db_app_connection%2Fbashrc_change.png)

- at the end of the file add : `export DB_HOST=mongodb://192.168.10.150:27017/posts`
  (we need to check if there is variable called DB_HOST and if it is make sure that is
connected to the right IP of our MongoDB - 150 and port - 27017)
- `ctrl + s` to save, `ctrl + x` to exit
- `source .bashrc` - to run bashrc file and apply changes
- `printenv DB_HOST` - to check if our variable is present and persistent
- `cd app` - to enter our app directory
- `npm install` - to install our app
- now we should look for those two informations:

![db_cleared.png](files%2Ffiles_db_app_connection%2Fdb_cleared.png)

- `node seeds/seed.js` - to seed database
- `node app.js` - to run the app

If everything went fine we should receive that message in Gitbash:

![working1.png](files%2Ffiles_db_app_connection%2Fworking1.png)

and after typing in `http://192.168.10.100:3000/posts` into our browser this should appear:

![working2.png](files%2Ffiles_db_app_connection%2Fworking2.png)

How to provision step 4?
-

In step 4 previously we had to use command: `vagrant ssh db` and then add few extra commands manually.
To automate this process we can refactor our `scriptdb.sh` provision script.

First we need to apply some changes to `mongod.conf` file. This a command to automate it:

* `sudo sed -i 's/^\(\s*bindIp:\).*/\1 0.0.0.0/' /etc/mongod.conf`

`sed`: This command is a stream editor that is used to modify text files. 

`-i`: This option tells sed to modify the file in place

`s/^\(\s*bindIp:\).*/\1 0.0.0.0/` this is the regular expression pattern that sed uses to find and replace text in the file. 
It is surrounded by single quotes to prevent the shell from interpreting special characters and also make sure that the indent is correct.

Then we need to add :

* `sudo systemctl restart mongod` - to restart MongoDB
* `sudo systemctl enable mongod` - to start MongoDB and make sure that change is accepted.

The script should look like this:

![step_4.png](files%2Ffiles_db_app_connection%2Fstep_4.png)

How to provision step 5?
-

In step 5 we had to make changes into `.bashrc` file manually.
To automate it we can use this commands:

* `echo 'export DB_HOST=mongodb://192.168.10.150:27017/posts' | sudo tee -a /etc/environment`

`echo`: this command outputs a string to the console. In this case, we are using it to output the string export DB_HOST=mongodb://192.168.10.150:27017/posts.

`export`: this keyword is used to create or modify environment variables in the current shell session.

`DB_HOST`: this is the name of the environment variable we are creating.

`mongodb://192.168.10.150:27017/posts`: this is the value of the `DB_HOST variable`. It is a connection string for a MongoDB server running at IP address 
`192.168.10.150` and listening on `port 27017`, with a database name of `posts`.

`|`: this is a pipe symbol, which is used to redirect the output of one command to another command as input.

`tee`: This command is used to read from standard input and write to standard output and/or files. In this case, we are using it to append the output of the echo command to the system-wide environment file /etc/environment.

and after that in our script we can add:

* `source .bashrc` - we need to run that file again to make changes
* `cd app` - change to app directory
* `npm install` 
* `node seeds/seed.js` - this command is used to execute the code in the seed.js file using the Node.js runtime. 
* `node app.js` - install app.js

The `script.sh` file should look like this:

![step_5.png](files%2Ffiles_db_app_connection%2Fstep_5.png)

How to provision both steps?
-