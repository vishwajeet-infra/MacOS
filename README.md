macOS Unlocker V4 for VMware Workstation
Important

The Unlocker project is now considered complete. What does this mean?

It is still completely functional including support for the latest VMware 26H1 release.
VMware have now deprecated macOS support so there should not be any changes to the code.
macOS 27 Golden Gate removes Intel support so we are at the end of the line for future macOS releases.
The Unlocker remains supported and should continue to run for the foreseeable future.

There is a project called OC4VM which allows macOS guests without patching VMware. It also supports AMD CPU based host systems. The project can be found here https://github.com/vishwajeet-infra/MacOS

1. Introduction
Unlocker 4 is designed for VMware Workstation and Player and has been tested against:

Workstation Pro 16/17/25/26 on Windows and Linux
Workstation Player 16/17/25/26 on Windows and Linux
The Unlocker enables certain flags and data tables that are required to see the macOS type when setting the guest OS type, and modify the implmentation of the virtual SMC controller device. These capabiltiites are normally exposed in Fusion and ESXi when running on Apple hardware.

The patch code carries out the following modifications dependent on the product being patched:

Patch vmware-vmx and derivatives to allow macOS to boot
Patch vmwarebase.dll or libvmwarebase.so to allow Apple guests to be selected during VM creation
Provide a copy of the macOS VMware Tools for the guest
It is important to understand that the Unlocker cannot add any new capabilities to VMware Workstation and Player but enables support for macOS that is disabled in the VMware products that do not run on Apple hardware.

The Unlocker cannot:

add AMD CPU support
add support for new versions of macOS
add paravirtualized Apple GPU support
or any other features that are not already in the VMware compiled code.

2. Running the Unlocker
2.1 Download Release
The code is written in Go and has no pre-requisites and should run directly from the release zip download.

Download a binary release from https://github.com/vishwajeet-infra/MacOS
Optionally check the sha256 checksum matches that published in the release
Unzip (Windows) or untar (Linux) the archive to extract the executables and VMware Tools images
Navigate to the folder with the extracted files
2.2 Windows
On Windows you can double-click the executables to launch them from the "windows" folder. You may be prompted to run with Administrator rights which are required to patch VMware.

unlock.exe - apply patches to VMware
relock.exe - remove patches from VMware
check.exe - check the patch status of VMware
2.3 Linux
On Linux navigate to the folder where the unlocker has been unpacked, and run the required command from the "linux" folder. You will need to be either root or use sudo to run the scripts in the terminal.

unlock - apply patches to VMware
relock - remove patches from VMware
check - check the patch status of your VMware installation
2.3.1 Arch Linux and its derivatives
If you are using Arch Linux or a derivative of Arch, you can install and use this like any normal package from the AUR. Precompiled binaries and PKGBUILDs to build from the source of the latest release as well as from the main branch are provided. Included in all of the packages are some Pacman hooks to help unlock and relock VMware whenever there is an update to Unlocker, VMware Worksation Pro/Player, or any of VMware Workstation Pro/Player's components. The binary files are installed to the /usr/bin directory so they are already added to your $PATH.

2.4 Upgrading VMware
If a new VMware version is installed the patches will be lost as the update will overwrite the patched files. You will need to re-run the unlock program to patch the newly installed VMware files. This does not apply to the Arch Linux AUR packages due to the provided ALPM hooks.

2.5 VMware Tools
The Unlocker provides the VMware tools ISO images. Version 16/17/25/26 of Workstation Pro recognises the darwin.iso files and the tools can be installed in the usual way by using the "Install VMware Tools" menu item. The Player version does not automatically pick up the ISO images and so the ISO must be maually attached to the VM via the guest's settings.
