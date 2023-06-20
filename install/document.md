### Introduction
The HotSeconds plugin is mainly used for hot deploying code to remote servers, with a response time in seconds. It provides one-click operation throughout the entire process, saving a significant amount of time for the modify->package->deploy cycle. This plugin is divided into HotSecondsClient and HotSecondsServer.<br>
At present, only JDK 1.8 is supported. Support for higher versions will be considered in the future based on demand.<br>

Hot-deployment file range: support hot-deployment of all right-clicked files to the server, including java, .class files in jar, xml, html and other files, but path mapping needs to be configured for other files except java.<br>
Java hot loading range: modify code, add functions, add classes, etc.

### HotSecondsServer Installation
1.Upload HotSeconds1.0.zip to the server , and run 'sh install.sh'<br>
2.Copy hot-seconds-remote.xml to the resource directory of the code, and modify configurations like 'secret' as needed<br>
3.Add the JVM parameter -XXaltjvm=dcevm -javaagent:$path1/HotSecondsServer.jar=hotconf=$path2/hot-seconds-remote.xml<br>
Here, $path1 is the directory uploaded in the step 1, and $path2 is the directory uploaded in the step 2.<br>
If it is a java or .class file, you don’t need to add configuration, other files need to be filled<br>

### HotSecondsClient Installation
1.Download and install HotSecondsClient from the plugin market<br>
2.Go to the menu Run->HotSeconds Settings->Settings to add the server to connect to and configure<br>
The 'secret' should match that of the remote server. By filling in the local and remote mapping paths, files in the local directory, including files in subfolders, can be uploaded to the remote server.<br>
![](https://github.com/thanple/HotSecondsIDEA/blob/master/install/hotseconds-setting.png)
<br><br>
3. Run->HotSeconds Start/Stop to activate the HotSeconds plugin. Right-click to hot deploy the selected files to the remote server.<br>
![](https://github.com/thanple/HotSecondsIDEA/blob/master/install/use.png)
<br>The rules for uploading directories correspond to the Path mappings configured in the second step.<br><br>

### Plugin Keymap
In Keymap->Plugins->HotSecondsClient, you can customize shortcuts<br>
For instance, you can set shortcuts for HotSeconds Start/Stop and Hot swap this file.


### About extensions
This plug-in is not a panacea. After all, each company has its own framework, and there are so many open source frameworks on the market, but this plug-in is compatible with everything, and can expand the pre-logic and post-logic of uploading files. <br>
Copy IHotExtHandler.java in HotSeconds.zip to your project, implement this interface, and then configure your class name in hot-seconds-remote.xml, so that some logic that needs to refresh the cache and context can be done trigger.