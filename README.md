# hp Prodesk 600 G3 MT Hackintosh with Opencore 0.9.2

### OC ver. 0.9.2 - macOS Monterey 12.6.6
WITH NVIDIA dGPU ACCELERATION

### Specs

* Chipset Q270
* CPU: Intel i5-6500
* iGPU: HD 530
* dGPU: Nvidia GT 730 2GB
* SATA SSD
* SMBIOS: iMac 17,1 (same CPU and also dual-GPU machine) 
* If you want to use Ventura, use iMac18,1. 


#### Features:

- Native CPU and iGPU Power management
- Metal acceleration for Nvidia GT 730 dGPU
- Dual GPU configuration,
Intel HD 530 for video decoding and Nvidia GT 730 for display
- Displayport works for iGPU & dGPU
- USB Ports
- Speakers & Audio Output (backside)
- Displayport Audio
- Sleep and Wake
- Ethernet
- SATA drive support
- SIP is disabled in config.plist
- 
- VGA not tested

#### Not working yet:

- The frontside Audio Out (for headphones) und the Audio In on the backside don't work. I have only tried Alcid=28 so far with AppleALC (apple native audio). 
- Native power management for Nvidia GT 730. I tried with [this](https://elitemacx86.com/threads/how-to-enable-discrete-gpu-power-management-nvidia-amd.657/) guide, using [AGPMInjector Kext](https://github.com/Pavo-IM/AGPMInjector), but could nit get the `Heuristic-ID` of `04 00 00 00`, so I removed the Kext from the EFI. Feel free to try!

- Writing NVRAM (blocked with boot-arg `rtcfx_exclude=00-FF`): NVRAM is a big issue with this machine. Something with Opencore or macOS doesn't get along with the board's RTC-clock thing. After every boot with Opencore, you get `POST ERROR: Real-time clock power loss (005)`. Only SSDT-AWAC and the `rtcfx_exclude=00-FF` boot-arg can solve this. The boot-arg blocks any inteferance with the sectors, so NVRAM-dependent things like disabling SIP don't work. That is why I disabled it in the Config.plist. There is a possibility to look for the "bad" sectors with `rtcfx_exclude=XX-XX`, but I did not need it anyway. 





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

Any help for solving those few problems is welcome as well as my help for those struggling with this machine. 

Don't forget to set your own platform info.




