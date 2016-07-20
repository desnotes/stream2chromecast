Stream2Chromecast
=================

A Chromecast media streamer for Linux.

Stream2Chromecast casts audio and video files to a Chromecast device from Linux.

It can also transcode any unsupported files in real time and play them on the Chromecast.

It is written in Python 2.7 and uses either ffmpeg or avconv for transcoding.




Installation
------------
To play media file types that are unsupported by Chromecast, we need either ffmpeg or avconv installed to do the transcoding.

On Ubuntu we can either install avconv:-

    sudo apt-get install libav-tools
   
...or install ffmpeg

    sudo add-apt-repository ppa:mc3man/trusty-media
    apt-get install ffmpeg
   



Functionality
-------------
To stream supported media files to a Chromecast.

        stream2chromecast.py my_media.mp4


To transcode and stream unsupported media files to a Chromecast.
    (This requires either ffmpeg or avconv to be installed. See Installation.)

        stream2chromecast.py -transcode my_mpeg_file.mpg

To play a supported file from a URL.
    This plays the file directly from the remote address, so the file must be streamable and cannot be transcoded.

        stream2chromecast.py -playurl http://www.example.com/my_media.mp4


###Control playback

 - pause playback (currently only works when not transcoding)
   
        stream2chromecast.py -pause
       
 - continue (unpause) playback (currently only works when not transcoding)
   
        stream2chromecast.py -continue
       
 - stop playback
   
        stream2chromecast.py -stop  


###Volume control

 - set volume (takes a value between 0.0 and 1.0)

        stream2chromecast.py -setvol <volume>

 - increase or decrease volume by 0.1
 
        stream2chromecast.py -volup
        stream2chromecast.py -voldown
        
 - mute volume

        stream2chromecast.py -mute
        
        
          
###Status

 - get Chromecast status

        stream2chromecast.py -status
        
        
###Specifying a device when there are multiple Chromecasts on the network
To specify a device by name or IP address, use the -devicename parameter.
e.g.

 - To play a file on a device named "my_chromecast"
 
        stream2chromecast.py -devicename my_chromecast my_media.mp4

 - To play a file on a device at IP address 192.168.1.10
 
        stream2chromecast.py -devicename 192.168.1.10 my_media.mp4

 - To search the network and list the available devices
        
        stream2chromecast.py -devicelist


###Specify which transcoder to use
If both ffmpeg and avconv are installed, ffmpeg will be used by default. 

 - To specify avconv to be used and transcode a playback, use the -transcoder option

        stream2chromecast.py -transcoder avconv -transcode <file>
        

###Supply custom transcoder parameters
It is possible pass in specific parameters to ffmpeg or avconv using the -transcodeopts parameter with the options surrounded by quotes

 - To specify an output video bitrate of 1000k and an audio bitrate of 128k

        stream2chromecast.py -transcodeopts '-b:v 1000k -b:a 128k' -transcode <file>
        
            
###Specify a port to use for streaming media.
By default, a random unused port will be selected to serve the media from. In a firewalled environment, it can be useful to be able to specify the port to open

 - To specify port 8765 to serve media from
 
        stream2chromecast.py -port 8765 <file>


Notes
-----
avconv is a fork of ffmpeg. It is included in the Ubuntu in the repositories rather than ffmpeg. However there is a PPA repository available which contains the latest builds of ffmpeg. See the installation notes.


To Do
-----
    Automatic identification of media types that need transcoding.
    Add an option to pass raw ffmpeg / avconv options to the transcoder.
    Python 3 compatibility...?
    

License
-------
stream2chromecast.py is GPLv3 licensed.



Thanks
------
The excellent PyChromecast library by Paulus Schoutsen has been a great help for information on building the interface.

https://github.com/balloob/pychromecast


Thanks to TheCrazyT for this gist:-

https://gist.github.com/TheCrazyT/11263599


Thanks to [dohliam](https://github.com/dohliam) for bug fixes and additional functionality.

Thanks to [interlocuteur](https://github.com/interlocuteur) for bug fixes, error reports & advice.
