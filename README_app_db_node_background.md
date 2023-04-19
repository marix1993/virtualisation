How to use pm2 to run the node app as a background process and provision the whole process?
-

To run a process in the background in Linux, you can append the & character at the end of the command. For example:

`node app.js &` - this will run the app.js script in the background.

However, this is not a recommended way to run a 
Node.js app in the background as the process can 
terminate when you exit the terminal. To ensure 
that the process continues to run in the background, 
you can use a process manager like pm2 by using `pm2 start app.js` command.

To set up both VMs at once we need to make sure that our
installation of NodeJS `app.js` is run as a background process. 
Otherwise we we get locked out of the terminal so below is a way how to fix it.

1. First we need to change our provision shell file. The commands that we need to change are:

`curl -sL https://deb.nodesource.com/setup_6.x | sudo -E bash -`

and we need to change it to:

`curl -sL https://deb.nodesource.com/setup_16.x | sudo -E bash -`


This way we are making sure that our new version of NodeJS support `pm2 start app.js` command
and that we wont have to use `node app.js &` because it might terminate the process if we exit the terminal.

Next command that we need to change is:

`node app.js`

to:

`pm2 start app.js` - to make sure that the process is run in the background.

I also added `cd` at the end of the script to make sure that the whole
process will get back to main folder (I'm not sure if its required).

![changed_script.png](files%2Fchanged_script.png)

I commented the previous commands just to point out changes.

2. Now if everything works properly in our VS Code terminal we can type `vagrant up`.
and after a while we can:
- check our browser with IP provided to see if our app works
- in GitBash use `vagrant ssh app` to login into our app
- in second GitBash terminal use `vagrant ssh db` to login into MongoDB.

![everything_works.png](files%2Feverything_works.png)

Everything works!
-