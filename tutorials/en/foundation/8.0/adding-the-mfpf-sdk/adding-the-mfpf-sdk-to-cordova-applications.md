---
layout: tutorial
title: Adding the MobileFirst Platform Foundation SDK to Cordova Applications
breadcrumb_title: Cordova SDK
relevantTo: [cordova]
weight: 1
---
<ul>
<li class="download-sample">
<a href="https://github.com/MobileFirst-Platform-Developer-Center/Cordova" target="_blank">Download MobileFirst project</a>
        </li>
</ul>

<h2>Overview</h2>
<p>You can use the IBM MobileFirst Platform Command Line Interface (CLI) to leverage MobileFirst features in Cordova applications. This is made possible by packaging the MobileFirst SDK as a plug-in for Cordova named <code>cordova-plugin-mfp</code>.</p>
<p>Use this tutorial as a guide to create Cordova applications by using the MobileFirst CLI, add supported platforms to the application, and add MobileFirst features and 3rd-party Cordova plug-ins.<br />
The tutorial also explains the initialization flow of IBM MobileFirst Platform Foundation in a Cordova application, and how to register the application to MobileFirst Server.</p>
<p><strong>Notes:</strong></p>
<ul>
<li>MobileFirst CLI contains an instance of Cordova CLI v5.0.0, Android platform version 3.6.4, and iOS platform version 3.7.0. It is not possible to upgrade or replace these embedded versions. Therefore, it is not a requirement for you to install Cordova on your developer workstation.</li>
<li>Only Android and iOS are supported for creating Cordova apps by using the MobileFirst CLI.</li>
</ul>
<h3>Topics</h3>
<ul>
<li><a href="#cordovaCLICommands">Cordova CLI commands</a></li>
<li><a href="#creatingCordovaProject">Creating a Cordova project</a></li>
<li><a href="#cordovaProjectStructure">Cordova project structure</a></li>
<li><a href="#mobileFirstPlatformInitializationFlow">MobileFirst Platform initialization flow</a></li>
<li><a href="#previewWebResources">Previewing the application web resources</a></li>
<li><a href="#testingAnApplication">Testing an application on an emulator or device</a></li>
<li><a href="#managingCordovaPlatforms">Managing Cordova platforms</a></li>
<li><a href="#managingCordovaPlugins">Managing Cordova plug-ins</a></li>
<li><a href="#registeringApplications">Registering applications</a></li>
<li><a href="#supportedMFPFeatures">Supported MobileFirst features</a></li>
<li><a href="#sampleApplication">Sample application</a></li>
</ul>
<h2 id="cordovaCLICommands">Cordova CLI commands</h2>
<p>You can create a Cordova-based project with the MobileFirst plug-in by using the MobileFirst CLI. For more information about downloading and using the MobileFirst CLI, see the <a href="../advanced-client-side-development/updated-using-cli-to-create-build-and-manage-mobilefirst-project-artifacts/">Using CLI to create, build, and manage MobileFirst project artifacts</a> tutorial.</p>
<p>To see a list of the available Cordova commands, open <strong>Terminal</strong> and run the following command: <code>mfp cordova</code>.</p>
<p>[code gutter="false"]<br />
NAME<br />
     mobilefirst cordova</p>
<p>SYNOPSIS<br />
     mfp cordova &lt;command&gt; [options]</p>
<p>DESCRIPTION<br />
     IBM MobileFirst Platform Command Line Interface (CLI) for Cordova specific<br />
     actions.</p>
<p>     Specific help for each command is available. For example:<br />
     mfp help cordova create</p>
<p>GLOBAL COMMANDS<br />
     config .............................. View or alter configuration settings</p>
<p>PROJECT COMMANDS<br />
     cordova create .............................. Creates a new Cordova project<br />
     cordova emulate .................................. Emulates Cordova project<br />
     cordova platform ................................ Manages project platforms<br />
     cordova plugin .................................... Manages project plugins<br />
     cordova prepare ............................... Prepares a Cordova project<br />
     cordova preview ......................... Previews existing Cordova project<br />
     cordova run .......................................... Runs Cordova project</p>
<p>COMMAND-LINE FLAGS/OPTIONS<br />
     -v, --version ...............Prints out the version number of this utility<br />
     -d, --debug ........................Debug mode produces a debug log output<br />
     -dd, --ddebug ................... Debug mode produces a verbose log output</p>
<p>EXAMPLE USAGE<br />
     $ mfp cordova create myapp --platform android<br />
     $ cd myapp<br />
     $ mfp cordova preview<br />
     $ mfp cordova emulate --platform android<br />
[/code]</p>
<h2 id="creatingCordovaProject">Creating a Cordova project</h2>
<p>To create a Cordova application, run the command: <code>mfp cordova create</code>.<br />
You can use either the Interactive Mode as detailed below, or the Direct Mode (see <code>mfp help cordova create</code>).</p>
<ol>
<li>Enter the application name, package ID, application version, and desired platforms:</li>
<p>[code]<br />
[?] Enter name of app: MyCordovaApp<br />
[?] Enter the package ID: (com.ibm.MyCordovaApp)<br />
[?] Enter the app version: (1.0.0)<br />
[?] Select platforms to be supported by your app: (Press &lt;space&gt; to select)<br />
 ❯⬢ android<br />
  ⬢ ios<br />
[/code]</p>
<li>A default set of Cordova plug-ins, including <code>cordova-plugin-mfp</code>, are automatically added to the application. You can also add additional standard Cordova plug-ins.</li>
<p>[code]<br />
[?] The following plugins are automatically added to your app:<br />
cordova-plugin-mfp<br />
org.apache.cordova.device<br />
org.apache.cordova.dialogs<br />
org.apache.cordova.geolocation<br />
org.apache.cordova.globalization<br />
org.apache.cordova.inappbrowser<br />
org.apache.cordova.network-information</p>
<p>Please press enter to continue...</p>
<p>[?] Select additional plugins you would like to add:<br />
 ❯⬡ cordova-plugin-mfp-jsonstore<br />
  ⬡ cordova-plugin-mfp-push<br />
  ⬡ org.apache.cordova.battery-status<br />
  ⬡ org.apache.cordova.camera<br />
  ⬡ org.apache.cordova.console<br />
  ⬡ org.apache.cordova.contacts<br />
  ⬡ org.apache.cordova.device-motion<br />
  ⬡ org.apache.cordova.device-orientation<br />
  ⬡ org.apache.cordova.file<br />
  ⬡ org.apache.cordova.file-transfer<br />
  ⬡ org.apache.cordova.media<br />
  ⬡ org.apache.cordova.media-capture<br />
  ⬡ org.apache.cordova.splashscreen<br />
  ⬡ org.apache.cordova.statusbar<br />
  ⬡ org.apache.cordova.vibration<br />
[/code]</p>
<li>You can use an application template for your project. The CLI provides the default template <em>cordova-hello-world-mfp</em>. You can create your own repository of app templates to speed up your development process and point the path to the application template that you want to use.</li>
<p>[code]<br />
[?] Enter a path to an app template to be added: (cordova-hello-world-mfp)<br />
[/code]</p>
<blockquote><p>To learn more about Cordova application templates, see the topic about developing Cordova client apps, in the user documentation.</p></blockquote>
<li>The Cordova project is generated with the selected platforms and plug-ins.</li>
<p><a href="https://developer.ibm.com/mobilefirstplatform/wp-content/uploads/sites/32/2015/06/cordova-app.png"><img src="{{ site.baseurl }}/assets/backup/cordova-app-1024x560.png" alt="cordova-app" width="980" height="536" class="aligncenter size-large wp-image-14871" /></a></p>
</ol>
<h2 id="cordovaProjectStructure">Cordova project structure</h2>
<p>After the Cordova project is created, the following files and folders are generated. This project structure follows the standard Cordova project structure:</p>
<p><a href="https://developer.ibm.com/mobilefirstplatform/wp-content/uploads/sites/32/2015/06/cordova-project-structure.png"><img src="{{ site.baseurl }}/assets/backup/cordova-project-structure.png" alt="cordova-project-structure" width="220" height="237" class="alignright size-full wp-image-14355" /></a></p>
<ul>
<li><strong>application-descriptor.xml</strong> - Application metadata for MobileFirst</li>
<li><strong>config.xml</strong> - The Cordova configuration file with extended MobileFirst-related preferences</li>
<li><strong>hooks</strong> - The Cordova hooks folder</li>
<li><strong>mobilefirst</strong> - The folder that contains MobileFirst artifacts: <code>.wlapp</code> files that MobileFirst Server needs to recognize applications, as explained below</li>
<li><strong>platforms</strong> - The folder that contains Cordova platforms support</li>
<li><strong>plugins</strong> - The folder that contains Cordova plug-ins</li>
<li><strong>www</strong> - The folder that contains the application web resources</li>
</ul>
<h2 id="mobileFirstPlatformInitializationFlow">MobileFirst Platform initialization flow</h2>
<p>The initialization flow is similar to the flow of a MobileFirst Hybrid app. During initialization, the MobileFirst Cordova Plugin runs <code>WL.Client.init(wlInitOptions)</code>. After initialization completes, the function <code>wlCommonInit()</code> is called.</p>
<p>The <code>wlInitOptions</code> object and the <code>wlCommonInit</code> function are available inside the <code>index.js</code> file, which is part of the <em>cordova-hello-world-mfp</em> template. You can use the standard Cordova <code>deviceready</code> event to handle Cordova initialization, but the function <code>wlCommonInit</code> is the recommended way to identify that MobileFirst features are ready to be used.</p>
<p>[code lang="js"]<br />
var Messages = {<br />
    // Add here your messages for the default language.<br />
    // Generate a similar file with a language suffix containing the translated messages.<br />
    // key1 : message1,<br />
};</p>
<p>var wlInitOptions = {<br />
    // Options to initialize with the WL.Client object.<br />
    // For initialization options please refer to IBM MobileFirst Platform Foundation Knowledge Center.<br />
};</p>
<p>// Called automatically after MFP framework initialization by WL.Client.init(wlInitOptions).<br />
function wlCommonInit(){<br />
	// Common initialization code goes here<br />
    document.getElementById('app_version').innerText = WL.Client.getAppProperty(&quot;APP_VERSION&quot;);<br />
    document.getElementById('mobilefirst').setAttribute('style', 'display:block;');<br />
}</p>
<p>var app = {<br />
    // Application Constructor<br />
    initialize: function() {<br />
        this.bindEvents();<br />
    },</p>
<p>    // Bind any events that are required on startup. Common events are:<br />
    // 'load', 'deviceready', 'offline', and 'online'.<br />
    bindEvents: function() {<br />
        document.addEventListener('deviceready', this.onDeviceReady, false);<br />
    },</p>
<p>    // The scope of 'this' is the event. In order to call the 'receivedEvent'<br />
    // function, 'app.receivedEvent(...);' must be explicitly called.<br />
    onDeviceReady: function() {<br />
        app.receivedEvent('deviceready');<br />
    },</p>
<p>    // Update the DOM on a received event.<br />
    receivedEvent: function(id) {<br />
        var parentElement = document.getElementById(id);<br />
        var listeningElement = parentElement.querySelector('.listening');<br />
        var receivedElement = parentElement.querySelector('.received');</p>
<p>        listeningElement.setAttribute('style', 'display:none;');<br />
        receivedElement.setAttribute('style', 'display:block;');</p>
<p>        console.log('Received Event: ' + id);<br />
    }<br />
};</p>
<p>app.initialize();<br />
[/code]</p>
<h2 id="previewWebResources">Previewing the applications web resources</h2>
<p>You might want to preview the web resources of your application outside any specific platform, for example to debug common JavaScript logic.</p>
<p>Before you can preview application web resources, you must have a MobileFirst Development Server running. If a MobileFirst Server instance is not yet available, use the <code>mfp create</code> command to setup a new MobileFirst back-end project, followed by the <code>mfp start</code> command to initialize MobileFirst Server.</p>
<p>[code]<br />
mfp create MyMFPProject<br />
cd MyMFPProject<br />
mfp start<br />
[/code]</p>
<p>When previewing the Cordova app, you can make selections by using either the MobileFirst Operations Console Simple Browser Rendering, or Mobile Browser Simulator.<br />
After MobileFirst Server is started, navigate to the Cordova application folder and use the <code>mfp cordova preview</code> command to preview the application:</p>
<p>[code]<br />
mfp cordova preview<br />
[?] Select how to preview your app: (Use arrow keys)<br />
❯ browser: Simple browser rendering<br />
  mbs: Mobile Browser Simulator</p>
<p>[?] Select platform(s) to be previewed: (Press &lt;space&gt; to select)<br />
❯⬡ ios<br />
 ⬡ android<br />
[/code]</p>
<h2 id="testingAnApplication">Testing an application on an emulator or device</h2>
<p>To run the application by using the Android Emulator or the iOS Simulator, use the <code>emulate</code> command:<br />
[code]mfp cordova emulate[/code]</p>
<p>Alternately, you can plug a device into your computer and test the app directly on it by using the <code>run</code> command:<br />
[code]mfp cordova run[/code]</p>
<p><strong>Note:</strong> If you do not have a device plugged and execute the <code>run</code> command, this command starts an emulator/simulator, so that the behavior is the same as that of the <code>emulate</code> command.</p>
<p>[code]<br />
[?] What platforms do you want to run on? (Use arrow keys)<br />
   android<br />
 ❯ ios<br />
[/code]</p>
<p><a href="https://developer.ibm.com/mobilefirstplatform/wp-content/uploads/sites/32/2015/06/cordova-preview-e1437034704442.jpg"><img src="{{ site.baseurl }}/assets/backup/cordova-preview-e1437034704442.jpg" alt="cordova-preview" width="253" height="500" class="aligncenter size-full wp-image-14832" /></a></p>
<h2 id="managingCordovaPlatforms">Managing Cordova platforms</h2>
<p>You can manage the available platforms in the Cordova project by using the <code>platform</code> command: <code>mfp cordova platform [option]</code>.</p>
<ul>
<li>Add a new platform to Cordova app: <code>mfp cordova platform add</code><br />
[code]mfp cordova platform add<br />
[?] Select platforms to be supported by your app: (Press &lt;space&gt; to select)<br />
 ❯⬡ android<br />
  ⬡ ios<br />
[/code]
</li>
<li>List available platforms in Cordova app: <code>mfp cordova platform list</code><br />
[code]mfp cordova platform list<br />
Installed Platforms: ios 3.7.0<br />
Available Platforms: android<br />
[/code]</li>
<li>Remove a platform: <code>mfp cordova platform remove</code><br />
[code]mfp cordova platform remove<br />
[?] Select the configured platform(s) to remove from this app: (Press &lt;space&gt; to select)<br />
 ❯⬡ ios 3.7.0<br />
[/code]
</li>
<li>Update Cordova assets for each platform in Cordova app: <code>mfp cordova platform update</code></li>
</ul>
<h2 id="managingCordovaPlugins">Managing Cordova plug-ins</h2>
<p>You can manage the plug-ins used in the Cordova project by running the command:</p>
<p>[code]mfp cordova plugin [option][/code]</p>
<ul>
<li>Add<br />
        [code]<br />
[?] Select plugins(s) to be added to your app: (Press &lt;space&gt; to select)<br />
 ❯⬡ cordova-plugin-mfp-jsonstore<br />
  ⬡ org.apache.cordova.battery-status<br />
  ⬡ org.apache.cordova.camera<br />
  ⬡ org.apache.cordova.console<br />
  ⬡ org.apache.cordova.contacts<br />
  ⬡ org.apache.cordova.device-motion<br />
  ⬡ org.apache.cordova.device-orientation<br />
  ⬡ org.apache.cordova.file<br />
  ⬡ org.apache.cordova.file-transfer<br />
  ⬡ org.apache.cordova.media<br />
  ⬡ org.apache.cordova.media-capture<br />
  ⬡ org.apache.cordova.splashscreen<br />
  ⬡ org.apache.cordova.statusbar<br />
  ⬡ org.apache.cordova.vibration<br />
  ⬡ Add 3rd party plugin<br />
[/code]</li>
<li>List<br />
[code]<br />
cordova-plugin-mfp 7.1.0 &quot;IBM MobileFirst Platform Foundation&quot;<br />
org.apache.cordova.device 0.2.13 &quot;Device&quot;<br />
org.apache.cordova.dialogs 0.2.11 &quot;Notification&quot;<br />
org.apache.cordova.geolocation 0.3.11 &quot;Geolocation&quot;<br />
org.apache.cordova.globalization 0.3.3 &quot;Globalization&quot;<br />
org.apache.cordova.inappbrowser 0.5.4 &quot;InAppBrowser&quot;<br />
org.apache.cordova.network-information 0.2.14 &quot;Network Information&quot;<br />
[/code]</li>
<li>Remove<br />
[code]<br />
mfp cordova plugin remove org.apache.cordova.camera<br />
[/code]</li>
<li>Search<br />
[code]<br />
mfp cordova plugin search barcode<br />
[/code]</li>
<li>Update<br />
[code]<br />
mfp cordova plugin update<br />
[/code]</li>
</ul>
<h2 id="registeringApplications">Registering applications</h2>
<h3>Registering applications to a local development server</h3>
<p>The <code>mfp push</code> command is used to register client applications and deploy required application and adapter assets to MobileFirst Server.<br />
[code]mfp push[/code]</p>
<p>If you are previewing an app in the Browser, you can refresh the browser after the <code>push</code> command to preview the new version pushed.</p>
<h3>Registering applications to a remote development server</h3>
<p>It is also possible to register an application to an existing remote MobileFirst Server, such as a QA, UAT, preproduction or production server. The <code>mfp push</code> command can be used with the remote server name specified.</p>
<p>Create a remote server definition by using the command: <code>mfp server add</code>.<br />
You are prompted to provide a name, a fully qualified server address (<code>protocol://host-or-ip-address:port</code>), admin username and password, and additional details.</p>
<p>[code]mfp server add<br />
[?] Enter name of new server definition: myserver<br />
[?] Enter the fully qualified URL of this server: http://192.168.0.1:10080<br />
[?] Enter the MFP admin login id: admin<br />
[?] Enter the MFP admin password: *****<br />
[?] Save admin password for this server?: No<br />
[?] Enter the context root of the MobileFirst administration services: worklightadmin<br />
[?] Make this server the default?: (Y/n) n[/code]</p>
<p>To push to the newly defined remote server, run the command: <code> mfp push <em>myserver</em></code>.<br />
The <code>push</code> command connects to the server and retrieves the list of available back-end projects to be selected.</p>
<p>After pushing an application to the remote server, the application configuration (w<code>orklight.plist</code>/<code>wlclient.properties</code>, <code>config.xml</code> files) are updated to point to the remote server as the back-end server for the app.</p>
<p>By default, the <code>mfp push</code> command points to a local development server. Use <code>mfp server info</code> to list all defined servers and default servers.</p>
<blockquote><p>To learn more, see the <a href="../advanced-client-side-development/updated-using-cli-to-create-build-and-manage-mobilefirst-project-artifacts/">Using CLI to create, build, and manage MobileFirst project artifacts</a> tutorial.</p></blockquote>
<h2 id="supportedMFPFeatures">Supported MobileFirst features</h2>
<p>Not all MobileFirst features are currently supported by the MobileFirst SDK in Pure Cordova applications.</p>
<h3>Supported features</h3>
<ul>
<li>Direct Update</li>
<li>Push Notifications</li>
<li>JSONStore</li>
<li>3rd-party Cordova plug-ins<br />
        <strong>Note</strong>: 3rd-party plug-ins are plug-ins that are developed outside the Apache Cordova core plugins.<br />
        IBM provides customer support for the core plug-ins provided by Apache Cordova.<br />
        IBM does not provide customer support for 3rd-party Cordova plug-ins. Support for these plug-ins is provided by their developers.</li>
</ul>
<h3>Unsupported features</h3>
<ul>
<li>FIPS 140-2</li>
<li>Tealeaf</li>
<li>Cloudant</li>
<li>Shell applications</li>
<li>Swappable Cordova CLI and platform versions</li>
<li>Swappable WebViews (CrossWalk)</li>
</ul>
<blockquote><p>For more details about what features are supported by MobileFirst Cordova plug-in, see the product user documentation.</p></blockquote>
<p><a href="https://developer.ibm.com/mobilefirstplatform/wp-content/uploads/sites/32/2015/06/cordova-sample-app2.png"><img src="{{ site.baseurl }}/assets/backup/cordova-sample-app2.png" alt="cordova-sample-app" width="260" class="alignright size-full wp-image-15103" /></a></p>
<h2 id="sampleApplication">Sample application</h2>
<p><a href="https://github.com/MobileFirst-Platform-Developer-Center/Cordova" target="_blank">Click to download</a> the MobileFirst project.</p>
<p>The provided Cordova application contains a single screen with three buttons which exemplify possible uses of Cordova plug-ins and MobileFirst features:</p>
<ul>
<li>The <strong>VIBRATE</strong> button uses the Cordova plug-in <code>org.apache.cordova.vibration</code> to make the device vibrate.</li>
<li>The <strong>CAMERA</strong> button opens the device camera and presents the picture taken.</li>
<li>The <strong>RSS FEED</strong> button uses a MobileFirst adapter to retrieve data from a RSS feed and presents an alert message with the total of topics obtained from the feed.</li>
</ul>
<p><br clear="all" /></p>
<h3>Running the sample</h3>
<ol>
<li>Download and extract the sample <code>.zip</code> file.</li>
<li>From the command line, navigate to the <code>RSSAdapter</code> folder and run the command <code>mfp start</code> to start the MobileFirst Server.</li>
<li>Navigate to the <code>CordovaApp</code> folder and run the following commands:
<ul>
<li><code>mfp cordova platform add</code>, then follow the interactive instructions to add the iOS and Android platforms</li>
<li><code>mfp cordova plugin add</code></li>
<p>, then select the </ul>
<p><strong>cordova-plugin-mfp</strong>, <strong>org.apache.cordova.camera</strong> and <strong>org.apache.cordova.vibration</strong> plugins
    </li>
<li><code>mfp push</code></li>
<p> to register the Cordova application in the MobileFirst Server</p>
<li>Run the application by using the command <code>mfp cordova run</code> and follow the interactive instructions to select the device to run. If no device is present, an emulator is used instead.</li>
</ol>
<h3>Building the sample step by step</h3>
<p>Follow these instructions to implement the sample application.</p>
<ol>
<li>
<h4>Create the Cordova application</h4>
</li>
<p>Create a Cordova project by running the <code>mfp cordova create</code> command. Provide a name for it, and accept all the other default values. The application folder is created, with the default application template.</p>
<li>
<h4>Add the Vibration and Camera Plug-ins</h4>
</li>
<p>To add the Cordova Vibration and Camera plug-ins to the Cordova project, run the following commands:</p>
<p>[code]<br />
mfp cordova plugin add org.apache.cordova.vibration<br />
mfp cordova plugin add org.apache.cordova.camera<br />
[/code]<br />
Optionally, you can run the interactive command <code>mfp cordova plugin add</code> and select the vibration and camera plugins from the list presented.</p>
<li>
<h4>Edit the index.html file</h4>
</li>
<p>Edit the <code><em>your-app-name</em>/www/index.html</code> file to add the three buttons: <strong>VIBRATE</strong>, <strong>CAMERA</strong>, and <strong>RSS FEED</strong>, a list to present the results from RSS FEED, and an image to present the result from the camera plug-in:</p>
<p>[code lang="html"]<br />
&lt;body&gt;<br />
     &lt;div id=&quot;menu&quot; &gt;<br />
        &lt;img id=&quot;image&quot; /&gt;<br />
        &lt;a onclick=&quot;app.vibrate()&quot;&gt;VIBRATE&lt;/a&gt;<br />
        &lt;a onclick=&quot;app.getPicture()&quot;&gt;CAMERA&lt;/a&gt;<br />
        &lt;a onclick=&quot;app.getRSSFeed()&quot;&gt;RSS FEED&lt;/a&gt;<br />
        &lt;div id=&quot;div_rss&quot;&gt;<br />
          &lt;h1&gt;RSS FEED ITEMS&lt;/h1&gt;<br />
          &lt;ul id=&quot;list_rss&quot;&gt;&lt;/ul&gt;<br />
        &lt;/div&gt;<br />
      &lt;/div&gt;<br />
&lt;/body&gt;<br />
[/code]</p>
<li>
<h4>Edit the index.css file</h4>
<p>Edit the file <code><em>your-app-name</em>/www/css/index.css</code> to update the visual of the app.</p>
<p>[code lang="css"]<br />
body {<br />
  position: absolute;<br />
  height: 100%;<br />
  width: 100%;<br />
  text-align: right;<br />
  font-family: &quot;HelveticaNeue-Light&quot;, &quot;Helvetica Neue Light&quot;, &quot;Helvetica Neue&quot;, Helvetica, Arial, &quot;Lucida Grande&quot;, sans-serif;<br />
  font-weight: 300;<br />
  background: url(../img/bg-portrait.png);<br />
  background-size: cover;<br />
  background-repeat: no-repeat;<br />
  overflow: auto;<br />
}<br />
body, p, div{<br />
  margin: 0;<br />
}<br />
p {<br />
  padding-right: 5px;<br />
}<br />
div {<br />
  position: relative;<br />
  margin-right: 20px;<br />
  margin-left: 20px;<br />
  padding-right: 2px;<br />
  clear: both;<br />
  display:block;<br />
}<br />
a{<br />
  display:block;<br />
  font-size: 20px;<br />
  text-transform: none;<br />
  background-color:#00B2EF;<br />
  color:#FFFFFF;<br />
  margin-bottom: 10px;<br />
  margin-top: 2px;<br />
  padding-right: 5px;<br />
}<br />
li {<br />
  font-size:15px;<br />
  border-bottom: 1px solid #ccc;<br />
  text-align: center;<br />
}</p>
<p>.version_label {<br />
  font-weight: bold;<br />
  background-color:#FFFFFF;<br />
}<br />
#app_version {<br />
  padding-left: 2px;<br />
}<br />
#deviceready {<br />
  width: 160px;<br />
}<br />
#image{<br />
  width: 140px;<br />
}<br />
#menu {<br />
  top: 50%;<br />
}<br />
#div_rss{<br />
  display: none;<br />
  text-align: center;<br />
}<br />
.blink {<br />
    animation:fade 3000ms infinite;<br />
    -webkit-animation:fade 3000ms infinite;<br />
    -moz-animation:fade 3000ms infinite;<br />
}<br />
@-webkit-keyframes fade {<br />
    from { opacity: 1.0; }<br />
    50% { opacity: 0.4; }<br />
    to { opacity: 1.0; }<br />
}<br />
@keyframes fade {<br />
    from { opacity: 1.0; }<br />
    50% { opacity: 0.4; }<br />
    to { opacity: 1.0; }<br />
}<br />
.event {<br />
    color:#FFFFFF;<br />
}<br />
.listening {<br />
    background-color:#333333;<br />
    display:block;<br />
}<br />
.received {<br />
    background-color:#4B946A;<br />
    display:none;<br />
}<br />
/* Landscape layout (with min-width) */<br />
@media screen and (min-aspect-ratio: 1/1) and (min-width:400px) {<br />
  body {<br />
    background: url(../img/bg-landscape.png);<br />
    background-size: cover;<br />
    background-repeat: no-repeat;<br />
    max-height: 400px;<br />
  }<br />
}<br />
[/code]</p>
</li>
<li>
<h4>Edit the index.js file</h4>
</li>
<p>Edit the file <code>your-app-name/www/js/index.js</code> to implement the behavior of the buttons.</p>
<ul>
<li>For the <strong>VIBRATE</strong> button, use the function <code>navigator.vibrate(time)</code> to trigger the vibration.</li>
<li>For the <strong>CAMERA</strong> button, use the function <code>navigator.camera.getPicture(onSuccess,onFailure,options)</code> to open the camera.</li>
<li>For the <strong>RSS FEED</strong> button, use the <code>WLResourceRequest</code> API method to call the adapter procedure <code>getStories</code>, as described in the <a href="../server-side-development-category/invoking-adapter-procedures-hybrid-client-applications/" target="_blank">Invoking adapter procedures from hybrid client applications</a> tutorial.</li>
</ul>
<p>[code lang="js" highlight="39-78"]<br />
var Messages = {<br />
    // Add here your messages for the default language.<br />
    // Generate a similar file with a language suffix containing the translated messages.<br />
    // key1 : message1,<br />
};</p>
<p>var wlInitOptions = {<br />
    // Options to initialize with the WL.Client object.<br />
    // For initialization options please refer to IBM MobileFirst Platform Foundation Knowledge Center.<br />
};</p>
<p>// Called automatically after MFP framework initialization by WL.Client.init(wlInitOptions).<br />
function wlCommonInit(){<br />
	// Common initialization code goes here<br />
    document.getElementById('menu').setAttribute('style', 'display:block;');<br />
}</p>
<p>var app = {<br />
    // Application Constructor<br />
    initialize: function() {<br />
        this.bindEvents();<br />
    },</p>
<p>    // Bind any events that are required on startup. Common events are:<br />
    // 'load', 'deviceready', 'offline', and 'online'.<br />
    bindEvents: function() {<br />
        document.addEventListener('deviceready', this.onDeviceReady, false);<br />
    },</p>
<p>    // The scope of 'this' is the event. In order to call the 'receivedEvent'<br />
    // function, 'app.receivedEvent(...);' must be explicitly called.<br />
    onDeviceReady: function() {<br />
        app.receivedEvent('deviceready');<br />
    },</p>
<p>    // Update the DOM on a received event.<br />
    receivedEvent: function(id) {<br />
    },<br />
    // Trigger the vibration<br />
    vibrate: function(){<br />
        WL.Logger.info(&quot;vibrating&quot;);<br />
        navigator.vibrate(3000);<br />
    },<br />
    // Trigger the camera<br />
    getPicture: function(){<br />
        navigator.camera.getPicture(app.getPictureSuccess, app.getPictureFail, { quality: 50,<br />
            destinationType: Camera.DestinationType.FILE_URI });<br />
    },<br />
    // Receive the result from the camera<br />
    getPictureSuccess: function(imageURI){<br />
        WL.Logger.info(&quot;getPicture success &quot;+imageURI);<br />
        document.getElementById(&quot;image&quot;).src=imageURI;<br />
    },<br />
    // Called when some error occur with the camera<br />
    getPictureFail: function(){<br />
        WL.Logger.error(&quot;getPicture failed&quot;);<br />
    },<br />
    // Execute a request to RSSAdapter/getStories<br />
    getRSSFeed: function(){<br />
        var resourceRequest = new WLResourceRequest(<br />
                    &quot;/adapters/RSSAdapter/getStories&quot;,<br />
                    WLResourceRequest.GET);<br />
        resourceRequest.send().then(app.getRSSFeedSuccess,app.getRSSFeedError);<br />
    },<br />
    // Receive the response from RSSAdapter<br />
    getRSSFeedSuccess:function(response){<br />
        WL.Logger.info(&quot;getRSSFeedsSuccess&quot;);<br />
        //The response.responseJSON element contains the data received from the back-end<br />
        alert(&quot;Total RSS Feed items received:&quot;+response.responseJSON.rss.channel.item.length);<br />
    },<br />
    // Called when some error occurs during the request to RSSAdapter<br />
    getRSSFeedError:function(response){<br />
        WL.Logger.error(&quot;Response ERROR:&quot;+JSON.stringify(response));<br />
        alert(&quot;Response ERROR:&quot;+JSON.stringify(response));<br />
    }<br />
};</p>
<p>app.initialize();<br />
[/code]</p>
<li>
<h4>Create a MobileFirst Project and adapter</h4>
<p>For the RSS feed, it is necessary to create a MobileFirst adapter procedure that returns a JSON object containing a retrieved data.</p>
<ol>
<li>Change to a different folder (outside of the Cordova project) and create a MobileFirst back-end project by using the <code>mfp create MFPServer</code> command.
<p>This command creates a MobileFirst project inside the <code>MFPServer</code> folder.
</li>
<li>Navigate into the <code>MFPServer</code> folder and create the new HTTP adapter by runnin the <code>mfp add adapter RSSAdapter -t http</code> command. This command creates the RSS adapter inside the <code>MFPServer/adapters/RSSAdapter</code> folder. The HTTP adapter contains a sample procedure named <code>getStories</code> which retrieves data from the CNN RSS feed.
</li>
<li>Start the MobileFirst Server with the <code>mfp start</code> command. The new adapter is pushed to the server during the server initialization.
</li>
</ol>
<p>You can test the <code>getStories</code> procedure with the <code>mfp adapter call RSSAdapter/getStories</code> command.</p>
<p><strong>Note:</strong> For more details about HTTP adapters, see the <a href="../server-side-development-category/javascript-adapters/js-http-adapter/" target="_blank">JavaScript HTTP Adapter</a> tutorial.
</li>
<li>
<h4>Run the app</h4>
<ol>
<li>Navigate back to the application folder.</li>
<li>Register the Cordova application to the MobileFirst Server with the command <code>mfp push</code>.</li>
<li>Execute the application with the command <code>mfp cordova run</code>.</li>
<li>Follow the interactive instructions to select the device or emulator to run.</li>
</ol>
</li>
</ol>