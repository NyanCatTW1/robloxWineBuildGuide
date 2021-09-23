# To Pop!_OS/Kali Linux users  
## Please notice that the distro you are using is not capable of building Wine, due to many conflicts in 32/64 bit packages. You must change distro in order to build Wine.  
Also, don't use Kali Linux as your main distro, especially not with the default password.  
If you're using other distros, just ignore this section and read below.  

# The ultimate Roblox on Linux guide
This is a guide on building wine-tkg-git for Roblox as well as a couple of workarounds for issues, originally by `Nyan cat#8349`.

It includes the following patches and improvements:
 - Right-click mouse fix (by applying a patch)
 - Black cursor studio bug (by reverting the commit that caused it)

This guide is rapidly changing, so please pay attention to the date at which it was updated. If it was updated while you were following it, start over.


**In order to start this guide**, jump over to the [steps to compile](#steps-to-compile) section if you want to install Wine and Roblox.

Alternatively, you can hop over to the [video guide](#video-guide) section in case you prefer to follow a video guide (although compilation is recommended).

**In case you run into any issues while compiling**, you can hop over to the [common compilation errors](#common-compilation-errors) section.

**If you run into any problems while trying to actually play the game** or use Wine in general, take a look at the [common errors or issues](#common-errors-or-issues) section.

# Notice to video guide creators
If you are creating a video guide (YouTube, etc.) please attach a link to this guide in the pinned comments, as well as the description.

Mention of the Discord tag is optional but preferred.

If you are telling people to download a precompiled version of Wine in your guide, please mention it as such.

# Video guide
Here's a video guide on YouTube. Do note that it tells you to download a precompiled version of Wine, which may contain malware or behave unexpectedly:

[YouTube](https://www.youtube.com/watch?v=xQHBPXsorxU)

[CloudTube](https://tube.cadence.moe/watch?v=xQHBPXsorxU)

# Getting in touch
You can get in touch on the Grapejuice Discord server: https://discord.gg/mRTzEb6

Make sure to follow the rules and ask your question in one of the help channels. Do not post your question in multiple channels.


# Steps to compile  
<details open>
<summary>Click to fold/unfold</summary>

1. **Clone the wine-tkg-git repository**:  
`git clone https://github.com/Frogging-Family/wine-tkg-git.git`  
2. **Enter the just cloned directory**:  
`cd wine-tkg-git`  
3. **Download the patch file**:  
`curl https://raw.githubusercontent.com/e666666/robloxWineBuildGuide/main/roblox-wine-staging-v2.patch --output roblox-wine-staging-v2.patch`  
4. **Apply the patch**:  
`git apply roblox-wine-staging-v2.patch`  
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
   - Go to [this link](https://gitlab.com/brinkervii/grapejuice/-/wikis/home) and follow the instructions specific to your distribution.
11. **Configuring Grapejuice to use Wine**:
   - **If you are on Arch Linux**: ignore this step
   - **If you are on other distros**:
      - Open `~/.config/brinkervii/grapejuice/user_settings.json` in your text editor.
      - Set the `wine_binary` field to the path you found in step 9, followed by `/bin/wine`.
      
      **For example**, if your path was `/home/user/wine-tkg-git/wine-tkg-git/non-makepkg-builds/wine-tkg-staging-fsync-git-6.14.r7.g05c42b1d`, you will have to turn it into `/home/user/wine-tkg-git/wine-tkg-git/non-makepkg-builds/wine-tkg-staging-fsync-git-6.14.r7.g05c42b1d/bin/wine`
12. **Try it out**:
   - Press the Play button on any game on roblox.com
   - **If you encounter any issues**, errors or low performance, please look if they are mentioned in this guide. You can use `CTRL + F` in your browser to search for any errors mentioned here.
   - [Get in touch](#getting-in-touch) if you have any further questions!
</details>

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

**Using DXVK:**
In addition to changing the renderer as mentioned in the above two sections, you can also use DXVK from <https://github.com/doitsujin/dxvk>. It can greatly improve performance. Make sure to set the wineprefix to the Grapejuice wineprefix, like `WINEPREFIX=~/.local/share/grapejuice/wineprefix ./setup_dxvk.sh install`, and enable any of the Direct3D renderers. This can get better performance than Roblox's OpenGL or Vulkan renderer.

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
 
