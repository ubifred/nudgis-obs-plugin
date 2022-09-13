# Nudgis OBS Studio

## Description

The Nudgis OBS Studio plugin makes it easy to interface [Open Broadcaster Software](https://obsproject.com) with the [Nudgis platform from Ubicast](https://www.ubicast.eu).

The functionality of the plugin covers the following actions:
- performing live streams
- uploading recordings

The plugin is available for the following platforms:
- Windows 7/8/10/11 32/64 bits
- macOS (arm64 and x86)
- Linux: Ubuntu 64 bits and [Arch Linux](https://aur.archlinux.org/packages/nudgis-obs-plugin)  (Flatpack installation is also possible - see [Installation](#installation))

See the release notes for the minimal version of each OS

## Usage

Check out [our tutorial](https://help.ubicast.tv/permalink/v1263f480e913w8vr71t/iframe/).

<a target="_blank" title="Nudgis OBS Plugin Tutorial" href="https://help.ubicast.tv/permalink/v1263f480e913w8vr71t/iframe/"><img src="https://help.ubicast.tv/public/videos/v1263f48137336b4p4tr3zew63db9a/thumb_link.png" alt="Nudgis OBS Plugin Tutorial"/></a>

## Installation

OS-specific packages are available in the [releases github page](https://github.com/UbiCastTeam/nudgis-obs-plugin/releases). 

An [AUR package](https://aur.archlinux.org/packages/nudgis-obs-plugin) is available for Arch Linux.

### Windows

Check out [our tutorial](https://help.ubicast.tv/permalink/v1263f5564abdmnmj38p/iframe/).

<a target="_blank" title="Installing the OBS Nudgis plugin on Windows" href="https://help.ubicast.tv/permalink/v1263f5564abdmnmj38p/iframe/"><img src="https://help.ubicast.tv/public/videos/v1263f55698ddjr0tg91rzxa77tacn/thumb_link.png" alt="Installing the OBS Nudgis plugin on Windows"/></a>

Double click the .exe and follow the instructions. A "Windows protected your PC" popup will appear; click "More info" and confirm to allow installation; follow the wizard, and confirm you want to install the plugin into the same folder as OBS (important).

⚠️ We unfortunalty noticed that Microsoft Defender tag some version (it depends on the relaase and Windows Defender database) the installer as malware.

If this happens first check that this is indeed a false positive by uploader the file on on online virus analyzer (like https://www.virustotal.com or https://metadefender.opswat.com/), when you are confident that it is indeed a false positive you will have to tell Miscrosoft Defender to allow the execution of this file to avoid the following alert:

![Defender_alert](img/windows/window_alerte.png)

To allow the excution, open the Micorsoft Defender settings tab (type `defender` in the windows search bar) then look for the thead corresponding to the installer and double-check by clicking `details`

![Defender_alert](img/windows/MS_AV_detail.png)

Then go back and finally tick the `Allow on device` box:

![Defender_alert](img/windows/MS_AV_allow.png)

You can then follow the regular installation procedure

### macOS

Download the good .pkg package from the [releases github page](https://github.com/UbiCastTeam/nudgis-obs-plugin/releases).

The universal package can be installed on both x68 and arm64 machine.

After download follow this steps:

* open the Download folder, then `right click` on the file and choose `Open` or `double-click`

![Defender_alert](img/macos/macos_0.png)

* As the plugin is not sign you will have to confirm that you want to open it

![Defender_alert](img/macos/macos_1.png)

* Click `Continue` on the installer till the `Installation Type` step, at this step you *shall*  click `Change Install Location` and then choose `Install for me only`

![Defender_alert](img/macos/macos_3.png)
![Defender_alert](img/macos/macos_4.png)

* As the plugin is not sign you will have to confirm that you want to open it

![Defender_alert](img/macos/macos_1.png)

* If eveything went well you will see this

![Defender_alert](img/macos/macos_5.png)

⚠️ Depending on the level of securtiy you may also have to allow the installation of apps dowloaded for elsewhere than App store, this can be done by opening the `System Preferences` and tick the `App Store and identified developers` box in `Security and Privacy` tab:

![Defender_alert](img/macos/macos_security.png)

(you will also have to explicitly allow the app in this window)

### Linux

#### Ubuntu

Depending on the release version some minimal Ubuntu version is needed, chech the release note for details.

##### Install OBS

You may choose to install the latest version of OBS from project PPA:

```
sudo apt install software-properties-common
sudo add-apt-repository ppa:obsproject/obs-studio
sudo apt update
sudo apt install ffmpeg obs-studio
```

Or install the Ubuntu version

```
sudo apt install obs-studio
```

##### Install the corresponding Nudgis OBS Studio plugin

Check the relase note and download the .deb good package from the [releases github page](https://github.com/UbiCastTeam/nudgis-obs-plugin/releases).

```
sudo apt install ./nudgis-obs-plugin-1.0.0-Linux.deb
```

#### Flatpack

With flatpack you will get the latest version of OBS:

```
flatpack install com.obsproject.Studio
```

Then you shall install the `nugdis-obs-plugin` to the right place:

* create a tmp folder and extact the deb file inside:

```
mkdir /tmp/obs-nudgis-flatpack; cd /tmp/obs-nudgis-flatpack
dpkg-deb -x /path/to/nudgis-obs-plugin-1.0.0-Linux.deb .
```

* then copy the file to the right place

```
mkdir ~/.var/app/com.obsproject.Studio/config/obs-studio/plugins/nudgis-obs-plugin/{bin/64bit,data}
cp usr/lib/obs-plugins/nudgis-obs-plugin.so ~/.var/app/com.obsproject.Studio/config/obs-studio/plugins/nudgis-obs-plugin/bin/64bit
cp -r usr/share/obs/obs-plugins/nudgis-obs-plugin/locale ~/.var/app/com.obsproject.Studio/config/obs-studio/plugins/nudgis-obs-plugin/data
```

## Uninstallation

### Windows

The plugin can be uninstalled like any other installed software in the "Add or remove programs" menu.

### macOS

To remove this plugin open the terminal and type:

```
rm -rf "~/Library/Application Support/obs-studio/plugins/nudgis-obs-plugin.plugin/"
pkgutils --volume ~ --forget eu.ubicast.nudgis-obs-plugin
```

### Ubuntu

```
sudo apt remove nudgis-obs-plugin
```

## Development

### CI artifacts description

Deployment binaries are generated by the github/actions (Artifacts) CI, and are accessible from the [Actions section of the project repository](https://github.com/UbiCastTeam/nudgis-obs-plugin/actions).  

The file name of an Artifacts respects the following format:

\<name_of_plugin>\<platform>\_\<version_obs_compatible>_\<version_of_plugin>

For example
<pre>
nudgis-obs-plugin-linux-ubuntu-20.04-64_27.2.4_1.0.0
</pre>

Below is the listing of Artifact names, containing the deployment binaries for each platform for version 1.0.0 of the Nudgis OBS Studio plugin:

| Platform | Artifact Name                                        | Note                                                                                                                              |
| -------- | ---------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------- |
| Linux    | nudgis-obs-plugin-linux-ubuntu-20.04-64_27.2.4_1.0.0 | Ubuntu .deb package, may be used for other Linux platforms                                                                        |
| MacOS    | nudgis-obs-plugin-macos-x86_64_27.2.4_1.0.0          | Currently used for Intel and M1 platforms (OBS M1 version runs under [Rosetta](https://en.wikipedia.org/wiki/Rosetta_(software))) |
| MacOS    | nudgis-obs-plugin-macos-arm64_27.2.4_1.0.0           | Currently not used - in anticipation of native OBS versions M1                                                                    |
| Windows  | nudgis-obs-plugin-windows_27.2.4_1.0.0               | Universal 32/64 bits windows package                                                                                              |

### Setting up the development environment on Ubuntu 20.04

#### OBS compilation and installation in debug mode

Activation of deb-src repositories in /etc/apt/sources.list
<pre>
sudo perl -pi -0e 's/^(deb .*\n)# (deb-src)/$1$2/gm' /etc/apt/sources.list
sudo apt update
</pre>

Fetching sources, config
<pre>
sudo apt build-dep obs-studio
sudo apt install git wget libwayland-dev libxkbcommon-dev libxcb-composite0-dev libpci-dev qtbase5-private-dev
git clone https://github.com/obsproject/obs-studio.git
cd obs-studio
git checkout 27.2.4 -b 27.2.4
git submodule init
git submodule update
export CI_LINUX_CEF_VERSION=$(cat .github/workflows/main.yml | sed -En "s/[ ]+LINUX_CEF_BUILD_VERSION: '([0-9]+)'/\1/p")
wget https://cdn-fastly.obsproject.com/downloads/cef_binary_${CI_LINUX_CEF_VERSION}_linux64.tar.bz2
tar -xvaf cef_binary_${CI_LINUX_CEF_VERSION}_linux64.tar.bz2
cmake -B build . -DCMAKE_BUILD_TYPE=Debug -DENABLE_PIPEWIRE=FALSE -DCEF_ROOT_DIR=${PWD}/cef_binary_${CI_LINUX_CEF_VERSION}_linux64 -DCMAKE_CXX_FLAGS_DEBUG='-O0 -g3' -DCMAKE_C_FLAGS_DEBUG='-O0 -g3'
</pre>

Compiling and Installing
<pre>
cmake --build build
sudo cmake --install build
sudo ldconfig
</pre>

#### nudgis-obs-plugin compilation and installation in debug mode

<pre>
git clone git@github.com:UbiCastTeam/nudgis-obs-plugin.git
cd nudgis-obs-plugin
cmake -B build . -DCMAKE_BUILD_TYPE=Debug -DCMAKE_CXX_FLAGS_DEBUG='-O0 -g3' -DCMAKE_C_FLAGS_DEBUG='-O0 -g3'
cmake --build build
sudo cmake --install build
</pre>

#### Starting a GDB debug session

Installing gdb
<pre>
sudo apt install gdb
</pre>

Starting a debug session - with a breakpoint on the plugin initialization function
<pre>
gdb -ex 'set breakpoint pending on' -ex 'b src/nudgis-plugin.cpp:obs_module_load' -ex r obs
</pre>

Launching a debug session
<pre>
gdb obs
</pre>
