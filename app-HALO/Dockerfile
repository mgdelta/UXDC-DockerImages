FROM deltacloud.mgdelta.de:5000/uxdc-pi3-ecal-base:5.7.4
RUN echo "SPI Test"
WORKDIR /home/HALO
RUN git clone -b eCAL_update https://github.com/mgdelta/UXDC-HALOCtrl.git
RUN install_packages libboost1.67-dev wiringpi
WORKDIR /home/HALO/UXDC-HALOCtrl/_build
RUN cmake .. && make

ENTRYPOINT ["tail" ,"-f", "/dev/null"]
