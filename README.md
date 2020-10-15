# Tutorial_Ubuntu_18.04_Install_OpenCV
Install OpenCV on Ubuntu 18.04

## Step 1: Update Packages
```sudo apt -y update```  
```sudo apt -y upgrade```

## Step 2: Install OS Libraries
#### 1. Remove 
```sudo apt -y remove x264 libx264-dev```  

#### 2. Install Libraries
```sudo apt -y install build-essential checkinstall cmake pkg-config yasm```  
```sudo apt -y install git gfortran```  
```sudo apt -y install libjpeg8-dev libpng-dev```  
```sudo apt -y install software-properties-common```  
```sudo add-apt-repository "deb http://security.ubuntu.com/ubuntu xenial-security main"```  

```sudo apt -y update```  
```sudo apt -y install libjasper1```  
```sudo apt -y install libtiff-dev``` 

```sudo apt -y install libavcodec-dev libavformat-dev libswscale-dev libdc1394-22-dev```  
```sudo apt -y install libxine2-dev libv4l-dev``` 

```sudo apt -y install libgstreamer1.0-dev libgstreamer-plugins-base1.0-dev```  
```sudo apt -y install libgtk2.0-dev libtbb-dev qt5-default```  
```sudo apt -y install libatlas-base-dev```  
```sudo apt -y install libfaac-dev libmp3lame-dev libtheora-dev```  
```sudo apt -y install libvorbis-dev libxvidcore-dev```  
```sudo apt -y install libopencore-amrnb-dev libopencore-amrwb-dev```  
```sudo apt -y install libavresample-dev```  
```sudo apt -y install x264 v4l-utils``` 

#### (Optional Dependencies)
```sudo apt -y install libprotobuf-dev protobuf-compiler```  
```sudo apt -y install libgoogle-glog-dev libgflags-dev```  
```sudo apt -y install libgphoto2-dev libeigen3-dev libhdf5-dev doxygen```  


#### 3. Link
```cd /usr/include/linux```  
```sudo ln -s -f ../libv4l1-videodev.h videodev.h```  


## Step 3: Install Python Libraries
```sudo apt -y install python3-dev python3-pip```  
```sudo -H pip3 install -U pip numpy```  
```sudo apt -y install python3-testresources```

## Step 4: Download opencv and opencv_contrib
#### 1. Make a work file  
```mkdir opencv3411 && cd opencv3411```   
#### 2. Download opencv version 3.4.11  and download opencv_contrib version 3.4.11   
Check the version at https://opencv.org/releases/  
```git clone -b 3.4.11 https://github.com/opencv/opencv```  
```git clone -b 3.4.11 https://github.com/opencv/opencv_contrib```  

## Step 5: Compile and install OpenCV with contrib modules  
#### 1. Make a build file  
```mkdir build && cd build```  
  
Directory tree structure  
```
.
├──opencv3411
│   ├── build
│   ├── opencv
│   └── opencv_contrib
```

#### 2. Compile  
```cmake -D WITH_CUDA=ON -D PYTHON_DEFAULT_EXECUTABLE=/usr/bin/python3 -D OPENCV_EXTRA_MODULES_PATH=../opencv_contrib/modules ../opencv```  
You can change the file to anaconda virtual environment location

Check the modules you need will be built.  
For example,  
```
--   OpenCV modules:
--     To be built:                 alphamat aruco bgsegm bioinspired calib3d ccalib core cudaarithm cudabgsegm cudacodec cudafeatures2d cudafilters cudaimgproc cudalegacy cudaobjdetect cudaoptflow cudastereo cudawarping cudev datasets dnn dnn_objdetect dnn_superres dpm face features2d flann freetype fuzzy gapi hdf hfs highgui img_hash imgcodecs imgproc intensity_transform line_descriptor ml objdetect optflow phase_unwrapping photo plot python3 quality rapid reg rgbd saliency sfm shape stereo stitching structured_light superres surface_matching text tracking ts video videoio videostab xfeatures2d ximgproc xobjdetect xphoto
--     Disabled:                    world
--     Disabled by dependency:      -
--     Unavailable:                 cnn_3dobj cvv java js julia matlab ovis python2 viz
```

Then,   
```make```  or ```make -j8``` will be faster.  


#### 3. Install
```sudo make install```  
```sudo ldconfig```

## Finish  
Check pkg-config  
```pkg-config opencv --libs --cflags```
For example, 
```
-I/usr/local/include/opencv -I/usr/local/include -L/usr/local/lib -lopencv_cudabgsegm -lopencv_cudaobjdetect -lopencv_cudastereo -lopencv_stitching -lopencv_cudafeatures2d -lopencv_superres -lopencv_cudacodec -lopencv_videostab -lopencv_cudaoptflow -lopencv_cudalegacy -lopencv_cudawarping -lopencv_aruco -lopencv_bgsegm -lopencv_bioinspired -lopencv_ccalib -lopencv_dnn_objdetect -lopencv_dpm -lopencv_highgui -lopencv_videoio -lopencv_face -lopencv_freetype -lopencv_fuzzy -lopencv_hdf -lopencv_hfs -lopencv_img_hash -lopencv_line_descriptor -lopencv_optflow -lopencv_reg -lopencv_rgbd -lopencv_saliency -lopencv_sfm -lopencv_stereo -lopencv_structured_light -lopencv_phase_unwrapping -lopencv_surface_matching -lopencv_tracking -lopencv_datasets -lopencv_text -lopencv_dnn -lopencv_plot -lopencv_xfeatures2d -lopencv_shape -lopencv_video -lopencv_ml -lopencv_ximgproc -lopencv_xobjdetect -lopencv_objdetect -lopencv_calib3d -lopencv_imgcodecs -lopencv_features2d -lopencv_flann -lopencv_xphoto -lopencv_photo -lopencv_cudaimgproc -lopencv_cudafilters -lopencv_imgproc -lopencv_cudaarithm -lopencv_core -lopencv_cudev
```
