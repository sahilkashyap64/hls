# hls
HLS with video resolution switcher button
The external library that helps in appending the resolution selector button works well with  video.js version 5
if you use it with higher version of video.js ,you might run into errors

# [Video.js - HTML5 Video Player][vjs]
# [Player In Action](https://sahilkashyap64.github.io/hls/index.html)

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
### quality selector

https://user-images.githubusercontent.com/32007662/175784040-9c7a633f-704e-4d9d-8d08-f9a19efe1bf8.mp4



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
index2:quality selector with new library


https://user-images.githubusercontent.com/32007662/175784474-34d0f9d3-1795-439e-aa5b-702a433f9593.mp4


---
---

**Load url - index3.html**

```javascript
 $(document).ready(function () {

            // An example of playing with the Video.js javascript API
            // Will start the video and then switch the source 3 seconds latter
            // You can look at the doc there: http://docs.videojs.com/docs/guides/api.html
            videojs('video').ready(function () {
                var myPlayer = this;
                myPlayer.qualityPickerPlugin();
                myPlayer.src({type: 'application/x-mpegURL', src: 'https://content.jwplatform.com/manifests/yp34SRmf.m3u8'});

                $("#change").on('click', function () {
                  var new_url = $("#myInput").val();
                    myPlayer.src({type: 'application/x-mpegURL', src: new_url});
                });
            });

        });
    
```
index3:quality selector , play any HLS link


https://user-images.githubusercontent.com/32007662/175784493-0a4ac953-e37a-4018-bcfa-3d0bb77b8c16.mp4


---
---

**Make videojs playlist -index4.html**

```javascript
         var types = {mp4:'video/mp4',webm:'video/webm', m3u: 'application/x-mpegURL'};
var videoList = [{
  sources: [{
    src: 'http://media.w3.org/2010/05/sintel/trailer.mp4',
    type: types.mp4
  }],
  poster: 'https://www.rt.com/static/img/og-logo-rt.png',name : 'Video 1',
}, {
  sources: [{
    src: 'https://content.jwplatform.com/manifests/yp34SRmf.m3u8',
    type: types.m3u
  }],
  poster: 'http://media.w3.org/2010/05/bunny/poster.png',name : 'Video 2',
}, {
  sources: [{
    src: 'https://vjs.zencdn.net/v/oceans.mp4',
    type: types.mp4
  }],
  poster: 'https://vjs.zencdn.net/v/oceans.png',name : 'Video 3',
}, {
  sources: [{
    src: 'http://media.w3.org/2010/05/bunny/movie.mp4',
    type: types.mp4
  }],
  poster: 'http://media.w3.org/2010/05/bunny/poster.png',name : 'Video 4',
}, {
  sources: [{
    src: 'http://media.w3.org/2010/05/video/movie_300.mp4',
    type: types.mp4
  }],
  poster: 'http://media.w3.org/2010/05/video/poster.png',name : 'Video 5',
}];

            // An example of playing with the Video.js javascript API
            // Will start the video and then switch the source 3 seconds latter
            // You can look at the doc there: http://docs.videojs.com/docs/guides/api.html
            videojs('video').ready(function () {
                var myPlayer = this;
                myPlayer.qualityPickerPlugin();
                myPlayer.playlist(videoList);
                myPlayer.playlistUi();

                $("#add").on('click', function () {
                 var currentplaylist= myPlayer.playlist();
                 let position=myPlayer.playlist.currentItem();
                 let lenh=videoList.length + 1;
                 console.log('len',lenh);
                   var new_url = $("#myInput").val();
                  videoList.push( {
  sources: [{
    src: new_url?new_url:'https://content.jwplatform.com/manifests/yp34SRmf.m3u8',
    type: 'application/x-mpegURL'
  }],
  poster: 'http://media.w3.org/2010/05/bunny/poster.png',name : 'Video '+lenh,
});

myPlayer.playlist(videoList,position);
 console.table(videoList);
 var updatedplaylist= myPlayer.playlist();
                  console.log('updatedplaylist',updatedplaylist);
                });
   
                var button = videojs.getComponent('Button');
//Close button
var closeButton = videojs.extend(button, {
    constructor: function() {
      button.apply(this, arguments);
      this.controlText("Exit Course");
      this.addClass('vjs-icon-cancel');
    },
    handleClick: function() {
      this.player().dispose();
    }
  });
  videojs.registerComponent('closeButton', closeButton);
  myPlayer.getChild('controlBar').addChild('closeButton', {});


// Extend default
var PrevButton = videojs.extend(button, {
  //constructor: function(player, options) {
  constructor: function() {
    button.apply(this, arguments);
    this.addClass('icon-angle-left');
    this.controlText("Previous");
  },


  handleClick: function() {
    console.log('clickedPrevious');
    myPlayer.playlist.previous();
  }
});

videojs.registerComponent('PrevButton', PrevButton);

myPlayer.getChild('controlBar').addChild('PrevButton', {}, 0);
           

       
/* Next BUTTON */
//var Button = videojs.getComponent('Button');

// Extend default
var NextButton = videojs.extend(button, {
  constructor: function() {
    button.apply(this, arguments);
    this.addClass('icon-angle-right');
    this.controlText("Next");
  },

  handleClick: function() {
    console.log('clickednext');
    myPlayer.playlist.next();
  }
}); 

videojs.registerComponent('NextButton', NextButton);

myPlayer.getChild('controlBar').addChild('NextButton', {}, 2);             

});
    
```

index4:playlist, jump to next and previous video
  (next and prev btn didn't render properly)


https://user-images.githubusercontent.com/32007662/175784532-3db02af0-5a5c-4bb6-8cc8-e1db52e1314c.mp4


---
---

**dynamic layer that plays any kind of links index5.html**

```javascript
        
        var vgsPlayer, poster;
  vgsPlayer = videojs('vid1');
  vgsPlayer.qualityMenu();
vgsPlayer.poster('https://img.youtube.com/vi/aqz-KE-bpKQ/maxresdefault.jpg');

/********* LOAD URL *********/
$('#vidlink li a').on('click', function(e) {
  e.preventDefault();
  var vidlink = $(this).attr('href');
  $('#vsg-vurl').val(vidlink);  
  $('input[type=submit]').click(); 
  //vsgLoadVideo(vidlink);
});


jQuery(function($) {

// vsgLoadVideo("https://www.youtube.com/watch?v=r1H98REH0c0");
// Video on page load

//jQuery(document).ready(function($) {

$("#vsg-loadvideo").submit(function(e) {
  e.preventDefault();

  var vidURL = $("#vsg-vurl").val();

  vsgLoadVideo(vidURL);

});

}); // jQuery(function($) END


function vsgLoadVideo(vidURL, poster) {

var type = getType(vidURL);

console.log(type);

if (getId(vidURL))
  poster = "http://img.youtube.com/vi/" + getId(vidURL) + "/hqdefault.jpg";

vgsPlayer.src({
  "src": vidURL,
  "type": type
});

vgsPlayer.httpSourceSelector();
if (poster)
  vgsPlayer.poster(poster);
else
  vgsPlayer.poster("//i.imgur.com/aE0LoTe.png");

// play seem to trigger to fast before Youtube is ready

//vgsPlayer.pause();
//	vgsPlayer.load();
vgsPlayer.play();
/*   setTimeout(function() {
  vgsPlayer.play();
}, 500); */

return false;

}


function ytVidId(url) {
//var p = /^(?:https?:\/\/)?(?:www\.)?youtube\.com\/watch\?(?=.*v=((\w|-){11}))(?:\S+)?$/;
//var p = /^.*(youtu.be\/|v\/|u\/\w\/|embed\/|watch\?v=|\&v=)([^#\&\?]*).*/;
var p = /^.*(youtu.be\/|v\/|u\/\w\/|embed\/|watch\?v=|\&v=|\?v=)([^#\&\?]*).*/;

if (url.match(p) || getId(url).length == 11)
  return false;
}

/**/
function getId(url) {
//var regExp = /^.*(youtu.be\/|v\/|u\/\w\/|embed\/|watch\?v=|\&v=)([^#\&\?]*).*/;
var regExp = /^.*(youtu.be\/|v\/|u\/\w\/|embed\/|watch\?v=|\&v=|\?v=)([^#\&\?]*).*/;
var match = url.match(regExp);

if (match && match[2].length == 11) {
  return match[2];
} else {
  return false;
}
}

var rtmp_suffix = /^rtmp:\/\//;
var hls_suffix = /\.m3u8/;
var mp4_suffix = /\.(mp4|m4p|m4v|mov)/i;
var hds_suffix = /\.f4m/;
var dash_suffix = /\.mpd/;
var flv_suffix = /\.flv/;
var webm_suffix = /\.webm/;
/* AUDIO */
//var mp3_suffix = /\.mp3/;
var mpeg_suffix = /\.(mp3|m4a)/i;
var ogg_suffix = /\.ogg/;

//var youtube_suffix = /\.youtube.com/;
//var yt_suffix = /^(?:https?:\/\/)?(?:www\.)?youtube\.com\/watch\?(?=.*v=((\w|-){11}))(?:\S+)?$/;
var yt_suffix = /^.*(youtu.be\/|v\/|u\/\w\/|embed\/|watch\?v=|\&v=)([^#\&\?]*).*/;
var dm_suffix = /\.?dailymotion.com/;
var vm_suffix = /\.?vimeo.com/;
/* ADVANCED REGEX */
//      var regVimeo = /^.*(vimeo.com\/)((channels\/[A-z]+\/)|(groups\/[A-z]+\/videos\/))?([0-9]+)/;
//      var regDailymotion = /^.+dailymotion.com\/(video|hub)\/([^_]+)[^#]*(#video=([^_&]+))?/;
//      var regMetacafe = /^.*(metacafe.com)(\/watch\/)(d+)(.*)/i;
//      var youtube_suffix = /(youtu.be\/|v\/|u\/\w\/|embed\/|watch\?v=|\&v=)([^#\&\?]*).*/;

function getType(url) {

/* AUDIO */
if (mpeg_suffix.test(url))
  return 'audio/mpeg';
if (ogg_suffix.test(url))
  return 'audio/ogg';
if (dash_suffix.test(url))
  return 'application/dash+xml';
if (rtmp_suffix.test(url))
  return 'rtmp/mp4';
if (hls_suffix.test(url))
  return 'application/x-mpegurl';
if (mp4_suffix.test(url))
  return 'video/mp4';
if (hds_suffix.test(url))
  return 'application/adobe-f4m';
if (flv_suffix.test(url))
  return 'video/flv';
if (webm_suffix.test(url))
  return 'video/webm';
if (yt_suffix.test(url)) {
  //alert(url.match(yt_suffix)[2]);
  //player.poster(ytmaxres(url.match(yt_suffix)[2]));
  //alert(ytmaxres(url.match(yt_suffix)[2]));
  return 'video/youtube';
}
if (dm_suffix.test(url))
  return 'video/dailymotion';
if (vm_suffix.test(url))
  return 'video/vimeo';

console.log('could not guess link type: "' + url + '" assuming mp4');
return 'video/mp4';
};

function getExt(ext) {

//if (ext == "youtube") ext = "mp4";
if (ext == "mp4" || ext == "m4v") ext = "m4v";
if (ext == "ogg" || ext == "ogv") ext = "oga";
if (ext == "webm") ext = "webmv";

return ext;
}
    
```
index5:play anykind of link eg: HLS,DASH,youtube,webm


https://user-images.githubusercontent.com/32007662/175784547-71b9f15f-5933-4746-8e51-87cce26cc6d2.mp4


---

---

**quality selector without plugins - index6.html**

```javascript 
videojs.Hls.xhr.beforeRequest = function (options) {
  /*
   * Modifications to requests that will affect every player.
   */

  let newUri = options.uri.includes('.ts') ? options.uri + "?q=test" : options.uri;

  return {
    ...options,
    uri: newUri };

};



let player = videojs("my-video", {responsive: true}, () => {
  console.log("Start");


  player.one("loadedmetadata", () => {

    let qualities = player.
    tech({ IWillNotUseThisInPlugins: true }).
    hls.representations();
console.log('qualities',qualities);
    createButtonsQualities({
      class: "item",
      qualities: qualities,
      father: player.controlBar.el_ });


    player.play();

    // ---------------------------------------------- //

    function createAutoQualityButton(params) {
      let button = document.createElement("div");

      button.id = "auto";
      button.innerText = `Auto`;

      button.classList.add("selected");

      if (params && params.class) button.classList.add(params.class);

      button.addEventListener("click", () => {
        removeSelected(params);
        button.classList.add("selected");
        qualities.map(quality => quality.enabled(true));
      });

      return button;
    }

    function createButtonsQualities(params) {

      let contentMenu = document.createElement('div');
      let menu = document.createElement('div');
      let icon = document.createElement('div');

      let fullscreen = params.father.querySelector('.vjs-fullscreen-control');
      contentMenu.appendChild(icon);
      contentMenu.appendChild(menu);
      fullscreen.before(contentMenu);

      menu.classList.add('menu');
      icon.classList.add('icon', 'vjs-icon-cog');
      contentMenu.classList.add('contentMenu');

      let autoButton = createAutoQualityButton(params);

      menu.appendChild(autoButton);

      qualities.sort((a, b) => {
        return a.height > b.height ? 1 : 0;
      });

      qualities.map(quality => {
        let button = document.createElement("div");

        if (params && params.class) button.classList.add(params.class);

        button.id = `${quality.height}`;
        button.innerText = quality.height + "p";

        button.addEventListener("click", () => {
          resetQuality(params);
          button.classList.add("selected");
          quality.enabled(true);
        });

        menu.appendChild(button);
      });

      setInterval(() => {
        let auto = document.querySelector("#auto");
        current = player.
        tech({ IWillNotUseThisInPlugins: true }).
        hls.selectPlaylist().attributes.RESOLUTION.height;
        console.log(current);

        document.querySelector("#auto").innerHTML = auto.classList.contains(
        "selected") ?

        `Auto <span class='current'>${current}p</span>` :
        "Auto";
      }, 1000);


    }

    function removeSelected(params) {
      document.querySelector("#auto").classList.remove("selected");
      [...document.querySelectorAll(`.${params.class}`)].map(quality => {
        quality.classList.remove("selected");
      });
    }

    function resetQuality(params) {
      removeSelected(params);

      for (let quality of params.qualities) {
        quality.enabled(false);
      }
    }
  });
});
    
```
index6:Quality selector without library


https://user-images.githubusercontent.com/32007662/175784642-dcaf94e9-c4a5-4ecb-9b95-fbde97e16e17.mp4


---



