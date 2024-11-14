https://docs.aws.amazon.com/prescriptive-guidance/latest/patterns/deploy-lambda-functions-with-container-images.html

https://docs.aws.amazon.com/AmazonECR/latest/userguide/docker-push-ecr-image.html#:~:text=To%20push%20a%20Docker%20image%20to%20an%20Amazon%20ECR%20repository&text=Authentication%20tokens%20must%20be%20obtained,get%2Dlogin%2Dpassword%20command.

https://medium.com/@sayalishewale12/complete-guide-to-creating-and-pushing-docker-images-to-amazon-ecr-70b67ac1ab4c

https://www.freecodecamp.org/news/build-and-push-docker-images-to-aws-ecr/

https://www.youtube.com/watch?v=wDmFRXcOglw&ab_channel=Valuebound

https://stackoverflow.com/questions/43121621/how-can-i-test-lambda-in-local-using-python

https://plainenglish.io/blog/aws-lambda-or-aws-batch-making-the-right-choice-for-your-workload

AWS Lambda functions can be configured to run up to 15 minutes per execution.

AWS Batch doesn’t have default timeout limit, if job timeout is not specified, the job runs until the container exits.

Timeout duration can be specified for AWS Batch jobs so that if a job runs longer than that, it will be automatically terminated by AWS Batch.

So, AWS Lambda is preferred for short running tasks while AWS Batch is preferred for long running computaion heavy tasks.


##

docker build -t IMAGE .  ##

docker build -f docker_buildtest/Dockerfile --force-rm -t testimage .

---
Notes

docker run -p 9000:8080 newimage    ##

## -p flag allows it to display to the outside world from the container

curl -XPOST "http://localhost:9000/2015-03-31/functions/function/invocations" -d '{}'   ## inside {} is where you put the context, body

example : curl -X POST "http://localhost:9000/2015-03-31/functions/function/invocations" -d '{"body": "{\"image_url\": \"https://www.python.org/static/community_logos/python-logo-master-v3-TM.png\"}"}'


---------------------------------------
# common docker commands


A container is a runnable instance of an image. which is why you cannot delete an image if there is a running container from that image. You just need to delete the container first.

docker ps -a                # Lists containers (and tells you which images they are spun from)

docker images               # Lists images 

docker rm <container_id>    # Removes a stopped container

docker rm -f <container_id> # Forces the removal of a running container (uses SIGKILL)

docker rmi <image_id>       # Removes an image 
                            # Will fail if there is a running instance of that image i.e. container

docker rmi -f <image_id>    # Forces removal of image even if it is referenced in multiple repositories, 
                            # i.e. same image id given multiple names/tags 
                            # Will still fail if there is a docker container referencing image

docker system prune  # MUST RUN AFTER DELETE OR LOSE UNCLAIMED MEMORY SPACE

Everytime we call RUN, it builds a new layer.

## free up memory
docker system prune  # ~20Gb free up  
However, this is not always updated. To ensure it works, use the clean up function in the top right of the Docker Desktop GUI.

### retagging images (Docker only has unique IDs, but can have various nametags)
docker tag myapp:latest myapp-renamed:latest
docker rmi <old-image-name>:<old-tag>

-no-cache  flag keeps the docker image small.

## Example Dockerfile
# Use an official Python runtime as a base image
FROM python:3.12-slim

# Set the working directory in the container
WORKDIR /app

# Copy the script to the container
COPY . .

RUN pip install --no-cache-dir -r requirements.txt

WORKDIR /app/scripts

# Set the entrypoint for the container
ENTRYPOINT ["python", "scripts/run_awsbatch.py"]

NOTE: In Docker, the directories might not behave similarly to your original locally run repo.

i.e. instead of `from core import *`, you might have to do `from scripts.core import *`.

Also, reminder to import the **parent** directory instead of the actual module folder.

  
