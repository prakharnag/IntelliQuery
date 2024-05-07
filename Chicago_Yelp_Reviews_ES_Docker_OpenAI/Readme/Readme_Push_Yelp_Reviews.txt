ELASTICSEARCH - VECTOR DB
***************************


Requirements : openAI 1.7.2 and elasticsearch 8.12.0

Step_1: You must download docker desktop and create an docker account.

	Step_1.1: Run the docker desktop

	          Now, to run the elasticsearch 8.12 we will use docker image, follow step 2 for it.


Step_2: Open the terminal and navigate to YelpData_push and using the command below pull the original elasticsearch 8.12.0 image from docker hub:
	
	
        docker-compose up 


	Step_2.1: Go to your web-browser and on the url type in -> localhost:9200, you will see a json response which confirms that elasticsearch 8.12.0 has started.


Step_3: Now, you can open the Push_Yelp_Reviews.ipynb file for creating changes. 

        The data/changes can be seen inside this path of elasticsearch -> /usr/share/elasticsearch/data (This directory can be found on the running container on your docker desktop)

        Before pushing the image, you need to commit the changes


Step_4: Open the terminal and get the container ID from it by using the below command:
	
	run docker ps


Step_5: Stop the container by using the container id copied from step_4 and use the below command :
	
	docker stop containerID


Step_6: Now we need to commit our changes, follow this to create commit command :

	 docker commit CONTAINER ID [REPOSITORY[:TAG]]

	 For example : docker commit 6c31284597e6 prakharnag98/elasticsearch_vector:latest

	 This commits all the new changes and will create a new image.


Step_7: Push the Image to the Docker hub using the below command.

	docker push YOUR-DOCKER-USERNAME/[REPOSITORY[:TAG]]

	For ex: docker push prakharnag98/elasticsearch_vector:latest


Step_8: Now, lets build a multi-platform image and push it on docker hub

	      Note: The build command requires a Dockerfile otherwise it will produce an error. This docker file contains the information about the image we need to build from before pushing.
            
              You will have to modify the content of Dockerfile based on the image name you gave during commit. 

		    
	Step_8.1:     Open the given Dockerfile in text editor and make changes accordingly as shown below and save it. 

	     	      FROM [REPOSITORY[:TAG]]

		      For example : FROM prakharnag98/elasticsearch_vector:latest

                      Note: Please make sure you are in the directory where the Dockerfile is present.

                      Multi-platform build is not supported for the docker driver.Therefore, we need to switch to a different driver.


	Step_8.2:     Use the below command to create a new driver 

	
                      docker buildx create --use  

	
	              and then execute the below command to build a multi-platform image.


	Step_8.3:     docker buildx build --platform linux/amd64,linux/arm64,linux/arm/v7 -t <username>/<image>:multi --push .

		      For example: docker buildx build --platform linux/amd64,linux/arm64 -t prakharnag98/elasticsearch_vector:multi --push .

	              This will push the Multi-platform docker image to the docker hub with the tag "multi".

