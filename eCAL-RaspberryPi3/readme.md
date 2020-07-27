# How to create Docker Image for eCAL on Raspberry Pi 3

Just build the Image (staged file) like
```
docker build -t ecal_on_pi:v5.5.5 . -f Dockerfile.staged
```

Running the Image in a Container
docker run --rm -itd --network host --name <Containername> ecal_on_pi:v5.5.5 
  
Looking into the Container with bash
docker exec -it <Containername> bash
