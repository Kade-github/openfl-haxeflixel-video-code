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
and add extra code
after `addChild(new FlxGame(gameWidth, gameHeight, initialState, zoom, updateframerate, drawframerate, skipSplash, startFullscreen));`
and before
`
 		#if !mobile
		addChild(new FPS(10, 3, 0xFFFFFF));
		#end
`
the code
`
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
`
so it would look something like
`
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
`
yess
