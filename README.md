# doocker-wp
Wp in docker

docker-compose.yml

To start with setup the directory in which we’ll build our WordPress theme. Create a new folder wherever you want and name it whatever you want. I named mine docker-wordpress-theme-setup to match the GitHub repository. We’ll set up our entire WordPress ecosystem in this directory.

Open your code editor, create a blank file named docker-compose.yml and save it in the directory you created above. This is the file Docker will use to set up WordPress and the MySQL database.

Open Terminal & navigate to the directory above.  Once there, type ls and you should see your docker-compose.yml file; copy the code from the template here & make changes to the port & name if you are running multiple docker wordpress instances.

If you want to change the port that the WordPress install will use, just change the 8000 value in ports to whatever value you would like. If you want it to run on port 9210 you would make the change like so:

ports:
  - "9210:80"

Then instead of localhost:8000, the URL would be: localhost:9210

The first volumes parameter under wordpress is what tells Docker to surface the wp-content directory and the resulting WordPress directories in the local file system. 

You don’t have to change anything here, it’s a local path that is keyed off the directory the config.yml file is in. The wp-content directory along with the themes and plugins directories will be created automatically when we run the Docker command to install everything. This is nice because anything created by WordPress (e.g. adding a plugin through the admin) or you (uploading an image) will show up in these directories just like they would on a server.

finally copy the uploads.ini file into the folder so it can take uploads