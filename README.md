# Vulkan on Raspberry Pi — Forging the Fire Within

![vulkan logo](https://raw.githubusercontent.com/TwilightHacker/vulkan_on_rpi/main/Vulkan%20Logo.jpg)

A battle-worn guide for warriors and tinkerers alike—this scroll shall lead you through the sacred rites of unlocking Vulkan’s power on the humble Raspberry Pi. Whether you seek speed, strength, or just to conquer new knowledge, the path lies ahead. Ready your tools.

## 🔥 Table of the Journey
- [TLDR](#tldr)
- [Compiling From Scratch](#compiling-from-scratch)
- [Demos](#demos)

## ⚔️ TLDR — For Those Who Ride Fast
Call upon PiKISS, the swift companion, to guide you past the shadows of manual toil.

```
sudo apt install curl
curl -sSL https://git.io/JfAPE | bash
```

To keep the winds fresh, update PiKISS:
```
cd ~/piKiss
git pull
```
Once summoned, run PiKISS and ride through the configuration halls:
![PiKISS-Configure](https://github.com/TwilightHacker/vulkan_on_rpi/blob/main/PiKISS%20Screenshots/PiKISS-configure.jpg?raw=true)<br /><br />
Choose “Vulkan” to begin the forging of the sacred drivers:
![PiKISS-Vulkan](https://github.com/TwilightHacker/vulkan_on_rpi/blob/main/PiKISS%20Screenshots/PiKISS-vulkan.jpg?raw=true)<br /><br />
At journey’s end, victory is declared when you see this banner:<br />
![PiKISS-Vulkan Ready](https://github.com/TwilightHacker/vulkan_on_rpi/blob/main/PiKISS%20Screenshots/PiKISS-vulkan-ready.jpg?raw=true)<br /><br />

## 🔧 Compiling from the Ashes
For those who choose the long road, honor awaits.
Check your system’s soul:

```
uname -a 
```
![Version Check](https://github.com/TwilightHacker/vulkan_on_rpi/blob/main/Manual%20Compile%20Screenshots/Version32_64.jpg?raw=true)<br /><br />
Sharpen your tools with updates:

```
sudo apt update
sudo apt upgrade
``` 

Gather dependencies as you would gather rations for a siege:

```
sudo apt install libxcb-randr0-dev libxrandr-dev libxcb-xinerama0-dev libxinerama-dev libxcursor-dev libxcb-cursor-dev libxkbcommon-dev xutils-dev xutils-dev libpthread-stubs0-dev libpciaccess-dev libffi-dev x11proto-xext-dev libxcb1-dev libxcb-*dev bison flex libssl-dev libgnutls28-dev x11proto-dri2-dev x11proto-dri3-dev libx11-dev libxcb-glx0-dev libx11-xcb-dev libxext-dev libxdamage-dev libxfixes-dev libva-dev x11proto-randr-dev x11proto-present-dev libclc-dev libelf-dev git build-essential mesa-utils libvulkan-dev ninja-build libvulkan1 python-mako libdrm-dev libxshmfence-dev libxxf86vm-dev libunwind-dev valgrind libzstd-dev vulkan-tools vulkan-utils ninja-build
```

Clear old remnants of failed campaigns:

```
sudo rm -rf /home/pi/mesa_vulkan
```
Begin your build anew:

```
sudo apt purge meson -y
sudo pip3 install meson
sudo pip3 install mako
cd ~ && git clone https://gitlab.freedesktop.org/mesa/mesa.git mesa_vulkan
cd mesa_vulkan
```
Choose your banner—64-bit or 32-bit:</br>
**64-bit:**
```
CFLAGS="-mcpu=cortex-a72" \
CXXFLAGS="-mcpu=cortex-a72" \
```
**32-bit:**
```
CFLAGS="-mcpu=cortex-a72 -mfpu=neon-fp-armv8" \
CXXFLAGS="-mcpu=cortex-a72 -mfpu=neon-fp-armv8" \
```
```
meson --prefix /usr \
-D platforms=x11 \
-D vulkan-drivers=broadcom \
-D dri-drivers= \
-D gallium-drivers=kmsro,v3d,vc4 \
-D buildtype=release build
ninja -C build -j4
sudo ninja -C build install
```
Invoke the forge:
```
glxinfo -B
```
Then ensure the beast lives:</br>
![glxinfo -B Command](https://github.com/TwilightHacker/vulkan_on_rpi/blob/main/Manual%20Compile%20Screenshots/glxinfo.jpg?raw=true)<br/><br/>

## 🛡️ Glorious Demos — Prove Your Might
Without trials, there is no glory. Face the demos head-on:
```
sudo apt install libassimp-dev
git clone --recursive https://github.com/SaschaWillems/Vulkan.git  sascha-willems 
cd sascha-willems && python3 download_assets.py
mkdir build
cd build $ cmake -DCMAKE_BUILD_TYPE=Debug  .. 
make -j4
```
The results lie in build/bin. Run them. Witness them. Let your Vulkan banner fly!

