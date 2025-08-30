***OpenSUSE Tumbletweed GUIDE***

Install nVidia drivers:
sudo zypper install openSUSE-repos-Tumbleweed-NVIDIA
sudo zypper install-new-recommends

Install and set VirtualBox
sudo zypper in virtualbox

sudo gpasswd -a <username> vboxusers

Install and set Java
sudo zypper in java-24-openjdk-devel java-21-openjdk-devel java-16-openjdk-devel java-17-openjdk-devel

sudo update-alternatives --config java
sudo update-alternatives --config javac

Fix Jetbrains-based IDEs
sudo zypper install libgthread-2_0-0