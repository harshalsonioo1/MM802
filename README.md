# MM802
360- Degree video teleconferencing application. 

We developed an android application that can be downloaded in APK format and ran in any cell-phone. It allows users to play Live-streamed or pre-downloaded 360-degree VR videos using the native player of the app conected to any Google cardboard. Another way around, just play it on the cell-phone using our full-screen player.  

1 Requirements
Matlab(R2015a or higher) with Parallel Computing Toolbox and Image Processing Toolbox;
Any C++ IDE(Visual Studio 2015 is recommended);
FFMPEG(add the binary folder, e.g. “C:\Program Files\ffmpeg-20190625-dd662bb-win64-static\bin”, to system PATH.)
Python v3.6
Java version v8 with JDK 
PurplePill Unity3D SDK ( Can be downloaded from Google drive by clicking the link for APK file. )
Any Android device with Android version > 5.0

Pre-processing: 
Download the PANO's source code from the link here: https://drive.google.com/open?id=1oZnoxBnemrTsmUdhkvak8KHTyQ9SRg7p

To run server-side PANO:
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

To run the Client side:
  1) Download the apk file of our app through this link: https://drive.google.com/file/d/1K5cvTEQpyD8CcNHVuX7qsgCnl1Fe_H-2/view?usp=sharing
  2) Follow the demo video which can be found here: https://drive.google.com/open?id=1fAjwfCXBnIma5uSDhF_MYbDUBaIrQgX2
  
 Evaluation: 
 PSPNR: PSPNR values for every videos are generated whilst PANO is pre-processing the videos. File "CalcPSPNR" shows the calculation performed for the same. It can be compared with other methods using the code mentioned in "EvalPSPNR" which reads the PSPNR values generated by algorithm saved in ".mat" file format. 
 Bandwidth, FPS: Consumption of bandwidth is calculated by tracking the network charcateristic of the application in the cell phone using Game bench (https://blog.gamebench.net/measuring-frame-rates-in-android-and-ios-games). Cell- Phone must have root access.  
  
