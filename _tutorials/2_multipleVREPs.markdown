---
layout: page
title: Multiple V-REP instances
img: /assets/img/vrep.jpg
---

## 1) Download V-REP
Download V-REP from the official webpage [here](http://www.coppeliarobotics.com/downloads.html){:target="_blank"}.
This guide is verified to work with v.3.6.2 and Ubuntu 18.04.

## 2) Extract
Extract the V-REP .zip file in the V-REP directory as many times as you need workers for your reinforcement learning algorithm (e.g., 4 times)

## 3) Make the V-REP directories unique
Go to the extracted directories (feel free to rename these). In remoteApiConnections.txt change portIndex1_port to something unique so they are not the same for any V-REP instance (e.g., 19995, 19996, 19997, 19998). Make a new file in all the extracted directories called simulationID.txt and write a unique ID (e.g., 1, 2, 3, 4) (don't use zero and don't jump any numbers). The command for writing the ID’s are as follows:
{% highlight bash %}
touch simulationID.txt
echo "1" > simulationID.txt
{% endhighlight %}

Finally, copy and replace  “libv_repExtRosInterface.so” from /home/mat/workspace/gorobots-mthor/utils/v-rep_simulations/v-rep_libs/reallib/libv_repExtRosInterface.so to the V-REP_# directory.
