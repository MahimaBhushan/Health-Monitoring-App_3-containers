# Health-Monitoring-App_3-containers

Here we are using 3 container and running them individually instead of using a docker compose.

1. mongodb : the mongodb image is directly installed from the docker-hub.

2. container to collect the data : we will only have to build the image.

3. container to display the data on dashboard : we will have to build the image.

Point to remember:

1. The containers must be run sequentially, first the mongodb should be started, then the data collection container must run, which is followed by the dashboard container.

   There must exist some seconds of delay between each container.
   

file structure:

health-app : 

---> collect1 ----> (Dockerfile) + other files

---> dashboard1 ----> (Dockerfile) + other files           

files present in collect1 folder:

1. collect_data_10.py : we are filling in random values into the Mongo database for testing purpose. Later we can use it to get data from the router with the help of pexpect.

2. Dockerfile : Docker builds images automatically by reading the instructions from a Dockerfile -- a text file that contains all commands, in order, needed to build a given image

3. requirements.txt : this file contains all the packages to be installed using pip install which will be used in the dockerfile.

files present in  dashboard1 folder:

1. assets folder : Contains all the images,stylesheets and javascript. For css and js to be included into the dashboard.

2. app.py : initialises an app object

3. index.py : conatins the main dash layout

4. callback.py : onevent functions. To change which file to be called when router added, change here

5. layouts.py : layouts of all pages

6. Dockerfile : Docker builds images automatically by reading the instructions from a Dockerfile -- a text file that contains all commands, in order, needed to build a given image

7. requirements.txt : this file contains all the packages to be installed using pip install which will be used in the dockerfile.

8. db.py : Get the data from the database to display on dashboard.


Steps: 

1. pull the mongodb docker image and run it, also name the container as mongo

   >>docker run --name mongo mongo
   
2. build the collect image and run the container linking it with the database
  
   >>docker build -t collectdata .
   
   >>docker run --link mongo:mongo collectdata
   
3. build the dashboard image and run the container linking with the database also map the ports

   >>docker build -t dashboard .
   
   >>docker run --link mongo:mongo -p 5050:5555 dashboard
   
   The dashboard can be viewed on  http://127.0.0.1:5050 on the browser. The live data is being read and updated on the dashboard.
  
   
  The advantage of docker-compose file will be avoid the above 3 steps of individually building and running the containers. 
  
  By just doing
 
  >>docker-compose up 
  
  we will be able to lauch the app.


Things to be rectified:

1. the time in the dashboard plots are 5hrs ahead.

2. on clicking the router_id multiple tabs are opening. Whereas, only one must be opened.
