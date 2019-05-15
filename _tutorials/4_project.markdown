---
layout: page
title: V-REP Headless compile
img: /assets/img/vrep.jpg
---

To run V-REP in true headless mode, you have to compile it your self. This tutorial will explain exactly how to do that. I am as always working in an Ubuntu 18.04 environment, so keep that in mind.

First you will have to install some packages required for compiling V-REP. These can be installed using the following command:

{% highlight bash %}
sudo apt-get update && sudo apt-get install -y lua5.1 lua5.1-doc lua5.1-lgi lua5.1-lgi-dev lua5.1-policy lua5.1-policy-dev liblua5.1-0 liblua5.1-0-dbg liblua5.1-0-dev liblua5.1-dev libboost-all-dev
{% endhighlight %}

Now you need to make a new directory in which you will compile V-REP. I will use a directory called mybuild in my home directory:

{% highlight bash %}
mkdir ~/mybuild && cd ~/mybuild
{% endhighlight %}

Then you need to clone the V-REP repository to your install directory:

{% highlight bash %}
git clone https://github.com/CoppeliaRobotics/v_rep.git
{% endhighlight %}

To compile V-REP, several additional repositories are also needed. These should be placed in a programming directory as follows:
{% highlight bash %}
mkdir ~/mybuild/programming && cd ~/mybuild/programming
git clone https://github.com/CoppeliaRobotics/include.git
git clone https://github.com/CoppeliaRobotics/common.git
git clone https://github.com/CoppeliaRobotics/v_repMath.git
{% endhighlight %}

Now you need to create the makefile specifying that V-REP should be compiled in headless mode. You can download mine [here]({{ site.url }}/assets/files/makefile) (which also fixes various bugs with the default one). Please place this makefile inside the **~/mybuild/v_rep** directory.

You are now ready to compile V-REP:
{% highlight bash %}
cd ~/mybuild/v_rep && make
{% endhighlight %}

It is unfortunately not possible to run the compiled V-REP directly. Instead, we have to download a pre-compiled version of V-REP from [here](http://coppeliarobotics.com/ubuntuVersions.html){:target="_blank"} and then move the **libv_rep.so** from the newly compiled V-REP to the pre-compiled one. In the following, I have downloaded V-REP and placed it in a directory called **V-REP_PRO_EDU_V3_6_1_Ubuntu18_04_headless** in my home directory. Using the following command, the **libv_rep.so** is copied from the compiled to the pre-compiled V-REP directory:

{% highlight bash %}
cp -f ~/mybuild/v_rep/lib/libv_rep.so ~/V-REP_PRO_EDU_V3_6_1_Ubuntu18_04_headless/libv_rep.so
{% endhighlight %}

You should now be able to launch V-REP in headless mode:
{% highlight bash %}
~/V-REP_PRO_EDU_V3_6_1_Ubuntu18_04_headless/vrep.sh
{% endhighlight %}

You can follow [this tutorial](http://www.coppeliarobotics.com/helpFiles/en/commandLine.htm){:target="_blank"} to see what commands can be used for V-REP in headless mode.
Also see [this tutorial]({{ site.url }}/tutorials/6_multipleVREPs/) on how to have multiple instances of V-REP simulationsly.

*Plase contact me if you find any mistakes or bugs in this tutorial <i class="far fa-smile"></i>*
