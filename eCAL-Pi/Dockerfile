# Get base Image for Raspberry Pi 3 32Bit OS
FROM balenalib/raspberrypi3:latest as base

RUN echo 'Docker Image for eCAL (pub version)'

ARG ECAL_TAG_VERSION="v5.5.5"

# Python packages for using py with eCAL
#RUN install_packages python3-pip
#RUN install_packages python3.6-dev python3.7-dev

# dependency packages (with qt5, but we will not need it here in the headless docker image) 
RUN install_packages wget git cmake doxygen graphviz build-essential zlib1g-dev libhdf5-dev libprotobuf-dev libprotoc-dev protobuf-compiler libcurl4-openssl-dev file qt5-default \
	python3-pip python3.6-dev python3.7-dev openssl libssl-dev

# python modules necessary for eCAL
RUN python3 -m pip install setuptools

# let's get eCAL from public repository
WORKDIR /home/eCAL

# clone stable branch with all submodules
RUN git clone --branch $ECAL_TAG_VERSION --recursive git://github.com/continental/ecal.git 

# let's head for compiling
WORKDIR /home/eCAL/ecal/_build

# configure the shit and build it
# switched off apps because of problems for QT apps in this headless environment (unnecessary apps for this container)
# This config has to be ne adapted to the used eCAL Version
# Attention: v5.6.0 has an issue with the thirdparty tinyxml2
RUN cmake .. -DCMAKE_BUILD_TYPE=Release \
	-DECAL_THIRDPARTY_BUILD_PROTOBUF=OFF \
	#-DECAL_THIRDPARTY_BUILD_CURL=OFF \
	#-DECAL_THIRDPARTY_BUILD_HDF5=OFF \
	-DBUILD_SAMPLES=ON \
	-DECAL_INSTALL_SAMPLE_SOURCES=ON \
	-DBUILD_PY_BINDING=ON \
	-DECAL_INCLUDE_PY_SAMPLES=ON \
	-DBUILD_APPS=OFF \
	-DHAS_QT5=OFF \
	&& make -j4 \
	&& cpack -G DEB \
	&& dpkg -i _deploy/eCAL-* \
	&& cmake --build . --target create_python_egg --config Release \
	&& python3 -m easy_install _deploy/ecal-*

#RUN make -j4

# pack all files to a .deb package and install it
#RUN cpack -G DEB && dpkg -i _deploy/eCAL-*

# create python modules and install them in system
#RUN cmake --build . --target create_python_egg --config Release \
#	&& python3 -m easy_install _deploy/ecal-*

# we are ready for ecal, clean up sources and build folder to save image size
WORKDIR /home
RUN rm -rf eCAL

# Do nothing and keep this container running endless for development purposes only, remove later
# connect to this Container's shell with docker exec -it <mycontainer> bash
ENTRYPOINT ["tail", "-f", "/dev/null"]
