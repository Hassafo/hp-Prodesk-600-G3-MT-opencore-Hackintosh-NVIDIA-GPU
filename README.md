# Hackintosh hp Prodesk 600 G3 MT Opencore

### Opencore 0.9.2 - macOS Monterey 12.6.6
WITH NVIDIA dGPU ACCELERATION

#### Features:

- native CPU and iGPU Power management
- Metal acceleration for Nvidia GT 730 dGPU
- Dual GPU configuration, Intel HD 530 for video decoding and Nvidia GT 730 for display
- Displayport at iGPU & dGPU
- USB Ports
- Speakers & Audio Output (backside)
- Displayport Audio
- Sleep and Wake
- Ethernet
- SATA drive supported
- SIP is disabled in config.pl
- VGA not tested

#### Not working yet:

- Native power management for Nvidia GT 730
- Writing NVRAM (blocked with boot-arg `rtcfx_exclude=00-FF`). 


### 2. Specs

* Chipset Q270
* Intel i5-6500
* HD 530 iGPU
* Nvidia GT 730 2GB
* SATA SSD
* SMBIOS: iMac 17,1 (same CPU and also dual-GPU machine) 



## IMPORTANT FOR INSTALLATION:


**My EFI folder contains two *config* files. The ***config_intel.plist*** is for installation and the other one for getting dual gpu configuration.
First, rename ***config.plist*** to `config_intel.plist` for installation and booting, having your monitor connected to the iGPU and BIOS set to use the Intel iGPU.
Then follow this: **

###  NVIDIA GPU PATCHING (Post-install)
1. Get [KeplerPatcher](https://github.com/chris1111/Geforce-Kepler-patcher/releases/tag/V7)	
2. Open it and follow the instructions. SIP should already be disabled by the config.plist.
3. Reboot
4. Use the `config_nvidia.plist` now (rename it to `config.plist`) and shutdown.
5. Switch your DP cable to the port of the Nvidia GPU
6. Boot
7. You now have full acceleration on the Nvidia GPU!

Don't forget to set your own platform info.




