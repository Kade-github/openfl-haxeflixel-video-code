# openfl-haxeflixel-video-code
This is my research on how to play videos in openfl haxeflixel (webm only supported)
# How To Setup
1. Download the Friday Night Funkin source code in https://github.com/ninjamuffin99/Funkin (make sure its the new file system otherwise you need to put extra code `which i have the solution for lol`)
2. Install actuate by doing `haxelib install actuate`
3. Install the extension-webm fork by doing `haxelib git extension-webm https://github.com/GrowtopiaFli/extension-webm`
4. It won't work lol so type the command `lime rebuild extension-webm windows`
(sry idk how to fix this for mac)
5. Download the zip of this repository and copy paste the files inside the `source` folder to your fnf source code's `source` folder
6. Edit the `Main.hx` file in the fnf source code
And add after
```js
addChild(new FlxGame(gameWidth, gameHeight, initialState, zoom, updateframerate, drawframerate, skipSplash, startFullscreen));
```
And before
```js
#if !mobile
addChild(new FPS(10, 3, 0xFFFFFF));
#end
```
The code
```js
#if web
var str1:String = "HTML CRAP";
var vHandler = new VideoHandler();
vHandler.init1();
vHandler.video.name = str1;
addChild(vHandler.video);
vHandler.init2();
GlobalVideo.setVid(vHandler);
vHandler.source(ourSource);
#elseif desktop
var str1:String = "WEBM SHIT"; 
var webmHandle = new WebmHandler();
webmHandle.source(ourSource);
webmHandle.makePlayer();
webmHandle.webm.name = str1;
addChild(webmHandle.webm);
GlobalVideo.setWebm(webmHandle);
#end
```
So it would look something like
```js
addChild(new FlxGame(gameWidth, gameHeight, initialState, zoom, updateframerate, drawframerate, skipSplash, startFullscreen));
		
var ourSource:String = "assets/videos/DO NOT DELETE OR GAME WILL CRASH/dontDelete.webm";
		
#if web
var str1:String = "HTML CRAP";
var vHandler = new VideoHandler();
vHandler.init1();
vHandler.video.name = str1;
addChild(vHandler.video);
vHandler.init2();
GlobalVideo.setVid(vHandler);
vHandler.source(ourSource);
#elseif desktop
var str1:String = "WEBM SHIT"; 
var webmHandle = new WebmHandler();
webmHandle.source(ourSource);
webmHandle.makePlayer();
webmHandle.webm.name = str1;
addChild(webmHandle.webm);
GlobalVideo.setWebm(webmHandle);
#end

#if !mobile
addChild(new FPS(10, 3, 0xFFFFFF));
#end
```
# Setting up `Project.xml`
1. Edit `Project.xml` in the fnf source code
2. Find the section with `<haxelib name="etc" />`
3. Add these two extra lines
```xml
<haxelib name="actuate" />
<haxelib name="extension-webm" if="desktop" />
```
4. `FOLLOW THIS 4TH STEP ONLY IF YOUR USING THE OLD FILE SYSTEM`
In the section with `<assets path="bla">`
Add these two lines
```xml
<assets path="assets/videos" include="*.mp3" if="web"/>
<assets path="assets/videos" include="*.ogg" unless="web"/>
```
5. If your in the new file system
Create a new folder named `videos` inside assets/preload
If your in the old file system
Create a new folder named `videos` inside assets
# Setting up the desktop build
For all you windows users out there
You need to do an extra step
You must know how to use cmd or `Command Prompt`
(sorry but this is only for `64 bit` architectures)
1. Download ffmpeg
https://github.com/BtbN/FFmpeg-Builds/releases/download/autobuild-2021-05-14-20-06/ffmpeg-n4.4-15-ge87e006121-win64-gpl-shared-4.4.zip
2. Extract the zip file to your choice
3. Go inside the `bin` folder inside the extracted zip file
4. Open `Command Prompt`
5. Change directory inside the `bin` folder
6. `More on this later`
# Understanding of how video works
As you know, this only supports `webm` video files not `mp4` or `any other file type`
The reasoning of this is because of the different types of codecs not embedded inside openfl
Let me give an explanation
`Video Files` require a `codec`
a codec is an `encoder` or a `decoder` for video files
You `CANNOT` compress video files to a smaller size in modern times because they are already `COMPRESSED` and that is why we have `codecs` so you can't push the limit
OpenFL has no codec embedded into it that's why someone who made `openfl-webm` coded the webm codec from scratch using `c++` for haxe/openfl
But if you will ask `Why does it work for html?`
It's because when it comes to html the `BROWSER` has the codec
If you were to do it Natively `Native means an application that uses the system's commands instead of depending on other software like browsers which is for html5`, there are no codecs built into it.
Now if you were to ask `Why is it named extension-webm if it was openfl-webm then?` It's because `openfl-webm` is ancient and broken so someone made `extension-webm` to fix it: https://github.com/HaxeExtension/extension-webm
Now if you were to ask `Then why did i install https://github.com/GrowtopiaFli/extension-webm instead of https://github.com/HaxeExtension/extension-webm then?` It's because i added some extra code in `WebmPlayer.hx` to fix memory leaks.
Now if you were to ask `What are memory leaks?` well a memory leak is a thing wherein the memory is stuffed and not freed, in basic terms, your `RAM` processes more data.
Why you ask? it's because the video isn't being replaced but keep being added each time.
How did i fix this issue you asked? i added extra code to `WebmPlayer.hx` which allows you to change the `SOURCE VIDEO` of the webm player anytime.
# Solution for the desktop build
Now how will we setup the video on desktop?
Well in webm player there is `NO` audio support because it's broken lol so now we are in trouble but do not worry because ffmpeg is here to save us.
My solution is to `Audio Sync` a way of Synchronizing the audio version of the video to the video `You must have an ogg file either just the video's audio or just empty audio that lasts as long as the video's time`.
