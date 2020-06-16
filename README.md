# Edge-Orchestration-and-ML
This part of the github repo contains implementation of our docker images on edge-orchestration. To run this part of project follow the process check https://github.com/animeshjain2/Age-Detection for other part):

1.Install Docker from https://get.docker.com/. Just run the curl and shell Command(Always update after 1.5 month).

2.Learn about the docker from https://docs.docker.com/develop/.

3.Create edge-orchestration directory in var directory. After creating that create user and device directory in /var/edge-orchestration.

4.Create orchestration_userID.txt in /var/edge-orchestration/user directory and save Test in it then cretae orchestration_deviceID.txt in /var/edge-orchestration/device and save 7e841a12-a083-48fe-8040-83815e0b7410 in it.

5.After that install and setup edge-orchestration from https://github.com/lf-edge/edge-home-orchestration-go/tree/Baobab

6.Pull Images from dockerhub https://hub.docker.com/r/animeshj123/age_det_image/tags for real time and video.

7.Before running image containers setup enviroment(only for localhost machine) for the service.

    a). xhost +local:docker
	
    b).XSOCK=/tmp/.X11-unix
	
8. Run the service with api on Edge-orchestration:

curl -X POST "192.168.0.103:56001/api/v1/orchestration/services" -H "accept: application/json" -H "Content-Type: application/json" -d "{ \"ServiceName\": \"age_detection\", \"ServiceInfo\": [{ \"ExecutionType\": \"container\", \"ExecCmd\": [ \"docker\", \"run\", \"-it\",\"--rm\",\"--device=/dev/video0\", \"--net=host\",\"--ipc=host\", \"-e\",\"DISPLAY=$DISPLAY\",\"-v\",\"/tmp/.X11-unix:/tmp/.X11-unix\",\"-e\",\"QT_X11_NO_MITSHM=1\",\"animeshj123/age_det_image:02\"]}], \"StatusCallbackURI\": \"http://192.168.0.103:8888/api/v1/services/notification\"}"

	 
9. Results:

        sudo docker logs -f edge-orchestration.  
    
