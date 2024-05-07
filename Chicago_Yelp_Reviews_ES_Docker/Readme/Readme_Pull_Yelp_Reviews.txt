HOW TO PULL ELASTICSEARCH DOCKER IMAGE*********************************************

Requirements -> Python 3.11 and elasticsearch 8.12.0Step_1: You must download docker desktop and create an docker account.
	
       Step_1.1: Run the docker desktop
Step_2: Go inside the YelpData_pull folder and follow the below steps to pull the elasticsearch image that you pushed to docker hub.

	Step_2.1: Open docker-compose.yml and update the docker image name as shown below:

                  YOUR-DOCKERHUB-USERNAME/[REPOSITORY[:TAG]] (This will be the image that you pushed to docker hub).
	
	          For example : prakharnag98/elasticsearch_8.12:multi	Step_2.2: To pull the image you created during push, open the terminal/cmd and run following command:

	          docker-compose up 

	          This will pull your image from Docker hub and will run the container for it.                  "docker-compose up" uses docker-compose.yml file that contains all the information about the image, such as services, port, volumes, etc.


Step_3: Run the pullYelpData.ipynb script to fetch the data, if data is visible, then all steps were a success.

If you are face any issues in Step 2, alternatively, you can also do :1. docker pull YOUR-DOCKERHUB-USERNAME/[REPOSITORY[:TAG]]  

   For example - docker pull prakharnag98/elasticsearch_8.12:multi
2. docker-compose up (you need to be in your YelpData_pull folder)3. Verify that elasticsearch is running and the data can be fetched

   a. Go to your browser and type localhost:9200 and press Enter.      If you see a JSON response, this means it is running fine.

4. Run the pullYelpData.ipynb script to fetch the data, if data is visible, then all steps were a success.

   Docker image and the running container can also been checked on Docker desktop.