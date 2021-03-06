# MM802
360- Degree video teleconferencing application. 

Welcome! We developed an android application that can be downloaded in APK format and ran in any cell-phone - anytime, anywhere. It allows users to play Live-streamed or pre-downloaded 360-degree VR videos using the our VR native player or normal mobile full-screen. 
Before we begin, download the app on your android device  to enjoy the 360-degree experience from here: https://drive.google.com/open?id=1K5cvTEQpyD8CcNHVuX7qsgCnl1Fe_H-2

# Requirements and Pre-requisites:

-Matlab(R2015a or higher) with Parallel Computing Toolbox and Image Processing Toolbox;

-Any C++ IDE(Visual Studio 2015 is recommended);

-FFMPEG(add the binary folder, e.g. “C:\Program Files\ffmpeg-20190625-dd662bb-win64-static\bin”, to system PATH.)

-Python v3.6

-Java version v8 with JDK 

-PurplePill Unity3D SDK ( Can be downloaded from Google drive by clicking the link for APK file. )

-Any Android device with Android version > 5.0

# Pre-processing: 
-Download the PANO's source code from the link here: https://drive.google.com/open?id=1oZnoxBnemrTsmUdhkvak8KHTyQ9SRg7p

# To run server-side PANO:
  1)  Prepare the programs and data
    All the Matlab programs are in root folder “/”. The videos are in the folder “/videos”, the trajectory data is in two format is in “/traj” and “viewpoint”, the pre-calculated tile depth data is in “/DepthMap”. 
  
  2)  cut chunks
    run “/cutChunk.m” to cut the videos to one-second chunks in “/videos”.
  
  3)  calculate tile valueness
    set the variable calcTileVal to 1 in “/main.m”, then run “/main.m” to calculate the valueness of each tile in each chunk. The result is stored in “/ratio”.
  
  4)  generate tiling scheme
    if you’re using Visual Studio 2015, open the project file “/tilingDP/tilingDP.sln” and run it, otherwise you should build a new project in your IDE and copy “/tilingDP/main.cpp” into it, modify the data path at line 254/358/380 as appropriate. The tiling scheme is stored in “/tiling1004”.
  
  5)  run the simulation
    set the variable calcTileVal to 0 in “/main.m”, then run “/main.m”. The results about PSPNR and bitrate consumption per user per chunk are stored in “/baselineResult” and “/ourResult” for further analyzation.
    
The codes presented into MPD folder provides a snippet of our servers. It has webclient that we used initially to test our system. Currently, the server is loaded and running on our local machines. 

# To run the Client side:
  1) Download the apk file of our app through this link: https://drive.google.com/file/d/1K5cvTEQpyD8CcNHVuX7qsgCnl1Fe_H-2/view?usp=sharing
  2) Follow the demo video which can be found here: https://drive.google.com/open?id=1fAjwfCXBnIma5uSDhF_MYbDUBaIrQgX2
  
# Evaluation: 
  1) PSPNR: PSPNR values for every videos are generated whilst PANO is pre-processing the videos. File "PSPNR_Calc.m" shows the calculation performed for the same. It can be compared with other methods using the code mentioned in "PSPNR_eval_bandwidth.m" which reads the PSPNR values generated by algorithm saved in "component_wise_improvement.mat" file format. 
  
  2) Stardard Deviation, Frames per second (FPS): We have written a script file to calculate the average FPS and Standard deviation of the FPS across the video play. We are assesing the values of it on console using GameBench.  To see how FPS and STD is being calculated just load the HTML file and see the values on console from here: https://drive.google.com/open?id=1siSwKPPzYbp7sSYrjj41fnTU0QOQuc6z
  
  3) Bandwidth: Consumption of bandwidth is calculated by tracking the network charcateristic of the application in the cell phone using Game bench (https://blog.gamebench.net/measuring-frame-rates-in-android-and-ios-games). Cell- Phone must have root access.  
  
# Additional Details (Snippets - Insight into working of server and clients):

1) VideoTrackingAndDetection: This c++ main file functions to detect the objects inside the video frame using pre-trained YOLO model. This is the first step for our server as it gives cordinates of interestingness in the video. Using its results, PANO calculates the quality metrics. 

2)  PANO Tiling: This C++ file provides an insight into our Tiling Scheme. We have changed the parameters namely velocity, threshold, and coverage to optimize our results. 

3) MPD program: Unity c# script files for Web server and Web Client. 

4) FFMPEG Decoder: Decoding and understanding the received video stream at client side (Desktop-based). 

5) DecodingAndRendering : Unity decoder and render for client side player(Desktop-based).

6) apk_soruce_code: It has the link to the source code of our mobile application as well as the APK file that can be installed and run on spot.
