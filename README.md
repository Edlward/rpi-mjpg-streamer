## A. Setup mjpg-streamer ##

#### install necessary packages for mjpg-streamer ####

```
$ sudo apt-get update

$ sudo apt-get install libv4l-dev libjpeg8-dev subversion imagemagick v4l-utils
```

#### build mjpg-streamer ####

```
$ svn co https://svn.code.sf.net/p/mjpg-streamer/code/mjpg-streamer/ mjpg-streamer

$ cd mjpg-streamer

$ sudo ln -s /usr/include/linux/videodev2.h /usr/include/linux/videodev.h

$ make USE_LIBV4L2=true clean all
```

#### (for Raspberry Pi Camera boards) setup video4linux ####

```
$ sudo modprobe bcm2835-v4l2

$ sudo vi /etc/modules

# add following line
bcm2835-v4l2
```

#### Add yourself to the video group ####

```
$ sudo usermod -a -G video $USER
```

## B. Run mjpg-streamer ##

#### Run mjpg-streamer from the shell directly ####

```
# copy & edit run-mjpg-streamer.sh to your environment or needs
$ cp run-mjpg-streamer.sh.sample run-mjpg-streamer.sh
$ vi run-mjpg-streamer.sh

# then run
$ ./run-mjpg-streamer.sh
```

#### Run mjpg-streamer as a service ####

```
# copy & edit init/mjpg-streamer to your environment or needs
$ sudo cp init/mjpg-streamer.sample /etc/init.d/mjpg-streamer
$ sudo chmod +x /etc/init.d/mjpg-streamer
$ sudo vi /etc/init.d/mjpg-streamer

# then register as a boot-up service
$ sudo update-rc.d mjpg-streamer defaults

# or remove it
$ sudo update-rc.d -f mjpg-streamer remove

# and start/stop it
$ sudo service mjpg-streamer start
$ sudo service mjpg-streamer stop
```

