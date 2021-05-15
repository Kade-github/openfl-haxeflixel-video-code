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
