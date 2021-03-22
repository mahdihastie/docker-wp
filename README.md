# doocker-wp
Wp in docker

docker-compose.yml
For the rest of the tutorial I’m assuming you have some familiarity with Terminal and have a favorite code editor. However, I’ll still call out the Terminal commands explicitly to do my best to make sure no one gets lost along the way.
Open your code editor, create a blank file named docker-compose.yml and save it in the directory you created in Section 3. This is the file Docker will use to set up WordPress and the MySQL database.
Open Terminal. When you start Terminal the blank screen will likely be in your home directory. Just in case type the command below and hit ‘return’:
BASH
cd ~
The cd command means “change directory” and the tilde is a shortcut to the home directory. So now you’re located in your home directory. Next we need to navigate to the directory we created in Section 3. For me, I type:
BASH
cd docker-wordpress-theme-setup
Once there, type ls and you should see your docker-compose.yml file.
Now let’s add some instructions to create our WordPress setup. In your code editor, paste the following in the docker-compose.yml file and save it.
YAML
version: '3'
services:
  db:
    image: mysql:5.7
    volumes:
      - db_data:/var/lib/mysql
    restart: always
    environment:
      MYSQL_ROOT_PASSWORD: somewordpress
      MYSQL_DATABASE: wordpress
      MYSQL_USER: wordpress
      MYSQL_PASSWORD: wordpress
  wordpress:
    depends_on:
      - db
    image: wordpress:5.1.1-php7.3-apache
    ports:
      - "8000:80"
    restart: always
    environment:
      WORDPRESS_DB_HOST: db:3306
      WORDPRESS_DB_USER: wordpress
      WORDPRESS_DB_PASSWORD: wordpress
    working_dir: /var/www/html
    volumes:
      - ./wp-content:/var/www/html/wp-content
      - ./uploads.ini:/usr/local/etc/php/conf.d/uploads.ini
volumes:
  db_data:

If you want to change the port that the WordPress install will use, just change the 8000 value in ports to whatever value you would like. If you want it to run on port 9210 you would make the change like so:
YAML 

ports:
  - "9210:80"

Then instead of localhost:8000, the URL would be: localhost:9210

The first volumes parameter under wordpress is what tells Docker to surface the wp-content directory and the resulting WordPress directories in the local file system. (A special thanks to this Stack Overflow answer for helping me figure this part out.)
You don’t have to change anything here, it’s a local path that is keyed off the directory the config.yml file is in. The wp-content directory along with the themes and plugins directories will be created automatically when we run the Docker command to install everything. This is nice because anything created by WordPress (e.g. adding a plugin through the admin) or you (uploading an image) will show up in these directories just like they would on a server.
