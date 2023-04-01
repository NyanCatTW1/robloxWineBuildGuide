# Note To Pop!_OS/Kali Linux users  
## Please notice that the distro you are using is not capable of building Wine, due to many conflicts in 32/64 bit packages.
## You must change distro in order to build Wine.
Also, don't use Kali Linux as your main distro, especially not with the default password.  
If you're using other distros, just ignore this section and read below.  

<br>

# The Ultimate Roblox on Linux Guide
This is a guide on building wine-tkg-git for Roblox as well as a couple of workarounds for issues, originally by `Nyan cat#8349`.

It includes the following patches and improvements:
 - Right-click mouse fix (by applying a patch)
 - Black cursor studio bug (by reverting the commit that caused it)

This guide is rapidly changing, so please pay attention to the date at which it was updated. If it was updated while you were following it, start over.


**In order to start this guide**, jump over to the [steps to compile](#steps-to-compile) section if you want to install Wine and Roblox.

Alternatively, you can hop over to the [video guide](#video-guide) section in case you prefer to follow a video guide (although compilation is recommended).

**In case you run into any issues while compiling**, you can hop over to the [common compilation errors](#common-compilation-errors) section.

**If you run into any problems while trying to actually play the game** or use Wine in general, take a look at the [common errors or issues](#common-errors-or-issues) section.

<br>

# Notice to video guide creators
If you are creating a video guide (YouTube, etc.) please attach a link to this guide in the pinned comments, as well as the description.

Mention of the Discord tag is optional but preferred.

If you are telling people to download a precompiled version of Wine in your guide, please mention it as such.

<br>

# Video guide
Here's a video guide on YouTube. Do note that it tells you to download a precompiled version of Wine, which may contain malware or behave unexpectedly:

[YouTube](https://www.youtube.com/watch?v=xQHBPXsorxU)

[CloudTube](https://tube.cadence.moe/watch?v=xQHBPXsorxU)

<br>

# Getting in touch
You can get in touch on the Grapejuice Discord server: https://discord.gg/mRTzEb6

Make sure to follow the rules and ask your question in one of the help channels. Do not post your question in multiple channels.

<br>

# Steps to compile  
<details open>
<summary>Click to fold/unfold</summary>

## Note to Arch Linux users
 **"it is not really the most up to date" -Package Maintainer**
 
[wine-tkg-roblox](https://aur.archlinux.org/packages/wine-tkg-roblox)<sup>AUR</sup> applies the patches automatically and builds wine.
1. **Clone the wine-tkg-roblox git repository**:
`git clone https://aur.archlinux.org/wine-tkg-roblox.git`
2. **Enter the just cloned directory**:
`cd wine-tkg-roblox`
3. **Install the patched wine**:
`makepkg -si`
 
**Or install the [wine-tkg-roblox](https://aur.archlinux.org/packages/wine-tkg-roblox)<sup>AUR</sup> using your preferred AUR package manager**
 
## If you are not using Arch Linux or are not using the AUR package, follow the guide below
1. **Clone the wine-tkg-git repository**:  
`git clone https://github.com/Frogging-Family/wine-tkg-git.git`  
2. **Enter the just cloned directory**:  
`cd wine-tkg-git`  
3. **Download the patch file**:  
`curl https://raw.githubusercontent.com/NyanCatTW1/robloxWineBuildGuide/main/roblox-wine-staging-v2.5.patch --output roblox-wine-staging-v2.5.patch`  
4. **Apply the patch**:  
`git apply roblox-wine-staging-v2.5.patch`  
5. **Change to the source folder**:  
`cd wine-tkg-git`  
6. **Edit `customization.cfg` to fit your needs (optional)**
7. **Install dependencies**:
   - **If you are on Arch Linux, skip this step**
   - **If you are on Debian/Debian-based (Ubuntu, etc)**: change `_nomakepkg_dep_resolution_distro=""` to `_nomakepkg_dep_resolution_distro="debuntu"` in `customization.cfg`. Then, run `sudo dpkg --add-architecture i386 && sudo apt update && sudo apt upgrade && sudo apt install autoconf libxi-dev libvulkan-dev`
   - **If you are on Fedora-based**: change `_nomakepkg_dep_resolution_distro=""` to `_nomakepkg_dep_resolution_distro="fedora"` in `customization.cfg`
   - **If you are on Solus-based**: Use the following two commands to install everything you need:  
 <details>
  <summary>Show/hide the commands</summary>
  
64 bit dependencies  
`sudo eopkg install mingw-w64-gcc alsa-lib-devel pulseaudio-devel dbus-devel fontconfig-devel freetype2-devel libgnutls-devel libnotify-devel  libjpeg-turbo-devel libpng-devel libtiff-devel mesalib-devel gst-plugins-good libxml2-devel libxmu-devel libxslt-devel faudio-devel gstreamer-1.0-devel faudio gstreamer-1.0-plugins-base-devel ccache libx11-devel libxi-devel ldb-devel sdl2-devel vulkan ocl-icd-devel`  
32 bit dependencies  
`sudo eopkg install mingw-w64-gcc-32bit alsa-lib-32bit-devel pulseaudio-32bit-devel dbus-32bit-devel fontconfig-32bit-devel freetype2-32bit-devel libgnutls-32bit-devel libnotify-32bit-devel libjpeg-turbo-32bit-devel libpng-32bit-devel libtiff-32bit-devel mesalib-devel libxml2-32bit-devel libxmu-32bit-devel libxslt-32bit-devel faudio-32bit-devel  gstreamer-1.0-32bit-devel faudio-32bit gstreamer-1.0-plugins-base-32bit-devel libx11-32bit-devel libxi-32bit-devel unixodbc-32bit-devel unixodbc-32bit-devel unixodbc-32bit-devel libpcap-32bit-devel glibc-32bit-devel sdl2-32bit-devel libgcrypt-32bit-devel vulkan-32bit ocl-icd-32bit-devel libusb-32bit-devel`  
 
 </details>  
 
   - **If none of the above describes your distro**: You need to install the dependencies yourself. A list of them are at https://wiki.winehq.org/Building_Wine#Satisfying_Build_Dependencies, **You need the `Needed for many applications` ones as well.**  
 Make sure to check the [common compilation errors](#common-compilation-errors) section in case you hit any weird issues.  
   - **Tip**: You can install `ccache` on any distro mentioned above to speed up the 2nd time you compile by as much as 6 times.
8. **Compile**:
   - **If you are on Arch Linux**: `makepkg -si`
   - **If you are on another distro** (Debian, Fedora): `./non-makepkg-build.sh`
   - **If the script complains** `No _LOCAL_PRESET set in .cfg. Please select your desired base (or hit enter for default) :` Choose 0 (default-tkg) or simply press enter.
   - **If you encounter any issues**, errors or low performance, please look if they are mentioned in this guide. You can use `CTRL + F` in your browser to search for any errors mentioned here.
   - [Get in touch](#getting-in-touch) if you have any further questions!
9. **Getting the Wine path**
   - **If you are on Arch Linux**: ignore this step
   - **If you are on other distros**:
      - `cd non-makepkg-builds` (If this command failed, the build probably failed too.)
      - `ls`
      - Look for a folder that looks something like: `wine-tkg-staging-fsync-git-6.14.r7.g05c42b1d`
      - Run `realpath <name of the folder here>` to get the full path to the folder, which we will later use in Grapejuice.
10. **Installing Grapejuice**:
   - Go to [this link](https://brinkervii.gitlab.io/grapejuice/docs/) and follow the instructions specific to your distribution.
11. **Configuring Grapejuice to use Wine**:
   - **If you are on Arch Linux**: Make sure you uninstall Wine that came with the distro, **you should also set `wine_home` to `"/usr"` according to the steps below.** In case the `wine` command is not found, repeat Step 8.
   - **If you are on other distros**:
      - Open `~/.config/brinkervii/grapejuice/user_settings.json` in your text editor.
      - Set **every** `wine_home` fields to the path you found in step 9. (There are multiple of them!)
12. **Try it out**:
   - Press the Play button on any game on roblox.com
   - **If you encounter any issues**, errors or low performance, please look if they are mentioned in this guide. You can use `CTRL + F` in your browser to search for any errors mentioned here.
   - [Get in touch](#getting-in-touch) if you have any further questions!
</details>
<br>

# Installing DXVK (DirectX over Vulkan)
<details open>
<summary>Click to fold/unfold</summary>
<br>

### DirectX over Vulkan (**DXVK**) is a translation layer for Direct3D 9/10/11 which converts Direct3D API Calls over to native Vulkan using Wine.
### DXVK greatly improves game 3D performance. Installation is quick and simple, resulting in **amazing** performance.
### Follow the instructions below to install DXVK in your Grapejuice wine prefix.  
### (As it work better than DXVK on *some* devices, you should also try the Vulkan renderer, which can be done by skipping to step 4 **once you've done step 1**.)
<br>

1. **Verify Vulkan is installed. [Skip if already installed]**:
- Vulkan is supported and integrated with most graphics drivers offered by most popular distributions. You most likely already have Vulkan drivers.
- To verify if Vulkan is installed, install the `vulkan-tools` package from your distribution's package manager.
- Once the utility is installed, run `vkcube` from your terminal. If a test window appears with a spinning cube, Vulkan is installed in your system.
- If Vulkan is not installed, update your graphics drivers and verify your GPU or intergrated graphics support Vulkan.

2. **Downloading DXVK through grapejuice**:
- Go to the wineprefix that you want to install DXVK on, in this case it's the "Player" prefix
- Scroll down to the third party section, which is at the bottom
- Toggle the "Use DXVK D3D implementation" toggle, Grapejuice should now start downloading DXVK.


3. **Verify that Direct3D 10 or 11 is running in Roblox**:  
- To make sure DXVK is working, confirm Roblox is running Direct3D 10/11. [**D3D9 is not supported** as of August 2021]
- In Roblox, use the keyboard shortcut `Shift+F2` to see an information box in the bottom left of your screen.
- In the Graphics information section, you should see `D3D11` or `D3D10` as the rendering engine.

4. **Force Roblox to use another renderer**:  
- If another rendering engine is being used, use the built in Grapejuice render option to force the use of Direct3D.
   - To force D3D11 in Roblox, open grapejuice, scroll down to the "Graphics Settings" section. and set the "Roblox Renderer" to DX11
   - To force Vulkan in Roblox, do the same thing as above, except set the "Roblox Renderer" to Vulkan
 
## Roblox should be running faster than ever before now!  
## Notice: If you ever delete the Grapejuice wineprefix, you'll have to do the above steps again to get DXVK back.  

</details>
<br>

# Common compilation errors
<details>
<summary>Click to fold/unfold</summary>

## ` ==> ERROR: Patch application has failed. The error was logged to [Some path]/wine-tkg-git/wine-tkg-git/prepare.log for your convenience.`  

This is likely an issue with wine-tkg-git. Check their Github page for any issues that were created and any possible workarounds. Usually, issues like these are fixed pretty quickly, so running `git pull` in the directory of wine-tkg-git should suffice.

If you still have issues, you can make a Github issue or ask on the Grapejuice Discord server (mentioned in the Getting in touch section).

## If there are still issues present (mouse freezing, etc)

Ensure you followed the guide properly, especially when it came to installing/using it.

## If it asks whether to uninstall gst-editing-services  
Answer `yes`.

## `ERROR: 'autoreconf -f' failed.`  
Try to install **autoconf**.

## `E: Unable to locate package [package name]`  
Make sure your Debian/Ubuntu version is up-to-date. If it is, make sure you ran all of the commands properly for Debian.

## `Cannot find the [something] binary.`  
Install the package that provides the [something binary] with your package manager.

If, for example, it can't find `strip`, install `strip`. Same with `fakeroot`.

## `error: « struct x11drv_thread_data » has no member named « xi2_state »`  

Install `libxi-dev`.

## `conflicting types for ‘resize_vk_surfaces’`  

Install `libvulkan-dev`. (thanks, `Plasmaman916#6510`!)

Github issue: https://github.com/Frogging-Family/wine-tkg-git/issues/375

## `configure: error: Cannot build a 32-bit program.`  
 - Make sure you followed the guide properly, especially when it comes to installing dependencies.
 - Check the log file at `src/wine-tkg-staging-fsync-git-32-build/config.log` to try to diagnose the issue.
 - [Get in touch](#getting-in-touch)

## `error: X 32-bit development files not found.`
**If you are on Debian-like**: Install `libx11-dev:i386`.

## `configure: error: gstreamer-1.0 base plugins 32-bit development files not found,`  
 - Make sure you followed the guide properly, especially when it comes to installing dependencies.
 - If you are on Debian, make sure the following packages are installed: `libgstreamer1.0-dev:i386 libgstreamer-plugins-base1.0-dev:i386 libglib2.0-dev:i386`
 - [Get in touch](#getting-in-touch)

## `configure: error: FreeType 32-bit development files not found.`  
 - Make sure you followed the guide properly, especially when it comes to installing dependencies.
 - If you are on Debian, make sure the following packages are installed: `libfreetype-dev:i386`
 - [Get in touch](#getting-in-touch)

## `wine client error:0: version mismatch 726/728. Your wineserver binary was not upgraded correctly,`  

You need to stop any running `wineserver` process. You can do this by either rebooting, or running `killall wineserver`. Note that this will stop all running Wine programs so you may lose unsaved work in Studio and other Wine programs.  
After that, run `makepkg -si` again if you are on Arch Linux, otherwise it should work fine by now.  
</details>
<br>
 
# Common Roblox errors or issues
<details>
<summary>Click to fold/unfold</summary>

## Bad performance/input lag

**Studio performance issues:**
Go into Studio, press Alt+S, and then go to the renderer tab. Options such as the quality level and graphics level are available.
Note that studio's OpenGL renderer can cause widgets to flicker, and studio's Vulkan renderer requires the child window renderer patch here https://github.com/Frogging-Family/wine-tkg-git/blob/master/wine-tkg-git/wine-tkg-patches/misc/childwindow.patch. It should be included if you already followed the compilation guide.

**Game Client performance issues:**
If you haven't already, try lowering the graphics quality.
You can also click here to see how to change the renderer, which shouldn't affect graphics quality: https://discord.com/channels/563960075086200862/853709212030861363/853783776752566282

**Choosing a renderer:**
Using DXVK or Vulkan renderer can get better performance than other renderers.  
You can use the [full DXVK installation guide](#Installing-DXVK-(DirectX-over-Vulkan)) to install DXVK.  
Alternatively, to force Vulkan in Roblox, open the Grapejuice Fast Flag editor and enable the `FFlagDebugGraphicsPreferVulkan` flag.  
Their performance differs from device to device, so you're suggested to try them both to see which one fits your device better.

**Wine esync and fsync:**
Wine staging, Lutris' Wine, and Wine TKG come with esync. Only Wine TKG comes with fsync. (this includes the Wine you build from this guide)
You can use either fsync or esync, both of which improve performance. fsync improves performance more than esync.

To enable them, edit `~/.config/brinkervii/grapejuice/user_settings.json` and go to the line with env.
To use esync, edit that line to `"env": {"WINEESYNC": "1"}` and increase the number of file descriptors if it's low (check with `ulimit -Hn`)
To use fsync, you first need a kernel which supports it. Then edit the line to `"env": {"WINEFSYNC": "1"}`

Afterwards, kill the wineserver with `WINEPREFIX=~/.local/share/grapejuice/wineprefix wineserver -k`. Keep in mind that this will stop any currently running Roblox instance.

## `Unable to read VR Path Registry`  
`Unable to read VR Path Registry from C:\users\username\AppData\Local\openvr\openvrpaths.vrpath`  

You can ignore this error.

## "An error occured trying to launch the experience. Please try again later."

If using Firefox, go to `about:config` and edit `network.http.referer.XOriginPolicy` to be `1`.

## "An error occured in the secure channel support"

On Arch Linux or Arch-based distributions, uninstall Grapejuice and then use the grapejuice-git package from the AUR. This has the package manager take care of dependencies.

Alternatively, install `lib32-gnutls`

## "The server name or address could not be resolved"

Enable the nscd service from glibc

## "Error at hooking LdrFindResource_U"

Remove the CAP_NET_RAW capability from the Wine binaries

## "Your graphics drivers seem to be too old for Roblox to use."

On Arch Linux or Arch-based distributions, run `sudo pacman -S vulkan-driver lib32-vulkan-driver vulkan-icd-loader lib32-vulkan-icd-loader`

## No Roblox window is created and there is GLXBadFBConfig in the logs

Run `glxinfo -B | grep "OpenGL version string"`, If the version is below `4.0`, this fix likely won't work.

Edit ~/.config/brinkervii/grapejuice/user_settings.json and replace `"env": {},` with `"env": {"MESA_GL_VERSION_OVERRIDE": "4.4"},`.

If you already set some other environment variables, just add `"MESA_GL_VERSION_OVERRIDE": "4.4"` to the list.

Afterwards, kill the wineserver with `WINEPREFIX=~/.local/share/grapejuice/wineprefix wineserver -k`. Keep in mind that this will close any applications currently running through Grapejuice.

## Roblox crashes/kicks me out with an error
- "You have been kicked due to unexpected client behavior"
- "The program RobloxPlayerBeta.exe has encountered a serious problem and needs to close."
- "Unhandled exception: page fault on read access"
- "An unexpected error occurred and Roblox need to quit. We are sorry!"

You need Wine 6.11 or above, which this guide provices. This is an indication that you did not apply/install the built Wine properly.
</details>
<br>
