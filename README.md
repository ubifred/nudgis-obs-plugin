# Nudgis OBS Studio

## Description

The Nudgis OBS Studio plugin makes it easy to interface the OBS software (https://obsproject.com) with the Nudgis platform from Ubicast (https://www.ubicast.eu/fr/solutions/diffusion/ ).

The functionality of the plugin covers the following actions:
- performing a Live
- downloading a recording

The plugin is available for the following platforms:
- Windows 7/8/10/11 32/64 bits
- Mac OS
- Ubuntu 20.04 64 bits

## Installation

The plugin is available as a binary directly deployable on the desired platform.  
Deployment binaries are generated by the github/actions (Artifacts) CI.  
The deployment binaries are accessible from the **Actions** section of the project repository (https://github.com/UbiCastTeam/nudgis-obs-plugin/actions ).  
The **Actions** section references all the builds that have been performed.  
Selecting the latest build gives access to the listing of all available Artifacts.  
The file name of an Artifacts respects the following format:

\<name_of_plugin>\<platform>\_\<version_obs_compatible>_\<version_of_plugin>  
For example
<pre>
nudgis-obs-plugin-linux-ubuntu-20.04-64_27.2.4_1.0.0
</pre>

Below is the listing of Artifact names, containing the deployment binaries for each platform for version 1.0.0 of the Nudgis OBS Studio plugin:

| Platform | Artifact Name                                        | Note                                                                                                                              |
| -------- | ---------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------- |
| Linux    | nudgis-obs-plugin-linux-ubuntu-20.04-64_27.2.4_1.0.0 | installation package in .deb format                                                                                               |
| MacOS    | nudgis-obs-plugin-macos-x86_64_27.2.4_1.0.0          | Currently used for Intel and M1 platforms (OBS M1 version runs under [Rosetta](https://en.wikipedia.org/wiki/Rosetta_(software))) |
| MacOS    | nudgis-obs-plugin-macos-arm64_27.2.4_1.0.0           | Currently not used - in anticipation of native OBS versions M1                                                                    |
| Windows  | nudgis-obs-plugin-windows_27.2.4_1.0.0               |                                                                                                                                   |

### Sample Installation - Ubuntu-20.04

#### OBS Installation

<pre>
sudo apt install software-properties-common
sudo add-apt-repository ppa:obsproject/obs-studio
sudo apt update
sudo apt install ffmpeg obs-studio
</pre>

#### Installing the Nudgis OBS Studio plugin

Downloading the Artifact **nudgis-obs-plugin-linux-ubuntu-20.04-64_27.2.4_1.0.0** from the **Actions section** from the private repository https://github.com/UbiCastTeam in the current folder.

<pre>
unzip ./nudgis-obs-plugin-linux-ubuntu-20.04-64_27.2.4_1.0.0.zip
sudo apt install ./nudgis-obs-plugin-1.0.0-Linux.deb
</pre>


### Note concerning the installation on Mac OS

The installation script must be launched by carrying out a ```right click Open``` and ```click Open``` in order to authorize execution rights.

Following installation, an uninstallation script is available at the following URI:
<pre>
/Applications/OBS.app/Contents/Resources/data/obs-plugins/nudgis-obs-plugin/nudgis-obs-plugin-uninstall.command
</pre>

## Development environment deployment (Linux - ubuntu 20.04)

This paragraph describes the steps to perform to deploy the development environment in order to be able to compile a new version of the plugin and run it in debug mode in OBS.

### Recovery of OBS sources - compilation and installation in debug mode

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

### Retrieval of Nudgis OBS Studio plugin sources - compilation and installation in debug mode

<pre>
git clone git@github.com:UbiCastTeam/nudgis-obs-plugin.git
cd nudgis-obs-plugin
cmake -B build . -DCMAKE_BUILD_TYPE=Debug -DCMAKE_CXX_FLAGS_DEBUG='-O0 -g3' -DCMAKE_C_FLAGS_DEBUG='-O0 -g3'
cmake --build build
sudo cmake --install build
</pre>

### Starting a debug session gdb

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
