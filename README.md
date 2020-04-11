# hls
HLS with video resolution switcher button
The external library that helps in appending the resolution selector button works well with  video.js version 5
if you use it with higher version of video.js ,you might run into errors

# [Video.js - HTML5 Video Player][vjs]


# Video player to play HLS video and have a video quality switch button 

A video player that plays m3u8 format videos and lets the user to switch video quality manually

## HLS
It has many streams(quality) of one video i.e 360p,480p,720p. And it adpats to stream based on network stream
[How to create m3u8 file](https://medium.com/@mayur_solanki/how-to-create-mpd-or-m3u8-video-file-from-server-using-ffmpeg-97e9e1fbf6a3)

## Problem
HLS video automatically switch video quality depending on the network speed. 
It adapats to internet speed and gives you the video
● What I wanted was, to have a button to switch between the quality
---

## Found 2 solution
 index.html   [Credits to Hasan Alibegić](https://github.com/halibegic)
| Lib | Version |
| ------ | ------ |
| video.js | ^5.19.2 |
| hls.min.js | ^0.9.1 |
| vjs-quality-picker.js | ^0.0.2 |
| videojs5-hlsjs-source-handler.min.js | ^0.3.1 |

index2.html
| Lib | Version |
| ------ | ------ |
|video.js |^6.6.3|
|videojs-quality-menu.min.js|^1|
|videojs-hlsjs-plugin|^stable|
|videojs-live-dvrux.min.js|^1|

---

## Running

**After clone**

```sh
$ cd hls
```

**index.html**

```javascript
        var player = videojs('video');

        player.qualityPickerPlugin();
        
        player.src({
            src: 'http://qthttp.apple.com.edgesuite.net/1010qwoeiuryfg/sl.m3u8',
            type: 'application/x-mpegURL'
        });

        player.play();
    
```
---

**index2.html**

```javascript
        var options = {
            plugins: {
                // JSON config added by Brightcove player generator
                streamrootHls: {
                    hlsjsConfig: {
                        // Your Hls.js config
                    },
                    // captionConfig: {
                    //     line: -1,
                    //     align: 'center',
                    //     position: 50,
                    //     size: 40,
                    // }
                },
                qualityMenu: {
                    useResolutionLabels: true
                }
            }
        };
        var player = videojs('example-video', options);
        player.qualityMenu();
        player.dvrux();
    
```
---
