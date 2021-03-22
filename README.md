# docker-wp
Wordpress hosting in docker

To start with setup the directory in which we’ll build our WordPress theme. Create a new folder wherever you want, the name of the folder will the name of the docekr containers this script create. We’ll set up our entire WordPress ecosystem in this directory, so name sure the name is unique if working with multiple wordpress containers.

## To create a directory
~ mkdir [name of site]

Open your code editor, create a blank file named docker-compose.yml and save it in the directory you created above. This is the file Docker will use to set up WordPress and the MySQL database.

Open Terminal & navigate to the directory above.  Once there, type ls and you should see your docker-compose.yml file; copy the code from the template here & make changes to the port & name if you are running multiple docker wordpress instances.

## To create a file
~ touch [name of file].[extention of file if required]

If you want to change the port that the WordPress install will use, just change the 8000 value in ports to whatever value you would like. If you want it to run on port 9210 you would make the change like so:

ports:
  - "9210:80"

Then instead of localhost:8000, the URL would be: localhost:9210

The first volumes parameter under wordpress is what tells Docker to surface the wp-content directory and the resulting WordPress directories in the local file system. 

You don’t have to change anything here, it’s a local path that is keyed off the directory the config.yml file is in. The wp-content directory along with the themes and plugins directories will be created automatically when we run the Docker command to install everything. This is nice because anything created by WordPress (e.g. adding a plugin through the admin) or you (uploading an image) will show up in these directories just like they would on a server.

finally create an uploads.ini file in the folder & copy the code from the template so it can take uploads

when all this is done just run the docker compose command to kick off the build and then connect to the host; it must be run from the directory so it can see the docker-compose.yaml

# To run docker compose
~ docker-compose up -d

# To connect to the wordpress docker instance front end
http://[IP of server]:[port]/

# To connect to the wordpress docker instance back end
http://[IP of server]:[port]/wp-admin