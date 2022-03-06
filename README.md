# podman-setup
Steps to enable podman - on windows using wsl2 having ubuntu distro


Pre-requisite:
1. Install Windows Terminal [optional]: https://docs.microsoft.com/en-us/windows/terminal/install
Click https://aka.ms/terminal and this will open Windows Store and download/update Windows-Terminal utility

2. Setup WSL development env: https://docs.microsoft.com/en-us/windows/wsl/setup/environment

References:
Official Podman installation url: https://podman.io/getting-started/installation 
https://ubuntu.com/tutorials/install-ubuntu-on-wsl2-on-windows-11-with-gui-support#1-overview
https://www.how2shout.com/linux/how-to-upgrade-wsl-2-or-1-ubuntu-20-04-to-22-04-lts/
https://alessio.franceschelli.me/posts/windows/wsl2-upgrade/
https://dev.to/bowmanjd/install-docker-on-windows-wsl-without-docker-desktop-34m9
https://computingforgeeks.com/how-to-install-podman-on-ubuntu/


Windows Check Settings -> system -> about -> windows specifications -> shows Windows OS build: 22543.1000
wsl2 can't be installed if os build < 20000

C:\>wsl --status

C:\>wsl --list -o
The following is a list of valid distributions that can be installed.
The default distribution is denoted by '*'.
Install using 'wsl --install -d <Distro>'.

  NAME            FRIENDLY NAME
* Ubuntu          Ubuntu
  Debian          Debian GNU/Linux
  kali-linux      Kali Linux Rolling
  openSUSE-42     openSUSE Leap 42
  SLES-12         SUSE Linux Enterprise Server v12
  SLES-15         SUSE Linux Enterprise Server v15
  Ubuntu-18.04    Ubuntu 18.04 LTS
  Ubuntu-20.04    Ubuntu 20.04 LTS 
  

C:\wsl2>wsl --install -d Ubuntu-20.04
The requested operation requires elevation.
Installing: Virtual Machine Platform
Virtual Machine Platform has been installed.
Installing: Windows Subsystem for Linux
Windows Subsystem for Linux has been installed.
Installing: Ubuntu 20.04 LTS
Ubuntu 20.04 LTS has been installed.
The requested operation is successful. Changes will not be effective until the system is rebooted.

Installing, this may take a few minutes...
WslRegisterDistribution failed with error: 0x80370114
Error: 0x80370114 The operation could not be started because a required feature is not installed.

Press any key to continue...
  
<How to Fix this>
Control panel -> Programs & Feature -> Turn windows features on or off -> ON: windows subsystem for linux , off: windows hypervisor platform, ON: Virtual machine platform -> Reboot -> and then start ubuntu program...

Installing, this may take a few minutes...
Please create a default UNIX user account. The username does not need to match your Windows username.
For more information visit: https://aka.ms/wslusers
Enter new UNIX username: >> wsl2user

>> forgot password > hence uninstalled ubuntu and now re-installing from MS Store.
installed from MS store:
>C:\wsl2>wsl --set-default-version 2
For information on key differences with WSL 2 please visit https://aka.ms/wsl2
The operation completed successfully.

C:\wsl2>wsl --list -o
The following is a list of valid distributions that can be installed.
Install using 'wsl.exe --install <Distro>'.

NAME            FRIENDLY NAME
Ubuntu          Ubuntu
Debian          Debian GNU/Linux
kali-linux      Kali Linux Rolling
openSUSE-42     openSUSE Leap 42
SLES-12         SUSE Linux Enterprise Server v12
SLES-15         SUSE Linux Enterprise Server v15
Ubuntu-18.04    Ubuntu 18.04 LTS
Ubuntu-20.04    Ubuntu 20.04 LTS

C:\wsl2>wsl --install Ubuntu-20.04
Ubuntu 20.04 LTS is already installed.
Launching Ubuntu 20.04 LTS...

error : can't find file specified. <Fix by enabling wsl2 via control panel -> wsl2

C:\wsl2>wsl -l -v
  NAME            STATE           VERSION
* Ubuntu-20.04    Stopped         2

C:\wsl2>wsl --set-version Ubuntu-20.04 2
For information on key differences with WSL 2 please visit https://aka.ms/wsl2
Conversion in progress, this may take a few minutes.
The distribution is already the requested version.

C:\wsl2>wslconfig /u Ubuntu-20.04
Unregistering.
The operation completed successfully.

C:\wsl2>wsl --install -d Ubuntu-20.04
Ubuntu 20.04 LTS is already installed.
Launching Ubuntu 20.04 LTS...

Installing, this may take a few minutes...
Please create a default UNIX user account. The username does not need to match your Windows username.
For more information visit: https://aka.ms/wslusers
Enter new UNIX username: wsl2user
New password:
Retype new password:
passwd: password updated successfully
Installation successful!
To run a command as administrator (user "root"), use "sudo <command>".
See "man sudo_root" for details.

Welcome to Ubuntu 20.04.3 LTS (GNU/Linux 5.10.93.2-microsoft-standard-WSL2 x86_64)

wsl2user@apks1318:~$ sudo apt list --upgradable
[sudo] password for wsl2user:
Listing... Done
wsl2user@apks1318:~$ sudo apt upgrade
Reading package lists... Done
Building dependency tree
Reading state information... Done
Calculating upgrade... Done
0 upgraded, 0 newly installed, 0 to remove and 0 not upgraded.
wsl2user@apks1318:~$ sudo apt update
---
do regular update and upgrade
> sudo apt update && sudo apt upgrade

C:\wsl2>wsl --set-default-version 2
For information on key differences with WSL 2 please visit https://aka.ms/wsl2
The operation completed successfully.

C:\wsl2>wsl --set-default Ubuntu-20.04 2
The operation completed successfully.

C:\wsl2>wsl --set-version Ubuntu-20.04 2
For information on key differences with WSL 2 please visit https://aka.ms/wsl2
Conversion in progress, this may take a few minutes.
The distribution is already the requested version.

C:\wsl2>wsl -l -v
  NAME            STATE           VERSION
* Ubuntu-20.04    Running         2

How to Upgrade WSL 2 or 1 Ubuntu 20.04 to 22.04 LTS
https://www.how2shout.com/linux/how-to-upgrade-wsl-2-or-1-ubuntu-20-04-to-22-04-lts/

sudo apt update
sudo apt upgrade
sudo apt dist-upgrade
sudo apt install update-manager-core
#Edit release-upgrades configuration file using the below-given command: prompt=lts
sudo nano /etc/update-manager/release-upgrades

Upgrade to Ubuntu 20.04 (Focal Fossa) to Ubuntu 22.04 (Jelly Fish)
>sudo do-release-upgrade -d

After running the above command, the system will update and replace the system repository and after that, once the system is ready to get upgraded, you will ask finally whether you want to upgrade or not. If you have changed your mind then type ‘n‘ and the system will roll back all the made changes.

Once the installation of the new Jammy Jelly Fish is completed, remove the obsolete packages to clear some space by pressing Y and hitting the Enter key.

Once done, the WSL Ubuntu App will ask you to restart the system. However, it has not been started as an init system, so that will not be possible. Therefore, simply close the WSL app window and open it again.

Check Ubuntu 22.04 WSL version
wsl2user@apks1318:~$ cat /etc/os-release
PRETTY_NAME="Ubuntu Jammy Jellyfish (development branch)"
NAME="Ubuntu"
VERSION_ID="22.04"
VERSION="22.04 (Jammy Jellyfish)"
VERSION_CODENAME=jammy
ID=ubuntu
ID_LIKE=debian
HOME_URL="https://www.ubuntu.com/"
SUPPORT_URL="https://help.ubuntu.com/"
BUG_REPORT_URL="https://bugs.launchpad.net/ubuntu/"
PRIVACY_POLICY_URL="https://www.ubuntu.com/legal/terms-and-policies/privacy-policy"
UBUNTU_CODENAME=jammy
wsl2user@apks1318:~$


##Install Buildah.........
# Ubuntu 20.10 and newer -> ok as upgraded from 20.04 -> 22.04
sudo apt-get -y update
sudo apt-get -y install buildah

>wsl2user@apks1318:~$ buildah --version
buildah version 1.23.1 (image-spec 1.0.1, runtime-spec 1.0.2-dev)


##Install Podman
Podman is a daemonless container engine for developing, managing, and running OCI Containers on your Linux System.
https://computingforgeeks.com/how-to-install-podman-on-ubuntu/

> sudo apt install podman

wsl2user@apks1318:~$ podman images
WARN[0000] "/" is not a shared mount, this could cause issues or missing mounts with rootless containers
REPOSITORY  TAG         IMAGE ID    CREATED     SIZE

wsl2user@apks1318:~$ podman --version
podman version 3.4.4

wsl2user@apks1318:~$ podman pull hello-world
Resolved "hello-world" as an alias (/etc/containers/registries.conf.d/shortnames.conf)
Trying to pull docker.io/library/hello-world:latest...
Getting image source signatures
Copying blob 2db29710123e done
Copying config feb5d9fea6 done
Writing manifest to image destination
Storing signatures
feb5d9fea6a5e9606aa995e879d862b825965ba48de054caab5ef356dc6b3412

wsl2user@apks1318:~$ podman images
REPOSITORY                     TAG         IMAGE ID      CREATED       SIZE
docker.io/library/hello-world  latest      feb5d9fea6a5  5 months ago  19.9 kB

wsl2user@apks1318:~$ podman info
host:
  arch: amd64
  buildahVersion: 1.23.1
  cgroupControllers: []
  cgroupManager: cgroupfs
  cgroupVersion: v1
  conmon:
    package: 'conmon: /usr/bin/conmon'
    path: /usr/bin/conmon
    version: 'conmon version 2.0.25, commit: unknown'
  cpus: 8
  distribution:
    codename: jammy
    distribution: ubuntu
    version: "22.04"
  eventLogger: file
  hostname: apks1318
  idMappings:
    gidmap:
    - container_id: 0
      host_id: 1000
      size: 1
    - container_id: 1
      host_id: 100000
      size: 65536
    uidmap:
    - container_id: 0
      host_id: 1000
      size: 1
    - container_id: 1
      host_id: 100000
      size: 65536
  kernel: 5.10.93.2-microsoft-standard-WSL2
  linkmode: dynamic
  logDriver: k8s-file
  memFree: 14321631232
  memTotal: 16644096000
  ociRuntime:
    name: crun
    package: 'crun: /usr/bin/crun'
    path: /usr/bin/crun
    version: |-
      crun version 0.17
      commit: 0e9229ae34caaebcb86f1fde18de3acaf18c6d9a
      spec: 1.0.0
      +SYSTEMD +SELINUX +APPARMOR +CAP +SECCOMP +EBPF +YAJL
  os: linux
  remoteSocket:
    path: /mnt/wslg/runtime-dir/podman/podman.sock
  security:
    apparmorEnabled: false
    capabilities: CAP_CHOWN,CAP_DAC_OVERRIDE,CAP_FOWNER,CAP_FSETID,CAP_KILL,CAP_NET_BIND_SERVICE,CAP_SETFCAP,CAP_SETGID,CAP_SETPCAP,CAP_SETUID,CAP_SYS_CHROOT
    rootless: true
    seccompEnabled: true
    seccompProfilePath: /usr/share/containers/seccomp.json
    selinuxEnabled: false
  serviceIsRemote: false
  slirp4netns:
    executable: /usr/bin/slirp4netns
    package: 'slirp4netns: /usr/bin/slirp4netns'
    version: |-
      slirp4netns version 1.0.1
      commit: 6a7b16babc95b6a3056b33fb45b74a6f62262dd4
      libslirp: 4.6.1
  swapFree: 4294967296
  swapTotal: 4294967296
  uptime: 1h 23m 30.98s (Approximately 0.04 days)
plugins:
  log:
  - k8s-file
  - none
  - journald
  network:
  - bridge
  - macvlan
  volume:
  - local
registries: {}
store:
  configFile: /home/wsl2user/.config/containers/storage.conf
  containerStore:
    number: 0
    paused: 0
    running: 0
    stopped: 0
  graphDriverName: overlay
  graphOptions:
    overlay.mount_program:
      Executable: /usr/bin/fuse-overlayfs
      Package: 'fuse-overlayfs: /usr/bin/fuse-overlayfs'
      Version: |-
        fusermount3 version: 3.10.5
        fuse-overlayfs: version 1.7.1
        FUSE library version 3.10.5
        using FUSE kernel interface version 7.31
  graphRoot: /home/wsl2user/.local/share/containers/storage
  graphStatus:
    Backing Filesystem: extfs
    Native Overlay Diff: "false"
    Supports d_type: "true"
    Using metacopy: "false"
  imageStore:
    number: 1
  runRoot: /mnt/wslg/runtime-dir/containers
  volumePath: /home/wsl2user/.local/share/containers/storage/volumes
version:
  APIVersion: 3.4.4
  Built: 0
  BuiltTime: Thu Jan  1 05:30:00 1970
  GitCommit: ""
  GoVersion: go1.17.3
  OsArch: linux/amd64
  Version: 3.4.4

What Next:???
https://computingforgeeks.com/using-podman-and-libpod-to-run-docker-containers/
https://computingforgeeks.com/run-docker-podman-containers-as-systemd-service/
https://computingforgeeks.com/create-docker-container-registry-with-podman-letsencrypt/
https://computingforgeeks.com/how-to-install-harbor-docker-image-registry-on-centos-debian-ubuntu/
https://computingforgeeks.com/harbor-registry-ldap-integration/
https://computingforgeeks.com/how-to-prevent-users-from-creating-projects-in-harbor-registry/
