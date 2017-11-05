# rostweet

The rostweet package provides a bridge between ROS nodes and the Twitter microblogging service.

## Install

The following instructions assume that `$ROS_HOME` points to the base installation directory of your ROS distribution, e.g. `/opt/ros/kinetic`. Substitute as appropriate.

Install system dependencies:

    sudo apt-get install libcurl4-openssl-dev

Clone the repository:

    git clone https://github.com/xperroni/rostweet.git

Create a catkin workspace (or `cd` into an existing one) and link the package directories into it. For a new workspace, you can use the commands below:

    mkdir -p ws/src
    cd ws/src
    catkin_init_workspace
    find $(cd ../.. ; pwd)/rostweet/ -mindepth 1 -maxdepth 1 -name 'ros*' | while read path; do ln -s $path $(basename $path); done
    cd ..

If you haven't done so yet, source the ROS environment:

    source $ROS_HOME/setup.bash

Build and install the rostweet packages:

    catkin_make install -DCMAKE_INSTALL_PREFIX=$ROS_HOME -DCMAKE_BUILD_TYPE=Release

## Usage

After starting `roscore` you can run the rostweet bridge with:

    rosrun rostweet bridge

This will ask for username and password to be manually entered. See the `rostweet/launch/` subdirectory for example launch files.

One the service is running, you can manually test it using RQT. Open the GUI and select _Plugin -> Services -> Services Caller_:

<img src="https://xperroni.github.io/rostweet/rqt_1.jpg">

Then use the Service Caller interface to configure and send a tweet:

<img src="https://xperroni.github.io/rostweet/rqt_2.jpg">

A tweet should then be posted to the connected account.

Also see `rostweet/examples/post.cpp` for how to access the bridge service programmatically.

