# jetson nano tf-posenet
### (1) jetPack install 
 * jetPack version 4.2.2

### (2) opencv 3.4.0 version download

#### Library Required
 - pkg-config
 - unzip
 - cmake
 - build-essential
1. Let's update the version and install the upgrade.
```
sudo apt-get update  
sudo apt-get upgrade 
```
2. OpenCV supports python with relatively concise code compared to C++.  Basically, 2.7 is installed, but we installed numpy and version 3.
sudo apt-get install python2.7-dev python3-dev python-numpy python3-numpy  
3. Install the necessary library for OpenCV.
```
sudo apt-get install libjpeg-dev libpng-dev libtiff-dev  
sudo apt-get install libavcodec-dev libavformat-dev libswscale-dev libv4l-dev v4l-utils   
sudo apt-get install libxvidcore-dev libx264-dev libxine2-dev  
sudo apt-get install libgstreamer1.0-dev libgstreamer-plugins-base1.0-dev  
sudo apt-get install libgtk-3-dev  
sudo apt-get install mesa-utils libgl1-mesa-dri libgtkgl2.0-dev libgtkglext1-dev  
sudo apt-get install libatlas-base-dev gfortran libeigen3-dev  
```
4. When the installation is complete, proceed to install OpenCV in earnest.
```
mkdir opencv  
cd opencv  
wget -O opencv.zip https://github.com/opencv/opencv/archive/3.4.0.zip  
wget -O opencv_contrib.zip https://github.com/opencv/opencv_contrib/archive/3.4.0.zip  
```
Create a folder called openencv and openencv.zip and openencv_contrib in the folder.Download the zip. 
Importantly, openencv and openencv_contrib versions must be the same. (3.4.0)  
5. When the installation is complete, enter the command below to extract it.
```
unzip opencv.zip  
unzip opencv_contrib.zip  
```
6. You now create build folders for build and installation to prepare for build.
```
cd opencv-3.4.0  
mkdir build  
cd build  
```
7. <span style="color:red">Build caution!<span> - You can't get one letter wrong, so make a copy of it on a notepadmit it.

```
  cmake -D CMAKE_BUILD_TYPE=RELEASE \  
-D CMAKE_INSTALL_PREFIX=/usr/local \  
-D WITH_TBB=OFF \  
-D WITH_IPP=OFF \  
-D WITH_1394=OFF \  
-D BUILD_WITH_DEBUG_INFO=OFF \  
-D BUILD_DOCS=OFF \  
-D INSTALL_C_EXAMPLES=ON \  
-D INSTALL_PYTHON_EXAMPLES=ON \  
-D BUILD_EXAMPLES=OFF \  
-D BUILD_TESTS=OFF \  
-D BUILD_PERF_TESTS=OFF \  
-D WITH_QT=OFF \  
-D WITH_GTK=ON \  
-D WITH_OPENGL=ON \  
-D OPENCV_EXTRA_MODULES_PATH=../../opencv_contrib-3.4.0/modules \  
-D WITH_V4L=ON  \  
-D WITH_FFMPEG=ON \  
-D WITH_XINE=ON \  
-D BUILD_NEW_PYTHON_SUPPORT=ON \  
-D PYTHON2_INCLUDE_DIR=/usr/include/python2.7 \  
-D PYTHON2_NUMPY_INCLUDE_DIRS=/usr/lib/python2.7/dist-packages/numpy/core/include/ \  
-D PYTHON2_PACKAGES_PATH=/usr/lib/python2.7/dist-packages \  
-D PYTHON2_LIBRARY=/usr/lib/x86_64-linux-gnu/libpython2.7.so \  
-D PYTHON3_INCLUDE_DIR=/usr/include/python3.6m \  
-D PYTHON3_NUMPY_INCLUDE_DIRS=/usr/lib/python3/dist-packages/numpy/core/include/  \  
-D PYTHON3_PACKAGES_PATH=/usr/lib/python3/dist-packages \  
-D PYTHON3_LIBRARY=/usr/lib/x86_64-linux-gnu/libpython3.6m.so \  
../  
```

8. You need to make it afterwards, but enter -j number (the desired number of cores used). If you enter -j4, you will use all four cores, which results in significant heat generation. (Error may occur) It is recommended to use when there is a cooler or a fan that can cool the board.
```
make -j4
```
```
make -j2
```
9. OpenCV Compilation Deliverables
```
sudo make install  
sudo sh -c 'echo '/usr/local/lib' > /etc/ld.so.conf.d/opencv.conf'  
sudo ldconfig  
```
### (3) tensorflow & tf-posenet-estimation Download and Install
```
git clone https://github.com/sdm6410/tf-posenet.git  
cd tf-pose-estimation  
sh install-tensorflow.sh  
sh install-pose-estimation.sh  
```
<img width="100%" src="https://user-images.githubusercontent.com/41135138/129160255-295aaa51-d6aa-4dd7-a1f9-89ad5b4f19c5.gif" />
