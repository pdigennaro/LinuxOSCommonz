## 🧩 openSUSE Tumbleweed – Fresh Install & Setup Guide

---

### 1️⃣ System Preparation

Update repositories and recommended packages:

```bash
sudo zypper install openSUSE-repos-Tumbleweed-NVIDIA
sudo zypper install-new-recommends
sudo zypper update
sudo reboot
```

Check NVIDIA driver:

```bash
nvidia-smi
```

---

### 3️⃣ Java (Multiple JDK Versions)

Install JDKs:

```bash
sudo zypper in java-21-openjdk java-21-openjdk-devel
sudo zypper in java-24-openjdk-devel
```

Select default version:

```bash
sudo update-alternatives --config java
sudo update-alternatives --config javac
```

Check:

```bash
java -version
javac -version
```

---

### 5️⃣ Flutter & .NET SDK Setup

#### Install Flutter

If not already downloaded:

```bash
sudo zypper install cmake gtk3-devel ninja clang20 git-core
```

#### Configure Flutter

```bash
flutter --disable-analytics
flutter doctor --android-licenses
flutter doctor
```

#### Install .NET SDK (user mode)

```bash
chmod +x ./dotnet-install.sh
./dotnet-install.sh --channel 9.0
```

Add to `~/.bashrc`:

```bash
export DOTNET_ROOT=$HOME/.dotnet
export DOTNET_CLI_TELEMETRY_OPTOUT=1
export MSBuildSDKsPath=$DOTNET_ROOT/sdk/$( $DOTNET_ROOT/dotnet --version )/Sdks
PATH=$PATH:$DOTNET_ROOT
export PATH
```

---

### 6️⃣ Virtualization & Containers

#### VirtualBox

```bash
sudo zypper in virtualbox
sudo gpasswd -a $USER vboxusers
```

#### Docker

```bash
sudo zypper install docker docker-compose docker-compose-switch
sudo systemctl enable docker
sudo usermod -G docker -a $USER
newgrp docker
sudo systemctl restart docker
docker version
```

#### QEMU

```bash
sudo zypper in qemu
```

---

### 7️⃣ Qt & C++ Tools

```bash
sudo zypper in qtcreator qt-creator clang20 cmake ninja
```

---

### 8️⃣ Git & SSH Configuration

Install and configure Git:

```bash
sudo zypper install git-core
```

Generate SSH key for GitHub/GitLab:

```bash
ssh-keygen -t ed25519 -C "youremail@example.com"
eval "$(ssh-agent -s)"
ssh-add ~/.ssh/id_ed25519
cat ~/.ssh/id_ed25519.pub
```

---

### 9️⃣ System Utilities & Monitoring

Install common tools:

```bash
sudo zypper install conky
sudo zypper install kdenlive
```

Monitor resources:

```bash
top
watch free -h
```

---

### ✅ Final Checks

After everything:

```bash
sudo zypper update
sudo zypper ps -s
sudo reboot
```
