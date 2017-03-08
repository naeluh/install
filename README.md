# install

	OpenCV_DIR="/mnt/z/torch-opencv/opencv/cmake/templates" luarocks install cv

	Z:\torch-opencv

----------------------------------

	th neural_style.lua -gpu -1 -style_image convergence.jpg -content_image a.JPG

	wget http://developer.download.nvidia.com/compute/cuda/7_5/Prod/local_installers/rpmdeb/cuda-repo-ubuntu1404-7-5-local_7.5-28_amd64.deb

-------------------------------

Some packages could not be installed. This may mean that you have
requested an impossible situation or if you are using the unstable
distribution that some required packages have not yet been created
or been moved out of Incoming.
The following information may help to resolve the situation:

The following packages have unmet dependencies:
 nvidia-cuda-toolkit : Depends: nvidia-opencl-dev (= 5.5.22-3ubuntu1) but it is not going to be installed or
                                opencl-dev
E: Unable to correct problems, you have held broken packages.

	sudo apt-get install ocl-icd-opencl-dev


-----------------------



	luarocks install cutorch
	luarocks install cunn


Then this works

	export PATH=/usr/local/cuda-7.0/bin:$PATH 
	source ~/.bashrc

To install onlder cunn for lua 

	luarocks install https://raw.githubusercontent.com/soumith/cudnn.torch/R4/cudnn-scm-1.rockspec

	export LD_LIBRARY_PATH=/usr/local/cuda-7.0/lib64:$LD_LIBRARY_PATH
	source ~/.bashrc

------

Make for open cv


	cmake -D CMAKE_BUILD_TYPE=RELEASE \
	-D CMAKE_INSTALL_PREFIX=/usr/local \
	-D INSTALL_C_EXAMPLES=OFF \
	-D INSTALL_PYTHON_EXAMPLES=ON \
	-D OPENCV_EXTRA_MODULES_PATH=~/opencv_contrib/modules \
	-D BUILD_EXAMPLES=ON ..


	cmake -D CUDA_ARCH_BIN=3.2 \
    -D CUDA_ARCH_PTX=3.2 \
    -D CMAKE_BUILD_TYPE=RELEASE \
    -D CMAKE_INSTALL_PREFIX=/usr/local \
    -D WITH_TBB=ON \
    -D BUILD_NEW_PYTHON_SUPPORT=ON \
    -D WITH_V4L=ON \
    -D BUILD_TIFF=ON \
    -D WITH_QT=ON \
    -D INSTALL_C_EXAMPLES=OFF \
    -D ENABLE_PRECOMPILED_HEADERS=OFF \
   	-D BUILD_EXAMPLES=ON \
    -D WITH_OPENGL=ON ..


	sudo echo "/usr/local/cuda-8.0/lib64" > /etc/ld.so.conf.d/cuda.conf

	--------------------------------------

	wget http://developer.download.nvidia.com/compute/cuda/7_5/Prod/local_installers/rpmdeb/cuda-repo-ubuntu1404-7-5-local_7.5-28_amd64.deb


	=-----------------------

The installation of CUDA is little a bit tricky. I've followed the following steps and it works for me. You can refer to this link also.

Confirmation of the environment –

	lspci | grep -i nvidia (Confirm that the information of NVIDIA's board is displayed)
	uname -m (make sure that it is a x86_64)
	gcc --version (make sure it is installed)
Installation of CUDA –

Download cuda_7.5.18_linux.run file from https://developer.nvidia.com/cuda-downloads
Run the following command –

	a. sudo apt-get install build-essential

	b. sudo vi /etc/modprobe.d/blacklist-nouveau.conf

	c. Then, add the following line in that file: blacklist nouveau option nouveau modeset=0

	d. sudo update-initramfs -u
Reboot computer
At login screen, press Ctrl+Alt+F1and login to your user.
Go to the directory where you have the CUDA driver, and run

	a. chmod a+x .

	b. sudo service lightdm stop

	c. sudo bash cuda-7.5.18_linux.run --no-opengl-libs
During the install –

a. Accept EULA conditions

b. Say YES to installing the NVIDIA driver

c. Say YES to installing CUDA Toolkit + Driver

d. Say YES to installing CUDA Samples

e. Say NO rebuilding any Xserver configurations with Nvidia
Check if /dev/nvidia* files exist. If they don't, do the following –

	a. sudo modprobe nvidia
Set Environment path variables –

	a. export PATH=/usr/local/cuda-7.0/bin:$PATH

	b. export LD_LIBRARY_PATH=/usr/local/cuda-7.0/lib64:$LD_LIBRARY_PATH

	source ~/.bashrc

Verify the driver version –

	a. cat /proc/driver/nvidia/version
Check CUDA driver version

	a. nvcc –V
Switch the lightdm back on again

	a. sudo service lightdm start
Ctrl+Alt+F7 and login to the system through GUI
Create CUDA Samples –

	a. Go to NVIDIA_CUDA-7.5_Samples folder through terminal

	b. make

	c. cd bin/x86_64/linux/release/

	d. ./deviceQuery

	e. ./bandwidthTest

f. Both tests should ultimately output a 'PASS' in terminal
Reboot the system



	th neural_style.lua -gpu 0 -print_iter 1 -backend nn -optimizer adam


---------------------------------------------

Nvidia drivers

If you have an Nvidia graphics card on your system, then its recommended to install the official drivers provided by Nvidia. The proprietory drivers would utilise the hardware properly delivering full performance.

Installation is pretty easy and it uses a ppa repository. So you do not need to compile anything. However, make sure to follow the steps properly.

These steps would work on Ubuntu and close derivatives like Xubuntu, Kubuntu, Lubuntu and also Linux Mint and Elementary OS.

1. Find out your graphics card model
Use the lspci command to find out the model of your graphics card

	$ lspci -vnn | grep -i VGA -A 12
01:00.0 VGA compatible controller [0300]: NVIDIA Corporation GT218 [GeForce 210] [10de:0a65] (rev a2) (prog-if 00 [VGA controller])
        Subsystem: ASUSTeK Computer Inc. Device [1043:8416]
Here its GeForce 210

2. Find out the right driver version for your graphics card
Visit http://www.nvidia.com/Download/index.aspx
Fill in the details about your graphics card and system and then click Search. On the next page, it should tell you the correct driver version with a download link and additional information.

For the above GeForce 210 card, it showed 331.67 as the correct driver which can be downloaded from the website. However we shall install the drivers from ppa to make things easier.

3. Setup the xorg-edgers ppa
The xorg-edgers ppa provides the very latest nvidia drivers. Run the following commands to set it up.

	$ sudo add-apt-repository ppa:xorg-edgers/ppa -y
	$ sudo apt-get update
Now the ppa is setup and the package information is also updated.

4. Install the driver
Either you can install the driver directly by installing a single package containing "nvidia" and the major version number ( 173, 304, 310, 313, 319, 331, 334 or 337).

# 331 driver
	$ sudo apt-get install nvidia-331

# 334 driver
	$ sudo apt-get install nvidia-334

# install the latest version
	$ sudo apt-get install nvidia-current
Or you can enable it from the "Additional Drivers" section. This is different on different Ubuntu flavors.

Synaptic package manager

If you have synaptic package manager installed, then go to Settings > Repositories > Additional Drivers tab and select the correct nvidia driver, and click Apply changes.

# or launch it from command line
	$ sudo software-properties-gtk
ubuntu software updates nvidia
Ubuntu

If you are running Ubuntu unity desktop, simply launch the dash and search for "driver". Then click the application named "Additional Drivers". It will launch the same dialog box as shown above.

Xubuntu

Go to "All Settings > Additional Drivers" and you should see a list of all available nvidia drivers ready to be installed. Select the correct driver and click Apply Changes. The new driver would be downloaded, installed and configured for use.

Kubuntu

Go to System Settings > System Administration > Driver Manager and select the nvidia driver there and click Apply.

After the installation is complete, reboot the system. You should see an option called "Nvidia X Server Settings" in your applications menu. From there you can check information about the graphics card and configure it.

5. Verify the installation
The last thing to do is verify that the nvidia drivers are loaded and working. Run the lspci command again and this time the kernel driver should show nvidia

	$ lspci -vnn | grep -i VGA -A 12
01:00.0 VGA compatible controller [0300]: NVIDIA Corporation GT218 [GeForce 210] [10de:0a65] (rev a2) (prog-if 00 [VGA controller])
        Subsystem: ASUSTeK Computer Inc. Device [1043:8416]
        Flags: bus master, fast devsel, latency 0, IRQ 46
        Memory at e2000000 (32-bit, non-prefetchable) [size=16M]
        Memory at d0000000 (64-bit, prefetchable) [size=256M]
        Memory at e0000000 (64-bit, prefetchable) [size=32M]
        I/O ports at 2000 [size=128]
        [virtual] Expansion ROM at e3080000 [disabled] [size=512K]
        Capabilities: <access denied>
        Kernel driver in use: nvidia
Check the last line which says "kernel driver in use: nvidia". This shows that nvidia drivers are now in action. Also check hardware acceleration with the glxinfo command

	$ glxinfo | grep OpenGL | grep renderer
OpenGL renderer string: GeForce 210/PCIe/SSE2
The OpenGL renderer string should be anything other than "MESA". Then it indicates that the hardware drivers are being used for hardware acceleration.

6. Nvidia settings tool
Nvidia would install a gui tool called "Nvidia X Server Settings" somewhere in the menu. It can also be launched from the command line using the command "nvidia-settings". The tool shows miscellaneous information about the graphics card and the monitor connected, and also allows to configure various options.

nvidia settings gpu info
The tool allows to configure the resolution of the monitor. If you are using dual monitors for example, then you can configure the monitor positions as well.

Removing the drivers
Incase anything goes wrong after the installation, like you are not able to boot Ubuntu, then try removing the Nvidia drivers.

Boot into the recovery console from the grub menu and then issue the following commands

# remount root file system as writable
	$ mount -o remount,rw /

# remove all nvidia packages
$ apt-get purge nvidia*
Additional Notes
Many tutorials out there talk about blacklisting the nouveau driver. This is no longer necessary, since the nvidia driver would blacklist nouveau itself. This can be verified by checking the contents of nvidia driver files in the the modprobe.d directory.

$ grep 'nouveau' /etc/modprobe.d/* | grep nvidia
/etc/modprobe.d/nvidia-331_hybrid.conf:blacklist nouveau
/etc/modprobe.d/nvidia-331_hybrid.conf:blacklist lbm-nouveau
/etc/modprobe.d/nvidia-331_hybrid.conf:alias nouveau off
/etc/modprobe.d/nvidia-331_hybrid.conf:alias lbm-nouveau off
/etc/modprobe.d/nvidia-graphics-drivers.conf:blacklist nouveau
/etc/modprobe.d/nvidia-graphics-drivers.conf:blacklist lbm-nouveau
/etc/modprobe.d/nvidia-graphics-drivers.conf:alias nouveau off
/etc/modprobe.d/nvidia-graphics-drivers.conf:alias lbm-nouveau off
Note that the files "nvidia-331_hybrid.conf" and "nvidia-graphics-drivers.conf" have blacklisted nouveau.

To check information about the nvidia driver module, use the commands lsmod, modprobe and modinfo

# check that nvidia kernel module is loaded or not
$ lsmod | grep nvidia
nvidia              10699336  49 
drm                   302817  2 nvidia

# find the real name of the nvidia module
$ modprobe -R nvidia
nvidia_331

# details about the nvidia_331 module
$ modinfo nvidia_331
filename:       /lib/modules/3.13.0-24-generic/updates/dkms/nvidia_331.ko
alias:          char-major-195-*
version:        331.67
supported:      external
license:        NVIDIA
.....
The kernel module file for the nvidia driver is located at "/lib/modules/3.13.0-24-generic/updates/dkms/nvidia_331.ko".

Note that it is a "dkms" module which means, its loaded dynamically. Due to this the grub screen, the Ubuntu/Kubuntu splash screens would have a low resolution since at that time the nvidia drivers are not in effect, and whatever resolution is available via the VESA extensions, are used.nvcc
