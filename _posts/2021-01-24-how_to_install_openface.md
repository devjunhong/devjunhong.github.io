---
title: "How to install OpenFace?"
excerpt: "Install OpenFace from the source code."
toc: true
toc_sticky: true
published: true
header:
  teaser: /assets/images/2021/01/24/openface_og.png
#   image: /assets/images/2021/01/24/openface_og_updated.png
#   caption: "Photo by me"
#   og_image: /assets/images/2021/01/24/openface_og_updated.png
layout: single
classes: wide

categories:
    - OpenFace
tags:
    - Face Detection
last_modified_at: 2021-01-24T08:06:00-05:00
---

# Intro 
Setting up the initial development environment is not really welcoming. If I'm going to upgrade my device, it is interesting. At least for me, I know it's the required work, but I want to spend my time to writing a code. Especially, when you failed a lot with multiple different approaches. Due to the outdated software, we find failure even though we try to follow the official document. Installing the [OpenFace](http://cmusatyalab.github.io/openface/) for me was the case. In this post, I'm going to what I tried to install the OpenFace, and how I managed to do it. 

# Official document
## By hand (fail)
My colleague tried to follow the official document[[5]](#fifth), and stuck on installing it. In the document, we can find several approaches; Docker, By hand, and Conda. This part of trial is the following of the 'By hand' section. 

The below is the error message we got. We tried to build it from source code using Ubuntu 20.04.1. Since it's built on the old version of Python, the preparation of set it up is required careful dependency issues.
```
[ 34%] Built target LandmarkDetector 
[ 54%] Built target FaceAnalyser 
[ 59%] Built target GazeAnalyser 
[ 81%] Built target Utilities 
[ 84%] Linking CXX executable ../../bin/FaceLandmarkImg /usr/bin/ld: cannot find -lThreads::Threads 
collect2: error: ld returned 1 exit status exe/FaceLandmarkImg/CMakeFiles/FaceLandmarkImg.dir/build.make:124: recipe for target 'bin/FaceLandmarkImg' failed 
make[2]: *** [bin/FaceLandmarkImg] Error 1 
CMakeFiles/Makefile2:308: recipe for target 'exe/FaceLandmarkImg/CMakeFiles/FaceLandmarkImg.dir/all' failed make[1]: ***
[exe/FaceLandmarkImg/CMakeFiles/FaceLandmarkImg.dir/all] Error 2 
Makefile:129: recipe for target 'all' failed make: *** [all] Error 2
```

# By hand (success)
After we stuck in the first trial, we moved to the next. By searching about the installation experience, we found an article[[1]](#first).  We are possible to install the OpenFace in our machine; Ubuntu 20.04.1 LTS. However, for our case, the article skips about installing OpenBlas. So, I attach how to install the OpenBlas here. And, I want to say thank you to the author(Pankaj Chejara) of the article. To install the OpenBLAS from the source, I followed this article [[2]](#second).
```sh
sudo apt-get update
sudo apt-get install build-essential
sudo apt-get install g++-8

sudo apt-get install cmake

sudo apt-get install git libgtk2.0-dev pkg-config libavcodec-dev libavformat-dev libswscale-dev

sudo apt-get install python-dev python-numpy libtbb2 libtbb-dev libjpeg-dev libpng-dev libtiff-dev libdc1394-22-dev

# start building OpenCV
wget https://github.com/opencv/opencv/archive/4.1.0.zip

sudo unzip 4.1.0.zip
cd opencv-4.1.0
mkdir build
cd build

cmake -D CMAKE_BUILD_TYPE=RELEASE -D CMAKE_INSTALL_PREFIX=/usr/local -D BUILD_TIFF=ON -D WITH_TBB=ON ..
make -j2
sudo make install
# if you don't see errors, it successes to install the OpenCV

# install dlib
wget http://dlib.net/files/dlib-19.13.tar.bz2
tar xf dlib-19.13.tar.bz2
cd dlib-19.13
mkdir build
cd build
cmake ..
cmake --build . --config Release
sudo make install
sudo ldconfig
cd ../..
# finish for dlib

sudo apt-get install libboost-all-dev

# install the OpenBLAS here 
git clone https://github.com/xianyi/OpenBLAS.git
cd OpenBLAS
make -j4
make install 
# if you see no errors on the screen, it finishes the install of the OpenBLAS

# starts to install the OpenFace
git clone https://github.com/TadasBaltrusaitis/OpenFace.git

cd OpenFace
mkdir build
cd build

cmake -D CMAKE_CXX_COMPILER=g++-8 -D CMAKE_C_COMPILER=gcc-8 -D CMAKE_BUILD_TYPE=RELEASE ..
make
# finish the installation of the OpenFace
```
After running the scripts, according to the article [[1]](#first), we can run the demo script. 
```sh
./bin/FaceLandmarkVid -f "../samples/changeLighting.wmv" -f "../samples/2015-10-15-15-14.avi"
```
I faced the exact same error as the author did. I copied some files (cen_patches_0.25_of.dat, cen_patches_0.35_of.dat, cen_patches_0.50_of.dat, cen_patches_1.00_of.dat) to the right place. 

I hope you can see the demo result too. 

![demo from the OpenFace](/assets/images/2021/01/24/openface.png)

# Using docker 
At the beginning of the installation, I thought if we can use docker, then it's no problem because the OpenFace is pretty popular for detecting the human face and landmark. I actually found several containers simply typing in the google. [[3]](#third), [[4]](#four) In this time, using docker is not an option for us. We've skipped utilizing it, but next time, I'm going to use docker definitely. It's the best way to align the development environment to the same point when I need to coperate with someone else. And also, there's an official document using docker too. [[5]](#fifth)

# Outro 
In this post, I've touched on installing the OpenFace which is famous for detecting a human face and pointing landmarks. The simple best way I recommend is using Docker, even though, I didn't try it in this post. I've managed to install it by building it on the local machine. Thanks for finding this post and I hope it saves your day. Please leave a comment or reaction if it is useful. Thanks 

# Reference 
<a name="first">[1]</a> [https://learnaitech.com/how-to-install-and-extract-facial-features-using-openface/](https://learnaitech.com/how-to-install-and-extract-facial-features-using-openface/)

<a name="second">[2]</a> [https://iq.opengenus.org/install-openblas-from-source/](https://iq.opengenus.org/install-openblas-from-source/)

<a name="third">[3]</a> [https://hub.docker.com/r/algebr/openface/](https://hub.docker.com/r/algebr/openface/)

<a name="four">[4]</a> [https://hub.docker.com/r/bamos/openface/](https://hub.docker.com/r/bamos/openface/)

<a name="fifth">[5]</a> [http://cmusatyalab.github.io/openface/setup/](http://cmusatyalab.github.io/openface/setup/)