# Edge-Orchestration-and-ML
This part of the github repo contains implementation of our docker images on edge-orchestration(check other repo https://github.com/animeshjain2/person-s-age-detection). To run this part of project follow the process:

1.Install Docker from https://get.docker.com/. Just run the curl and shell Command(Always update after 1.5 month).

2.Learn about the docker from https://docs.docker.com/develop/.

3.Create edge-orchestration directory in var directory. After creating that create user and device directory in /var/edge-orchestration.

4.Create orchestration_userID.txt in /var/edge-orchestration/user directory and save Test in it then cretae orchestration_deviceID.txt in /var/edge-orchestration/device and save 7e841a12-a083-48fe-8040-83815e0b7410 in it.

5.After that install and setup edge-orchestration from https://github.com/lf-edge/edge-home-orchestration-go/blob/master/doc/platforms/x86_64_linux/x86_64_linux.md.

6.Pull Images from dockerhub https://hub.docker.com/r/animeshj123/age_det_image/tags for real time and video.

7.Before running image containers setup enviroment for the service.

    a). xhost +local:docker
	
    b).XSOCK=/tmp/.X11-unix
	
    c).XAUTH=/tmp/.docker.xauth
	
    d)xauth nlist $DISPLAY | sed -e 's/^..../ffff/' | xauth -f $XAUTH nmerge -
	
8. Run the service with api on Edge-orchestration:

     curl -X POST "IP/api/v1/orchestration/services" -H "accept: application/json" -H "Content-Type: application/json" -d "{ \"ServiceName\": \"<Give the name>\", \"ServiceInfo\": [{ \"ExecutionType\": \"container\", \"ExecCmd\": [ \"docker\", \"run\", \"-it\",\"--rm\",\"--device=/dev/video0\",\"-e\",\"DISPLAY=$DISPLAY \",\"-v\",\"$XSOCK:$XSOCK\",\"-v\",\"$XAUTH:$XAUTH\",\"-e\",\"XAUTHORITY=$XAUTH\",\"-e\",\" QT_X11_NO_MITSHM=1\",\"<image_name>\"]}], \"StatusCallbackURI\": \"http://localhost:8080/api/v1/services/notification\"}"
	 
9. Results:

        sudo docker logs -f edge-orchestration.  
    
