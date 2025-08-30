***OpenSUSE Tumbletweed GUIDE***

### 1 Install nVidia drivers:
```
sudo zypper install openSUSE-repos-Tumbleweed-NVIDIA
sudo zypper install-new-recommends
```
### 2 Install and set VirtualBox
```
sudo zypper in virtualbox
```

Add current user vboxusers group:
```
sudo gpasswd -a <username> vboxusers
```

### 3 Install and set Java
```
sudo zypper in java-24-openjdk-devel java-21-openjdk-devel java-16-openjdk-devel java-17-openjdk-devel
```

Set alternatives:
```
sudo update-alternatives --config java
sudo update-alternatives --config javac
```

### 4 Fix Jetbrains-based IDEs
```
sudo zypper install libgthread-2_0-0
```

### 5 Install some DEV packages
```
sudo zymmer in cmake gtk3-devel clang20 git-core
```