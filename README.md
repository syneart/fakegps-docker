# fakegps-docker

Docker container with N210/B210/B200-mini

Requirements

Docker 1.9.1 (aufs)
====================================
---------------------------------------
    # docker info
Server Version: 1.9.1<br>
Storage Driver: aufs<br>
Root Dir: /var/lib/docker/aufs<br>
　Backing Filesystem: extfs<br>
　Dirs: 31<br>
　Dirperm1 Supported: true<br>
Execution Driver: native-0.2<br>
Logging Driver: json-file<br>
Kernel Version: 4.2.0-19-generic<br>
Operating System: Ubuntu 15.10<br>
CPUs: 1<br>

---------------------------------------
Ubuntu 14.04 LTS (or later) <br>
gnuradio-3.7.8.1 (or later)<br>
UHD-3.9.0 (or later)<br>

---------------------------------------

=first of all you need to have admin privileges  
    
    $ sudo su -
    
=setup Docker
    
    # curl -sSL https://get.docker.com | sh
    # docker run -i -t --name="fakegps_usrp" --privileged -v /dev/bus/usb:/dev/bus/usb ubuntu:14.04 /bin/bash

    # apt update
    # apt upgrade -y
    # apt install vim -y

\<Enter Running Container>

=Give terimal some color
    
    # sed -i 's/#force_color_prompt=yes/force_color_prompt=yes/g' '/root/.bashrc'

=Install PyBOMBS
    
    # apt-get install python-pip
    # pip install -U pip
    # pip install PyBOMBS
    # pybombs prefix init /usr/local -a usrlocal
    # pybombs config default_prefix /usr/local
    # pybombs recipes add gr-recipes git+https://github.com/gnuradio/gr-recipes.git
    # pybombs recipes add gr-etcetera git+https://github.com/gnuradio/gr-etcetera.git
    # pybombs -v install uhd gnuradio
    # ldconfig

=Download uhd images
    
    # /usr/local/lib/uhd/utils/uhd_images_downloader.py

=Test
    
    # uhd_usrp_probe
    
~ gps-sdr-sim (latest)

    # git clone https://github.com/osqzss/gps-sdr-sim
    # cd gps-sdr-sim/
    # apt-get install gcc
    # gcc gpssim.c -lm -O3 -o gps-sdr-sim
    # rm gpssim.bin; ./gps-sdr-sim -e brdc3540.14n -l 22.3089337,113.9296219,100 -s 2500000 -b 8
    # ./gps-sdr-sim-uhd.py -t gpssim.bin -s 2500000 -x 1000


----commit docker's container

	sudo docker commit -m="ORAL" -a="SyA" ec07a43b236a usrp/fakegps_oral
