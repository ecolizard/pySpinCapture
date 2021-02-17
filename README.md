# pySpinCapture
a python wrapper to the FLIR PySpin API to capture synchronized video

cameraCapture.py is a minimal program to configure a FLIR BlackFly S camera to stream compressed video data
to disk and output it to the screen in real-time. It is based on the FLIR Spinnaker PySpin API and its examples, 
and uses skvideo to wrap FFMPEG for fast H264 compression and writing, as well as tkinter to output to the screen. 
The camera is configured to output its 'ExposureActive' signal on Line 1, which allows precise alignment with a 
separate DAQ system as long as you have a free analog input channel at ~2x the frame rate or faster. This version
does not include triggering, so that the camera can run as fast as possible.

cameraCapture2cams.py extends functionality to 2 synchronized cameras, and uses triggering instead of freely 
running at the fastest possible frame rate. Note that this version requires a trigger to be sent to the cameras on
Line 0's, which are physically connected. 

cameraCapture2camsGpu.py is similar to cameraCapture2cams.py, but uses FFMPEG hardware encoding with NVIDIA's h26_nvenc
encoder, which is much faster and allows higher frame rates with minimal CPU and memory usage. This requires a compatible 
GPU as described at https://developer.nvidia.com/ffmpeg, https://trac.ffmpeg.org/wiki/HWAccelIntro.

cameraFreeRunNoCapture.py just outputs 2 camera streams to the monitor without saving.

All versions require a pull-up resistor to be installed between camera Line 1 and 3.3V signals to drive the exposure 
signal properly (as recommended in FLIR documentation; ~1kOhm seems to work well).
