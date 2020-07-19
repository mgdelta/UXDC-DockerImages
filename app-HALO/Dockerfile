FROM ecal-v5.5.0:latest
RUN echo "SPI Test"
WORKDIR /home/HALO
RUN git clone -b eCAL_update https://github.com/mgdelta/UXDC-HALOCtrl.git
RUN install_packages libboost1.67-dev wiringpi
WORKDIR /home/HALO/UXDC-HALOCtrl/_build
RUN cmake .. && make

ENTRYPOINT ["tail" ,"-f", "/dev/null"]
