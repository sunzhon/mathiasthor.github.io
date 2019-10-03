---
layout: page
title: Dynamixel Software
img: /assets/img/dynamixel.jpg
---

This guide assumes that you are running Ubuntu 18 and that you want to control dynamixel XM-430 servos using the U2D2.

## 1) SET USB LATENCY
Start by setting the USB latency on the NUC for fast communication. This can be done by running the following command:
{% highlight bash %}
sudo usermod -aG dialout $USER && echo 1 | sudo tee /sys/bus/usb-serial/devices/ttyUSB0/latency_timer
{% endhighlight %}

You can check it by running the following:
{% highlight bash %}
cat /sys/bus/usb-serial/devices/ttyUSB0/latency_timer
{% endhighlight %}

## 2) Install dependencies
The following dependencies need to be installed on the nuc.
### 2.1) ROS
To install ROS melodic on ubuntu 18 run the following commands:
{% highlight bash %}
sudo sh -c 'echo "deb http://packages.ros.org/ros/ubuntu $(lsb_release -sc) main" > /etc/apt/sources.list.d/ros-latest.list'
{% endhighlight %}
{% highlight bash %}
sudo apt-key adv --keyserver hkp://ha.pool.sks-keyservers.net:80 --recv-key 421C365BD9FF1F717815A3895523BAEEB01FA116
{% endhighlight %}

{% highlight bash %}
sudo apt-get update
{% endhighlight %}

{% highlight bash %}
sudo apt-get install ros-melodic-desktop-full
{% endhighlight %}
### 2.2) Dynamixel SDK and ROS Controller
Run the following commands to install the remaining dependencies:
{% highlight bash %}
sudo apt-get install -y git cmake python-tempita python-catkin-tools python-lxml xsltproc qt4-qmake libqt4-dev libqscintilla2-dev
{% endhighlight %}
Run the following to install the Dynamixel Workbench used for communicating with the servos through ROS:
{% highlight bash %}
sudo apt-get install ros-melodic-dynamixel-sdk
{% endhighlight %}
{% highlight bash %}
mkdir ~/catkin_ws && cd ~/catkin_ws
{% endhighlight %}
{% highlight bash %}
mkdir src && cd src
{% endhighlight %}
{% highlight bash %}
git clone https://github.com/MathiasThor/my_dynamixel_workbench.git
git clone https://github.com/MathiasThor/dynamixel-workbench.git
git clone https://github.com/ROBOTIS-GIT/dynamixel-workbench-msgs.git
git clone https://github.com/stonier/qt_ros
{% endhighlight %}
{% highlight bash %}
cd dynamixel-workbench-msgs && git checkout f91ae7dbd5d368a3121ca5bb901771b2e6471c01
{% endhighlight %}
{% highlight bash %}
source /opt/ros/melodic/setup.bash
source /home/$USER/catkin_ws/devel/setup.sh
{% endhighlight %}
In order to add the above command to your .bashrc use the following command:
{% highlight bash %}
gedit ~/.bashrc
{% endhighlight %}
and add the following in the end of the file:
{% highlight bash %}
source /opt/ros/melodic/setup.bash
source /home/$USER/catkin_ws/devel/setup.sh
{% endhighlight %}
Finally, compile the dynamixel ros controller:
{% highlight bash %}
cd ../.. && catkin_make
{% endhighlight %}

<!-- ![bitmoji](https://render.bitstrips.com/v2/cpanel/c0c6b631-0229-4042-80f0-140dd391f73a-20ec22bc-5fe2-4596-aab9-58b8d5de5ce9-v1.png?transparent=1&palette=1&width=246) -->
