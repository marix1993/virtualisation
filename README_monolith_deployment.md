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