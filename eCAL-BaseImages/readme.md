# How to create Docker Image for eCAL on Raspberry Pi 3

Just build the Image (staged file) like
```
docker build -t --rm uxdc-pi3-ecal-base:5.7.4 . -f Dockerfile-staged_uxdc-pi3-ecal-base_5.7.4
```

Running the Image in a Container
```
docker run --rm -itd --network host --name <Containername> uxdc-pi3-ecal-base:5.7.4 
```
  
Looking into the Container with bash
```
docker exec -it <Containername> bash
```
