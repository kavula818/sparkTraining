<!DOCTYPE html><html lang="en"><head><meta charset="utf-8"><title>Firebolt SDK version 0.3</title><link rel="stylesheet" type="text/css" href="/plugins/gitiles/+static/base.css" /><link rel="stylesheet" type="text/css" href="/plugins/gitiles/+static/doc.css" /><link rel="stylesheet" type="text/css" href="/plugins/gitiles/+static/prettify/prettify.css" /></head><body class="Site"><header class="Site-header "><div class="Header"><div class="Header-title"></div></div></header><div class="Site-content Site-Content--markdown"><div class="Container"><div class="doc"><h1><a class="h" name="Firebolt-SDK-version-0_3" href="#Firebolt-SDK-version-0_3"><span></span></a>Firebolt SDK version 0.3</h1><ul><li><p><a href="#intro">Introduction</a></p></li><li><p><a href="#prerequisites">Prerequisites</a></p><ul><li><a href="#system-requirements">System Requirements</a></li><li><a href="#software-requirements">Software Requirements</a></li></ul></li><li><p><a href="#installation">Installation</a></p><ul><li><a href="#installation-of-rdk-image-on-raspberry-pi">Installation of RDK Image on Raspberry Pi</a></li><li><a href="#installation-of-rne-sdk">Installation of Firebolt SDK</a></li></ul></li><li><p><a href="#developing-applications">Developing applications</a></p><ul><li><a href="#troubleshooting">Troubleshooting</a></li><li><a href="#breakpad-support">Breakpad support</a></li><li><a href="#bluetooth-support">Bluetooth support</a></li><li><a href="#gdb-support">GDB Support</a></li><li><a href="#generating-corefiles">Generating Corefiles</a></li></ul></li><li><p><a href="#terminal-access">Terminal Access</a></p><ul><li><a href="#for-raspberry-pi">For Raspberry Pi</a></li><li><a href="#for-comcast-devices">For Comcast Devices</a></li></ul></li><li><p><a href="#installing-sample-applications">Installing Sample Applications</a></p><ul><li><a href="#preparing-USB">Preparing USB</a></li><li><a href="#running-sample-applications-raspberry-pi">Running Sample Applications on Raspberry Pi</a></li><li><a href="#running-sample-applications-comcast-devices">Running Sample Applications on Comcast Devices</a></li><li><a href="#app-manager-registry-file">App Manager Registry File</a></li><li><a href="#running-sample-applications-standalone-on-raspberry-pi">Running Sample Applications Standalone on Raspberry Pi</a></li><li><a href="#running-sample-applications-standalone-on-comcast-devices">Running Sample Applications Standalone on Comcast Devices</a></li></ul></li><li><p><a href="#using-the-app-manager">Using the App Manager</a></p><ul><li><a href="#app-manager-logging-raspberry-pi">App Manager Logging on Raspberry Pi</a></li><li><a href="#app-manager-logging-comcast-devices">App Manager Logging on Comcast Devices</a></li></ul></li><li><p><a href="#key-app-features">Key App Features</a></p><ul><li><a href="#graphics-with-wayland">Graphics With Wayland</a></li><li><a href="#keyboard-and-remote-input">Keyboard And Remote Input</a></li><li><a href="#handling-resolution-changes">Handling Resolution Changes</a></li><li><a href="#communication-with-app-manager">Communication With App Manager</a></li><li><a href="#suspend-and-resume">Suspend And Resume</a></li><li><a href="#audio-and-video-playback-with-gstreamer">Audio And Video Playback With Gstreamer</a></li></ul></li><li><p><a href="#sample-applications">Sample Applications</a></p><ul><li><a href="#graphics-sample">Graphics Sample</a></li><li><a href="#player-sample">Player Sample</a></li><li><a href="#lifecycle-sample">Lifecyle Sample</a></li><li><a href="#mse-player-sample">MSE Player Sample</a></li></ul></li></ul><p><a name="intro"></a></p><h2><a class="h" name="Introduction" href="#Introduction"><span></span></a>Introduction</h2><p>RDK Native Environment SDK (Firebolt) is intended to provide a development environment for applications targeted to run in RDK environment.</p><p><a name="prerequisites"></a></p><h2><a class="h" name="Prerequisites" href="#Prerequisites"><span></span></a>Prerequisites</h2><p><a name="system-requirements"></a></p><h3><a class="h" name="System-Requirements" href="#System-Requirements"><span></span></a>System Requirements</h3><p>Ubuntu 14.4 <strong>64 bit</strong> OS or higher 8GB of RAM</p><p><a name="software-requirements"></a></p><h3><a class="h" name="Software-Requirements" href="#Software-Requirements"><span></span></a>Software Requirements</h3><p>The following software packages needs to be installed</p><ul><li>awk</li><li>wget</li><li>git-core</li><li>diffstat</li><li>unzip</li><li>texinfo</li><li>gcc-multilib</li><li>build-essential</li><li>chrpath</li><li>socat</li><li>cpio</li><li>python</li><li>python3</li><li>python3-pip</li><li>python3-pexpect</li><li>xz-utils</li><li>debianutils</li><li>iputils-ping</li><li>libsdl1.2-dev</li><li>xterm</li></ul><p>This can be installed using the following command</p><pre class="code"> sudo apt-get install gawk wget git-core diffstat unzip texinfo gcc-multilib \
 build-essential chrpath socat cpio python python3 python3-pip python3-pexpect \
 xz-utils debianutils iputils-ping libsdl1.2-dev xterm
</pre><p><a name="installation"></a></p><h2><a class="h" name="Installation" href="#Installation"><span></span></a>Installation</h2><p><a name="installation-of-rdk-image-on-raspberry-pi"></a></p><h3><a class="h" name="Installation-of-RDK-Image-on-Raspberry-Pi" href="#Installation-of-RDK-Image-on-Raspberry-Pi"><span></span></a>Installation of RDK Image on Raspberry Pi</h3><p>Firebolt support the following Raspberry Pi models</p><ul><li>Raspberry Pi 3 Model B+</li><li>Raspberry Pi 3 Model A+</li><li>Raspberry Pi 3 Model B</li><li>Raspberry Pi 2 Model B</li><li>Raspberry Pi Zero W*</li></ul><p>*Raspberry Pi Zero W SDK/image is not compatible with other models in this version.</p><p>As part of Firebolt package you should receive a compressed rdk sdimg.xz to flash to the raspberry pi sdcard. Insert the raspberry pi sdcard into your desktop machine and flash the image using the following commands (<strong>This will overwrite anything on the sdcard</strong>).</p><blockquote><pre class="code">  sudo mkfs.ext3 /dev/sdX
  xzcat /path/to/image/*.rpi-sdimg.xz  | sudo dd of=/dev/sdX bs=4M
  sync 
</pre></blockquote><p>Replace <em>/path/to/image/</em>  with correct path to sdimg.xz.<br />Replace the <em>X</em> in <em>sdX</em> with the correct device letter of the sdcard when inserted into your machine.<br /><strong>Example:</strong></p><blockquote><pre class="code">  xzcat RPIMC_default_20181015101838sdy.rootfs.rpi-sdimg.xz  | sudo dd of=/dev/sdc bs=4M
</pre></blockquote><p>Once flashed insert the sdcard into the pi and make sure it has a valid ethernet and HDMI connection. Then power up the pi, it should boot up into the app manager screen with the ethernet IP listed at the bottom right.</p><p><a name="installation-of-rne-sdk"></a></p><h3><a class="h" name="Installation-of-Firebolt-SDK" href="#Installation-of-Firebolt-SDK"><span></span></a>Installation of Firebolt SDK</h3><p>To install the sdk, go the directory where it is copied, and run the following commands:</p><p>On Raspberry Pi:</p><blockquote><pre class="code"> chmod +x ./raspberrypi-rdk-mc-RNE-SDK-2.0.sh
 ./raspberrypi-rdk-mc-RNE-SDK-2.0.sh 
</pre></blockquote><p>On Comcast Devices:</p><blockquote><pre class="code"> chmod +x ./DEVICE-RNE-SDK-2.0.sh
 ./DEVICE-RNE-SDK-2.0.sh 
</pre></blockquote><p>Replace DEVICE with your particular device: e.g. (pacexi5, pacexi5-RNE-SDK-2.0.sh)</p><p>Follow the instructions in the screen regarding installation directory. If you don&lsquo;t want to change the default directory, please press <em>ENTER</em> and proceed. It&rsquo;s easiest to run the above script in an empty directory and type . to install in the current directory.</p><p><a name="developing-applications"></a></p><h2><a class="h" name="Developing-applications" href="#Developing-applications"><span></span></a>Developing applications</h2><p>Assuming that the SDK is installed in <em>sdk_root</em> directory, issue the following command</p><blockquote><pre class="code"> source  &lt;sdk_root&gt;/environment-setup-&lt;chipset&gt;-rdk-linux-gnueabi
</pre></blockquote><p><strong>Example:</strong></p><blockquote><pre class="code"> source RNE-3.0/environment-setup-cortexa7t2hf-vfp-vfpv4-neon-rdk-linux-gnueabi
</pre></blockquote><p>Here RNE-3.0 is sdk_root directory</p><p>Now all the cross compiler tools are available for development. Four native sample applications are provided as part of build. To build the samples, go to the samples directory and execute the following command</p><blockquote><pre class="code"> ./build_samples.sh
</pre></blockquote><p>After the samples are built they are contained in a partnerapps directory for copying to the provided device.</p><p><a name="breakpad-support"></a></p><h3><a class="h" name="Breadpad-support" href="#Breadpad-support"><span></span></a>Breadpad support</h3><p>Google breakpad support is available for the applications. For more information about Google breakpad and it&#39;s integration, check this link <a href="https://chromium.googlesource.com/breakpad/breakpad/+/master/docs/linux_starter_guide.md">https://chromium.googlesource.com/breakpad/breakpad/+/master/docs/linux_starter_guide.md</a> The static library is added as part of SDK.</p><p>The rne player application, included as part of this, has breakpad support.</p><p><a name="bluetooth-support"></a></p><h3><a class="h" name="Bluetooth-support" href="#Bluetooth-support"><span></span></a>Bluetooth support</h3><p>This version supports bluez version 5.45. The support is limited to Human Interface Devices (HID) in this version.</p><p><a name="troubleshooting"></a></p><h3><a class="h" name="Troubleshooting" href="#Troubleshooting"><span></span></a>Troubleshooting</h3><p>If a shared library has secondary dependencies which it cannot resolve, the following linker flags should be added to tell the linker to ignore its undefined symbols -Wl, --allow-shlib-undefined</p><p><a name="gdb-support"></a></p><h3><a class="h" name="GDB-Support" href="#GDB-Support"><span></span></a>GDB Support</h3><p>Currently GDB is not shipped with the firemware/SDK.  It can be built with the sdk and copied to the device. Shell/SSH access is necessary to use it.</p><ol><li>Download the source for gdb.</li><li>Make sure you are in a shell setup for Firebolt Development</li><li>Create a directory for installing gdb</li></ol><blockquote><pre class="code"> mkdir gdb_install
</pre></blockquote><ol start="4"><li>Enter the directory of the downloaded gdb source, CONFIGURE_FLAGS is already set in a Firebolt shell for cross compiling needs</li></ol><blockquote><pre class="code"> cd gdb-x.x
 ./configure $CONFIGURE_FLAGS --prefix=/path/to/gdb_install
 make
 make install
</pre></blockquote><ol start="5"><li>At the root of your usb key, create a usr directory</li></ol><blockquote><pre class="code"> cd /path_to_root_of_usb_key
 mkdir usr
</pre></blockquote><ol start="6"><li>Copy contents of gdb_install directory into usr on your usb key</li></ol><blockquote><pre class="code"> cp -r gdb_install/*  /path_to_root_of_usb_key/usr/
</pre></blockquote><ol start="7"><li>Insert usb key into device</li><li>Edit run_partner_app.sh script with the following:</li></ol><blockquote><pre class="code">  export LD_LIBRARY_PATH=/usb/usr/lib
</pre></blockquote><pre class="code">Add the above to the script so gdb libs can be found

Change the launch line to prefix with the path to gdb on the key
</pre><blockquote><pre class="code">  /usb/usr/bin/gdb /usb/partnerapps/rne-triangle/rne_triangle
</pre></blockquote><p>This launch script provided with the Firebolt SDK can be modified to launch any binary built with and without gdb.  The launch script should be at the root of the partnerapps folder.</p><p><strong>Caveat</strong></p><p>Somtimes compiled library dependencies can exist in the Firebolt sdk but not on the firmware.  For example when running GDB it may say its missing libncursesw.so.5.  This can be resolved by copying the needed Firebolt SDK library onto our new lib directory on the key:</p><blockquote><pre class="code">cp /path_to_sdk/sysroots/cortexa15t2hf-neon-rdk-linux-gnueabi/lib/libncurses.so.5 /path_to_root_of_usb_key/usr/lib/
</pre></blockquote><p><a name="generating-corefiles"></a></p><h3><a class="h" name="Generating-Corefiles" href="#Generating-Corefiles"><span></span></a>Generating Corefiles</h3><p>By default on many Comcast devices core dump support is turned off for space reasons.  We can override this though, for Firebolt development purposes. Shell/SSH access is necessary for this.</p><ol><li>Insert the usb key into the device</li><li>Create a cores directory on the key</li></ol><blockquote><pre class="code">  cd /usb
  mkdir cores
</pre></blockquote><ol start="3"><li>Enable coredumps</li></ol><blockquote><pre class="code">  ulimit -c unlimited
</pre></blockquote><ol start="4"><li>Change /proc/sys/kernel/ to write cores to the usb key</li></ol><blockquote><pre class="code">  echo &quot;/usb/cores/%e_%s_%t&quot; &gt; /proc/sys/kernel/core_pattern
</pre></blockquote><p>Corefiles can then be evaluated on the device by using gdb built for the device or can be evaulated using a gdb built on/for the ubuntu desktop with multiarch support.</p><p><a name="terminal-access"></a></p><h2><a class="h" name="Terminal-Access" href="#Terminal-Access"><span></span></a>Terminal Access</h2><p><a name="for-raspberry-pi"></a></p><h3><a class="h" name="For-Raspberry-Pi" href="#For-Raspberry-Pi"><span></span></a>For Raspberry Pi</h3><p>Once the pi is booted into the app manager and the pi has a valid ethernet connection the app manager will list the device&#39;s ethernet ip on the bottom right. This can be used to ssh into the box from a machine on the same network.  Login is root, password is empty.</p><p>Example:</p><blockquote><pre class="code"> ssh root@192.168.0.103
</pre></blockquote><p>Then press enter twice to get ssh terminal access to the box.</p><p><a name="for-comcast-devices"></a></p><h3><a class="h" name="For-Comcast-Devices" href="#For-Comcast-Devices"><span></span></a>For Comcast Devices</h3><p>SSH access instructions will be provided to you.</p><p><a name="installing-sample-applications"></a></p><h2><a class="h" name="Installing-Sample-Applications" href="#Installing-Sample-Applications"><span></span></a>Installing Sample Applications</h2><p>The following sections will detail how to load and run the provided sample applications on the provided device.</p><p><a name="preparing-USB"></a></p><h3><a class="h" name="Preparing-USB" href="#Preparing-USB"><span></span></a>Preparing USB</h3><p>As of this release, USB storage device should have <strong>single partition and ext3 format</strong>. To format USB in ext3</p><p><strong>Below assumes usb device is on device sdb</strong></p><ul><li>Unmount USB drive</li></ul><blockquote><pre class="code"> sudo umount /dev/sdb
</pre></blockquote><ul><li>Format USB drive in ext3 format</li></ul><blockquote><pre class="code"> sudo mkfs.ext3 /dev/sdb
</pre></blockquote><p><a name="running-sample-applications-raspberry-pi"></a></p><h3><a class="h" name="Running-Sample-Applications-on-Raspberry-Pi" href="#Running-Sample-Applications-on-Raspberry-Pi"><span></span></a>Running Sample Applications on Raspberry Pi</h3><p>Once the sample applications are built with the provided sdk a partnerapps folder will be created at the root of the samples directory. You can then place this directory at the root of the USB storage device and then insert the USB stick into the pi. Once inserted, use a USB keyboard and press ctrl-e to reload the app manager. You will now see all the sample apps in the list.</p><p>You can also have the app manager launch your own binary by renaming the binary <em>partnerapp</em> and placing it in the partnerapps folder at the root of the USB storage device.</p><p><a name="running-sample-applications-comcast-devices"></a></p><h3><a class="h" name="Running-Sample-Applications-on-Comcast-Devices" href="#Running-Sample-Applications-on-Comcast-Devices"><span></span></a>Running Sample Applications on Comcast Devices</h3><p>Once the sample applications are built with the provided sdk a partnerapps folder will be created at the root of the samples directory. You can then place this directory at the root of the USB storage device and then insert the USB stick into the comcast device.</p><p>If provided ssh access:</p><ol><li>SSH into the comcast device</li><li>Mount the usb key to /usb</li></ol><blockquote><pre class="code">mount /dev/sda /usb
</pre></blockquote><p>Once inserted, use a USB keyboard and press ctrl-e to reload the app manager. You will now see all the sample apps in the list.</p><p>You can also have the app manager launch your own binary by renaming the binary <em>partnerapp</em> and placing it in the  partnerapps folder at the root of the USB storage device.</p><p><a name="app-manager-registry-file"></a></p><h3><a class="h" name="App-Manager-Registry-File" href="#App-Manager-Registry-File"><span></span></a>App Manager Registry File</h3><p>The appmanagerregistry.conf is a simple json file that the app manager reads to find the apps it can launch. This file is contained at the root of the partnerapps directory on the USB storage device. It can easily be modified to launch and interact with new partner applications.</p><p><a name="running-sample-applications-standalone-on-raspberry-pi"></a></p><h3><a class="h" name="Running-Sample-Applications-Standalone-on-Raspberry-Pi" href="#Running-Sample-Applications-Standalone-on-Raspberry-Pi"><span></span></a>Running Sample Applications Standalone on Raspberry Pi</h3><p>For debugging purposes you can run your applications standalone without the app manager Once sshed into the raspberry pi do the following:</p><ul><li>Shutdown the app manager</li></ul><blockquote><pre class="code"> systemctl stop appmanager
</pre></blockquote><ul><li>Start the westeros service (Needed for graphics to be displayed)</li></ul><blockquote><pre class="code"> systemctl start westeros
</pre></blockquote><ul><li>Run the provided run_partner_app.sh script provided in the partnerapps folder</li></ul><blockquote><pre class="code"> /usb/partnerapps/run_partner_app.sh
</pre></blockquote><p>By default the the above shell script runs the rne_triangle sample app.  But it can easily be modified to run any app of your choosing by editing the last line in the script.</p><p>To use the app manager again, just start its service back up.</p><blockquote><pre class="code"> systemctl start appmanager
</pre></blockquote><p><a name="running-sample-applications-standalone-on-comcast-devices"></a></p><h3><a class="h" name="Running-Sample-Applications-Standalone-on-Comcast-Devices" href="#Running-Sample-Applications-Standalone-on-Comcast-Devices"><span></span></a>Running Sample Applications Standalone on Comcast Devices</h3><p>For debugging purposes you can run your applications standalone without the app manager provided you have ssh access into the comcast device. Once sshed into the comcast device do the following:</p><ul><li>Shutdown the app manager</li></ul><blockquote><pre class="code"> systemctl stop xre-receiver
</pre></blockquote><ul><li>Start westeros (Needed for graphics to be displayed, this only needs to be run one time)</li></ul><blockquote><pre class="code"> /usb/partnerapps/run_westeros.sh
</pre></blockquote><ul><li>Run the provided run_partner_app.sh script provided in the partnerapps folder</li></ul><blockquote><pre class="code"> /usb/partnerapps/run_partner_app.sh
</pre></blockquote><p>By default the the above shell script runs the rne_triangle sample app.  But it can easily be modified to run any app of your choosing by editing the last line in the script.</p><p>To use the app manager again, just start its service back up.</p><blockquote><pre class="code"> systemctl start xre-receiver
</pre></blockquote><p><a name="using-the-app-manager"></a></p><h2><a class="h" name="Using-the-App-Manager" href="#Using-the-App-Manager"><span></span></a>Using the App Manager</h2><p>A USB keyboard or remote control (on supported systems) can be used on the device to interact with the app manager.</p><p>The following actions are supported:</p><ul><li>Pressing the up and down keyboard arrow keys (or remote arrows)  moves between the apps</li><li>Pressing Enter (or OK button remote)  will launch or switch to a selected app.</li><li>Pressing left or right arrow keys (or remote arrows)  will select one of three options (Launch/Suspend/Stop)<br />-- Launch will launch the selected application, if an app is already launched it will be switched to.<br />-- Suspend will put an application in suspend state if it supports it (Graphics Lifecycle and MSE sample player support suspend/resume)<br />-- If an app is suspended this option will become Resume, which when pressed will resume the application.</li><li>When an application is taking up the whole screen Pressing Ctrl-m (or remote xfinity key)  will bring you back to the app manager.</li><li>To reload the app manager (if the contents of the usb key were changed) press Ctrl-e (or Exit key on the remote).</li></ul><p><a name="app-manager-logging-raspberry-pi"></a></p><h3><a class="h" name="App-Manager-Logging-On-The-Raspberry-Pi" href="#App-Manager-Logging-On-The-Raspberry-Pi"><span></span></a>App Manager Logging On The Raspberry Pi</h3><p>The app manager application will log all its output to /opt/logs/appmanager.log.</p><p>All partner applications that are launched from the app manager will have their stdout/stderr also redirected to this file.</p><p><a name="app-manager-logging-comcast-devices"></a></p><h3><a class="h" name="App-Manager-Logging-On-Comcast-Devices" href="#App-Manager-Logging-On-Comcast-Devices"><span></span></a>App Manager Logging On Comcast Devices</h3><p>The app manager application will log all its output to /opt/logs/receiver.log.</p><p>All partner applications that are launched from the app manager will have their stdout/stderr also redirected to this file.</p><p><a name="key-app-features"></a></p><h2><a class="h" name="Key-App-Features" href="#Key-App-Features"><span></span></a>Key App Features</h2><p><a name="graphics-with-wayland"></a></p><h3><a class="h" name="Graphics-With-Wayland" href="#Graphics-With-Wayland"><span></span></a>Graphics With Wayland</h3><p>The app manager has the job of running a wayland compositor for all the apps it runs.  Before painting to the screen apps will connect to this compositor using wayland calls.</p><p>The following is a general graphics setup flow.</p><pre class="code">// Connect to compositor
display= wl_display_connect(display_name);  // A NULL display name connects to default WAYLAND_DISPLAY set by app manager

// Use the registry as the hook to connect to the rest of the wayland callbacks
registry= wl_display_get_registry(display); 
wl_registry_add_listener(registry, &amp;registryListener, &amp;ctx);

// Complete communication to compositor for above commands
wl_display_roundtrip(display);

// Setup EGL

// Use the the wayland display to get the egl display
ctx-&gt;eglDisplay = eglGetDisplay((NativeDisplayType)display);
// Continue setting up EGL...

// Create a surface with the compositor
// Get compositor reference from wayland registry callback
// Create surface
ctx-&gt;surface= wl_compositor_create_surface(ctx-&gt;compositor);

// Create egl window from surface
ctx-&gt;native= wl_egl_window_create(ctx-&gt;surface, ctx-&gt;planeWidth, ctx-&gt;planeHeight);

// Continue setting up surface with normal egl calls..

// Do Open GL setup for your app

// Run graphics app loop
while (shouldRunMainLoop)
{
  // dispatch queued wayland events on default queue, can also use blocking method wl_display_dispatch
  wl_display_dispatch_pending(display)

  // render your gl scene

  // swap buffers
  eglSwapBuffers(eglDisplay, eglSurfaceWindow);
}
</pre><p><a name="keyboard-and-remote-input"></a></p><h3><a class="h" name="Keyboard-And-Remote-Input" href="#Keyboard-And-Remote-Input"><span></span></a>Keyboard And Remote Input</h3><p>All keyboard and remote control (for supported systems) for a native app is handled through the standard wayland seat mechanism. Remote control keys will come in as a standard wayland keyboard seat.  The app manager compositor will route input to the focused app.</p><p>The following is a general way of getting keys</p><pre class="code">// Connect to display and registry callback with wayland registry
display= wl_display_connect(display_name);
registry= wl_display_get_registry(display);
wl_registry_add_listener(registry, &amp;registryListener, &amp;ctx);

// In registry callback add a seat listener
seat= (struct wl_seat*)wl_registry_bind(registry, id, &amp;wl_seat_interface, 4);
wl_seat_add_listener(seat, &amp;seatListener, ctx);

// In seat listener add listener for keyboard
keyboard= wl_seat_get_keyboard( seat );
wl_keyboard_add_listener( keyboard, &amp;keyboardListener, ctx );

// Use the keyboard listener callbacks to get key information:
static const struct wl_keyboard_listener keyboardListener = {
  keyboardHandleKeymap,
  keyboardHandleEnter,
  keyboardHandleLeave,
  keyboardHandleKey,
  keyboardHandleModifiers,
  keyboardHandleRepeatInfo,
};
</pre><p><a name="handling-resolution-changes"></a></p><h3><a class="h" name="Handling-Resolution-Changes" href="#Handling-Resolution-Changes"><span></span></a>Handling Resolution Changes</h3><p>Resolution changes can be handled through the wayland output mechanism. Add a listener on wl_output and then a callback for outputHandleMode. The outputHandleMode callback will be called with resolution changes. This will also be called once first registered to get initial output resolution.</p><pre class="code">// Connect to display and registry callback with wayland registry
display= wl_display_connect(display_name);
registry= wl_display_get_registry(display);
wl_registry_add_listener(registry, &amp;registryListener, &amp;ctx);

// In registry callback add an output listener
output= (struct wl_output*)wl_registry_bind(registry, id, &amp;wl_output_interface, 2);
wl_output_add_listener(output, &amp;outputListener, ctx);

// Make sure your outputListener contains an outputMode callback
static const struct wl_output_listener outputListener = {
   outputGeometry,
   outputMode,
   outputDone,
   outputScale
};

//output mode will get passed in a width and height
static void outputMode( void *data, struct wl_output *output, uint32_t flags,
                        int32_t width, int32_t height, int32_t refresh )
{
}
</pre><p><a name="communication-with-app-manager"></a></p><h3><a class="h" name="Communication-With-App-Manager" href="#Communication-With-App-Manager"><span></span></a>Communication With App Manager</h3><p>Apps will communicate with the app manager through the interprocess communication library rt. rt enables the app manager to call functions in your application and for your application to send events and status to the app manager.</p><p>Using rt:</p><pre class="code">// Your object to be registered must inherit the rtObject interface
// Here you will declare your object and define functions.
class MyObject : public rtObject {
 public:
  rtDeclareObject(MyObject, rtObject);
  rtMethodNoArgAndNoReturn(&quot;suspend&quot;, suspend);
  rtMethodNoArgAndNoReturn(&quot;resume&quot;, resume);

// You then need to initialize rt and register your object.
rtError rc = rtRemoteInit();
const char* objectName = &quot;MY OBJECT&quot;;
MyObject* myObject = new MyObject;
rc = rtRemoteRegisterObject(objectName, myObject);

// Then for rt processing to work you must call its process
// iteration in your apps main loop.

// This will register a callback that will get called everytime there is rt messages
// to be processed
rtRemoteRegisterQueueReadyHandler( rtEnvironmentGetGlobal(), rtRemoteCallback, nullptr );

// You then must call rtRemoteProcessSingleItem() to process the message. You can do
// this as part of your apps main loop or use a thread and wait on a condition.
</pre><p><a name="suspend-and-resume"></a></p><h3><a class="h" name="Suspend-And-Resume" href="#Suspend-And-Resume"><span></span></a>Suspend And Resume</h3><p>Apps should support a suspend and resume option if needed so they can start quickly and stay running in the background.  Apps when suspended should free all graphics and AV resources while using minimal CPU and RAM while running in the background. When the app is resumed it should be usable by the user in a few seconds.</p><p>The app manager is ready to call suspend/resume on your app through rt. You will need to initialize and register an object to rt that contains these functions.</p><pre class="code">// Your object to be registered must inherit the rtObject interface
// Here you will declare your object and define functions.
// Header file:
class MyObject : public rtObject {
 public:
  rtDeclareObject(MyObject, rtObject);
  rtMethodNoArgAndNoReturn(&quot;suspend&quot;, suspend); //declare suspend function to rt
  rtMethodNoArgAndNoReturn(&quot;resume&quot;, resume); //declare resume function to rt

  rtError suspend(); //actual suspend c++ function
  rtError resume(); //acutal resume c++ function

//CPP file:
// Define rt object and methods
rtDefineObject (MyObject, rtObject);
rtDefineMethod (MyObject, suspend);
rtDefineMethod (MyObject, resume);

// Implement suspend/resume c++ functions
rtError MyObject::suspend()
{
  // suspend your app from active state
}

rtError MyObject::resume()
{
  // resume your app from suspend state
}
</pre><p><a name="audio-and-video-playback-with-gstreamer"></a></p><h3><a class="h" name="Audio-And-Video-Playback-With-Gstreamer" href="#Audio-And-Video-Playback-With-Gstreamer"><span></span></a>Audio And Video Playback With Gstreamer</h3><p>How your app generally uses gstreamer is up to you.  Ideally your app will be able to use a playbin pipeline. The only requirement is that your app must use gstreamer for its audio and video needs and that it use the westerossink for its videosink.  westerossink allows your video path to go through wayland so it can be manipulated by the application manager if necessary.  A simple gstreamer use case is showcased in the rne-player sample app and a more real world MSE type AV player is showcased in the mse-player sample application.</p><p><a name="sample-applications"></a></p><h2><a class="h" name="Sample-Applications" href="#Sample-Applications"><span></span></a>Sample Applications</h2><p>The provided sample apps are to help developers get up to speed with using the graphics and video APIs in Firebolt. Generally all graphics and keyboard/remote input will be provided through wayland, and audio and video will use gstreamer.</p><p><a name="graphics-sample"></a></p><h3><a class="h" name="Graphics-Sample" href="#Graphics-Sample"><span></span></a>Graphics Sample</h3><p>rne-triangle sample app demonstrates a simple graphics app that uses opengl es and wayland to render a spinning triangle to the screen. The following key features are demostrated:</p><ol><li>How to use wayland and OpenGL ES to render graphics</li><li>How to get keyboard/remote input</li><li>How to get screen resolution</li></ol><p><a name="player-sample"></a></p><h3><a class="h" name="Player-Sample" href="#Player-Sample"><span></span></a>Player Sample</h3><p>rne-player sample app shows how to build and use a simple gstreamer pipeline that uses westerosink.  It will load a movie from a URL, buffer it, and play it back. The following key features are demonstrated:</p><ol><li>How to build a simple gstreamer pipeline with westerossink</li><li>How to get screen resolution</li></ol><p><a name="lifecycle-sample"></a></p><h3><a class="h" name="Lifecycle-Sample" href="#Lifecycle-Sample"><span></span></a>Lifecycle Sample</h3><p>graphics-lifecycle sample app extends the rne-triangle sample app to support rt and suspend/resume. The following key features are demonstrated:</p><ol><li>How to use wayland and OpenGL ES to render graphics</li><li>How to get keyboard/remote input</li><li>How to get screen resolution</li><li>How to setup and register an object with rt</li><li>How to handle suspend/resume</li></ol><p><a name="mse-player-sample"></a></p><h3><a class="h" name="MSE-Player-Sample" href="#MSE-Player-Sample"><span></span></a>MSE Player Sample</h3><p>The MSE (Media Source Extensions) player sample app demos how to put everything together for a more real world example. The app will show how to build a gstreamer pipeline that can be fed raw H264 and AAC frames asynchronously. The sample content contains three separate fragments of the same video to show how to simulate a seek by flushing the video pipeline and providing new samples at different period in time.  The app also uses the essos library which simplifies setting up wayland for graphics and keyboard/remote input.</p><p>The following key features are demonstrated:</p><ol><li>How to setup and use a more complicated gstreamer pipeline with a custom source</li><li>How to setup and register an object with rt</li><li>How to handle suspend/resume</li></ol></div></div></div><footer class="Site-footer"><div class="Footer"><div class="Footer-poweredBy">Powered by <a href="https://gerrit.googlesource.com/gitiles/">Gitiles</a></div><div class="Footer-links"><a class="Footer-link" href="/plugins/gitiles/rdk/components/generic/rne/generic/+show/refs/changes/01/273801/1/docs/README.md">source</a><a class="Footer-link" href="/plugins/gitiles/rdk/components/generic/rne/generic/+log/refs/changes/01/273801/1/docs/README.md">log</a><a class="Footer-link" href="/plugins/gitiles/rdk/components/generic/rne/generic/+blame/refs/changes/01/273801/1/docs/README.md">blame</a></ul></div></footer></body></html>