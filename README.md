# To Pop!_OS/Kali Linux users  
## Please notice that the distro you are using is not capable of building Wine, due to many conflicts in 32/64 bit packages. You must change distro in order to build Wine.  
Also, don't use Kali Linux as your main distro, especially not with the default password.  

## What is this?  
This is a guide on how to make Wine run Roblox **with staging patches**  
**It includes the mouse fix, you do not need any other patches.**  
**It also fixes the black cursor bug in Studio, by reverting the commit that caused the issue.**  
* [Guide version 25, 2021-08-20 11 AM (UTC+8)](#guide-version-25-2021-08-20-11-am-utc8)
   * [Video guides](#video-guides)
      * [Prebuilt](#prebuilt)
   * [Dependency install](#dependency-install)
      * [Arch Linux alike](#arch-linux-alike)
      * [Debian/Fedora alike](#debianfedora-alike)
      * [Other distros](#other-distros)
      * [Notice](#notice)
   * [Steps to compile](#steps-to-compile)
      * [After finishing Step 7.2, here is how to use the just built Wine](#after-finishing-step-72-here-is-how-to-use-the-just-built-wine)
* [Common build problems version 23, 2021-08-20 12 PM](#common-build-problems-version-23-2021-08-20-12-pm)
   * [If guide version changed during your build, consider starting over.](#if-guide-version-changed-during-your-build-consider-starting-over)
      * [If it complains ERROR: Patch application has failed](#if-it-complains-error-patch-application-has-failed)
      * [If Roblox is still acting up (Crash, Mouse bug, etc.)](#if-roblox-is-still-acting-up-crash-mouse-bug-etc)
         * [If you didn't install globally](#if-you-didnt-install-globally)
         * [If you installed globally](#if-you-installed-globally)
      * [If it asks whether to uninstall gst-editing-services](#if-it-asks-whether-to-uninstall-gst-editing-services)
      * [If it complains ERROR: 'autoreconf -f' failed.](#if-it-complains-error-autoreconf--f-failed)
      * [If the script is trying to uninstall stuff](#if-the-script-is-trying-to-uninstall-stuff)
      * [If it complains E: Unable to locate package [Package Name]](#if-it-complains-e-unable-to-locate-package-package-name)
      * [If it complains Cannot find the [Something] binary.](#if-it-complains-cannot-find-the-something-binary)
      * [If it complains error: « struct x11drv_thread_data » has no member named « xi2_state »](#if-it-complains-error--struct-x11drv_thread_data--has-no-member-named--xi2_state-)
      * [If it complains conflicting types for ‘resize_vk_surfaces’](#if-it-complains-conflicting-types-for-resize_vk_surfaces)
      * [If it complains error: Cannot build a 32-bit program.](#if-it-complains-error-cannot-build-a-32-bit-program)
      * [If it complains error: X 32-bit development files not found.](#if-it-complains-error-x-32-bit-development-files-not-found)
      * [If it complains error: gstreamer-1.0 base plugins 32-bit development files not found,](#if-it-complains-error-gstreamer-10-base-plugins-32-bit-development-files-not-found)
      * [If it complains error: FreeType 32-bit development files not found.](#if-it-complains-error-freetype-32-bit-development-files-not-found)
      * [If it complains wine client error:0: version mismatch 726/728.](#if-it-complains-wine-client-error0-version-mismatch-726728)
      * [If it complains Unable to read VR Path Registry](#if-it-complains-unable-to-read-vr-path-registry)

# Guide version 25, 2021-08-20 11 AM (UTC+8)  

## Video guides
### If you're making a video guide
**Attach link to this guide in the description + pin comment, please.**  
Mention of Discord nickname is optional but wanted.  
Also, if you're making a **Prebuilt** tutorial, **mention that it's a prebuilt that you made.**  
If you don't comply, you're a bad person.  
### Prebuilt  
The video tells you to install a prebuilt, while it is **easier**, it can be **risky** since you have to trust the creator for **not adding malware** to the build.  
(UPDATED!) How to play Roblox on Linux Ubuntu 20.04 LTS! (WORKING AUGUST 2021, READ DESCRIPTION)  
https://www.youtube.com/watch?v=xQHBPXsorxU  

## Dependency install  
### Arch Linux alike  
Makepkg will do it for you, you don't need to install them yourself.  
### Debian/Fedora alike  
On step 6, change **_nomakepkg_dep_resolution_distro** to `debuntu` or `fedora` according to your distro.  
You should also run `sudo dpkg --add-architecture i386 && sudo apt update` if you're using **Debian alike**.    
### Other distros  
Install manually, check https://wiki.winehq.org/Building_Wine#Satisfying_Build_Dependencies  
### Notice  
These are other common missing dependencies, make sure they are all installed, **or the build will fail.**  
**autoconf**, **libxi-dev**, **libvulkan-dev**

You should also install **ccache** if you don't expect yourself to make it work on the first try.  
It will make the build **after the the first one** at least **5 times faster**.


## Steps to compile  
The lines that look like `this` are commands, run them in your terminal.  
0. Install the build dependency (Check **Dependency install** section)  
1. Clone the wine-tkg-git repo:  
`git clone https://github.com/Frogging-Family/wine-tkg-git.git`  
2. Enter the just cloned directory:  
`cd wine-tkg-git`  
3. Download the patch file:  
`curl https://gist.githubusercontent.com/e666666/c9f057a16b9b4267e4e4f9520cab72b1/raw/1c0f4448e130f7ae13b4a9fcdf0628b832e93be9/roblox-staging-patch-v2.patch --output roblox-wine-staging-v2.patch`  
4. Apply the patch **(You must build Wine according to the later steps for the patch to do anything)**:  
`git apply roblox-wine-staging-v2.patch`  
5. Change to the deeper folder:  
`cd wine-tkg-git`  
6. Edit customization.cfg to your needs. (**Optional**)  
For example, you can build Wine 6.16 by setting `_plain_version` to `6.16` and `_staging_version` to `v6.16`, notice the extra `v`.  
7. Follow 7.1 or 7.2 according to your distro.  
**(Please read through Common build problems below the guide before asking for help on the server)**  
8.1. (If you are on **Arch Linux alike**) `makepkg -si` **(All lowercap)**  
After the build finished, **make sure to unset wine_binary in ~/.config/brinkervii/grapejuice/user_settings.json, if you changed it before.**  
8.2. (If you are not) `./non-makepkg-build.sh`

### After finishing Step 7.2, here is how to use the just built Wine  
**(You don't have to do this if you followed Step 7.1)**  
1. **From the same directory as the non-makepkg-build.sh**, `cd non-makepkg-builds`  
If you can't find non-makepkg-builds after the script finished, **the build 99% failed.**  
Check the script output in the terminal for info on the exact issue.  
2. There should be a directory named something like **wine-tkg-staging-fsync-git-6.14.r7.g05c42b1d**
3. Move the directory outside of the wine-tkg-git repo, so you can delete the repo later to save space (**Optional**)
4. Install Grapejuice
5. Open **~/.config/brinkervii/grapejuice/user_settings.json** in your favorite editor
6. Set **wine_binary** to **[The wine-tkg directory]/bin/wine**


# Common build problems version 23, 2021-08-20 12 PM  
## If guide version changed during your build, consider starting over.  

### If it complains `ERROR: Patch application has failed`  
` ==> ERROR: Patch application has failed. The error was logged to [Some path]/wine-tkg-git/wine-tkg-git/prepare.log for your convenience.`  
Open **prepare.log** (it's in the same directory as non-makepkg-build.sh) in a text editor, and scroll to the **bottom**.  
There should be a line that looks like an error, **you should also check lines around the error, they can be the cause as well.**  
If you want to ask for help, make sure to attach the **prepare.log** since the error itself is very generic.

### If Roblox is still acting up (Crash, Mouse bug, etc.)  
#### If you didn't install globally  
Make sure you changed **wine_binary** according to `After finishing Step 7.2`  
#### If you installed globally  
Try to issue `wine --version` from a terminal, it should look something like:  
`wine-6.15.r1.gb09fe464 ( TkG Staging Esync Fsync )`  
If it only shows `wine-6.15` or something like that, **the install failed**, try to reinstall.  
If it still doesn't work, make sure to unset **wine_binary** to `""` in **~/.config/brinkervii/grapejuice/user_settings.json**.

### If it asks whether to uninstall gst-editing-services  
If it asks whether to uninstall gst-editing-services, I suggest you to answer **yes**.  

### If it complains `ERROR: 'autoreconf -f' failed.`  
Try to install **autoconf**.

### If the script is trying to uninstall stuff  
If you are running **Debian alike**, and the script is trying to uninstall stuff by calling **apt**, answer **yes**.  
It is the build script swapping build library on the fly, so that you don't have to.

### If it complains `E: Unable to locate package [Package Name]`  
My guess is you are running **Debian alike**, this error can be sometimes safe.  
But in case stuff went wrong, try to do `sudo apt update`, **make sure the command succeeds.**

### If it complains `Cannot find the [Something] binary.`  
`==> ERROR: Cannot find the fakeroot binary.`  
`==> ERROR: Cannot find the strip binary`  
You need to install the command **fakeroot** and **strip**

### If it complains `error: « struct x11drv_thread_data » has no member named « xi2_state »`  
`../wine-mirror-git/dlls/winex11.drv/mouse.c:541:13: error: « struct x11drv_thread_data » has no member named « xi2_state »`  
Install **libxi-dev**.

### If it complains `conflicting types for ‘resize_vk_surfaces’`  
`../wine-mirror-git/dlls/winex11.drv/vulkan.c:878:6: error: conflicting types for ‘resize_vk_surfaces’`  
You've hit an known issue at https://github.com/Frogging-Family/wine-tkg-git/issues/375 .  
Fortunately, with help from `Plasmaman916#6510`, the fix was discovered.  
You just need to install **libvulkan-dev**, and it will work.

### If it complains `error: Cannot build a 32-bit program.`  
`configure: error: Cannot build a 32-bit program. you need to install 32-bit development libraries.`  
1. Make sure that you followed the **Dependency install** section.  
2. **(Debian alike)** Run `gcc --version`, after that, install **gcc-8-multilib**, replace 8 with the version that you got, try different version numbers (Ex. "8.4" and "8.4.0") if the package doesn't exist.
3. Check the log file at **src/wine-tkg-staging-fsync-git-32-build/config.log** to see what might be wrong.  
In order to find where stuff went wrong, I usually search for **the error** in the log file.  
3. If it's still not working, ping me with a message **including your exact distro and the log file**, so I can investigate further.  

### If it complains `error: X 32-bit development files not found.`  
`error: X 32-bit development files not found. Wine will be built without X support, which probably isn't what you want.`  
Do what it says, and install **libx11-dev:i386** if you're on Debian alike.

### If it complains `error: gstreamer-1.0 base plugins 32-bit development files not found,`  
`configure: error: gstreamer-1.0 base plugins 32-bit development files not found, GStreamer won't be supported.`  
1. Make sure that you followed the **Dependency install** section.
2. Make sure that you installed **the 32-bit version** of both **GStreamer 1.0 (libgstreamer1.0-dev:i386)** and **GStreamer Plugins Base 1.0 (libgstreamer-plugins-base1.0-dev:i386)**, they are **different** libraries!
3. Make sure that you installed **GLib (libglib2.0-dev:i386)** 32-bit development files. **It is GLib, not glibc!**
4. If it's still not working, ping me with a message **including your exact distro**, so I can investigate further

### If it complains `error: FreeType 32-bit development files not found.`  
`configure: error: FreeType 32-bit development files not found. Fonts will not be built.`
1. Make sure that you followed the **Dependency install** section.
2. Make sure that you installed **FreeType** for 32 bit, it's called **libfreetype-dev:i386** on Debian alike.
3. If it's still not working, ping me with a message **including your exact distro**, so I can investigate further

### If it complains `wine client error:0: version mismatch 726/728.`  
`wine client error:0: version mismatch 726/728. Your wineserver binary was not upgraded correctly, or you have an older one somewhere in your PATH. Or maybe the wrong wineserver is still running?`  
You forgot to stop the **wineserver** process before installing the new built Wine.  
Stop the process with `WINEPREFIX=~/.local/share/grapejuice/wineprefix wineserver -k`, and retry.  
If it still doesn't work, **Close all your Wine programs**, issue `killall wineserver` and then **reinstall** the new built Wine.

### If it complains `Unable to read VR Path Registry`  
`Unable to read VR Path Registry from C:\users\username\AppData\Local\openvr\openvrpaths.vrpath`  
This is a **safe** error, you can ignore it.  
