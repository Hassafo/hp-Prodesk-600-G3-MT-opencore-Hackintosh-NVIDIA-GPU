# hp Prodesk 600 G3 MT Hackintosh with NVIDIA GPU

### OC ver. 0.9.2 - macOS Monterey 12.6.6
WITH NVIDIA dGPU ACCELERATION

![](https://raw.githubusercontent.com/Hassafo/hp-Prodesk-600-G3-MT-opencore-Hackintosh/e58c3633a844947180995978023dda9449e4e494/Bildschirmfoto%202023-06-01%20um%2022.33.46.png))

![](https://raw.githubusercontent.com/Hassafo/hp-Prodesk-600-G3-MT-opencore-Hackintosh/e58c3633a844947180995978023dda9449e4e494/Bildschirmfoto%202023-06-01%20um%2022.35.10.png)

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
- All Audio ports and the speakers
- Displayport Audio
- Sleep and Wake
- Ethernet
- SATA drive support with TRIM. To be really sure, enable TRIM in terminal
- SIP is disabled in config.plist
- VGA not tested
- Wifi not tested. Will need a supported Wifi card with Kext.

#### Not working yet:
 
- Native power management for Nvidia GT 730. I tried with [this](https://elitemacx86.com/threads/how-to-enable-discrete-gpu-power-management-nvidia-amd.657/) guide, using the [AGPMInjector Kext](https://github.com/Pavo-IM/AGPMInjector), but could nit get the `Heuristic-ID` of `04 00 00 00`, so I removed the Kext from the EFI. Feel free to try!

- Writing NVRAM (blocked with boot-arg `rtcfx_exclude=00-FF`): NVRAM is a big issue with this machine. Something with Opencore or macOS doesn't get along with the board's RTC-clock thing. After every boot with Opencore, you get `POST ERROR: Real-time clock power loss (005)`. Only SSDT-AWAC and the `rtcfx_exclude=00-FF` boot-arg can solve this. The boot-arg blocks any inteferance with the sectors, so NVRAM-dependent things like disabling SIP don't work. That is why I disabled it in the Config.plist. There is a possibility to look for the "bad" sectors with `rtcfx_exclude=XX-XX`, but I don't need anyway. 
* ***So because of this, if you want Opencore to remember your boot choice in the picker, just hold CTRL while selecting your drive.***





## IMPORTANT FOR INSTALLATION

### Pre-install:

My EFI folder contains two *config* files. The `config_intel.plist` is only for installation and setup and the other one `config_nvidia.plist` is later for permanent use, enabling the Nvidia dGPU to be used after Kepler patching.

First, rename `config_intel.plist` to `config.plist`. Connect your monitor to the iGPU and set the BIOS to use the Intel iGPU. 

**BIOS Settings**:

* Intel Software Extension Guard SGX: `Disable`
* Secure Boot Configuration: `Legacy Support Disable and Secure Boot disable.` 
* Intel Vtd: `disabled`
* Intel VTx: `enabled`
* VGA Boot Device: `Intel VGA Controller`
* Video memory size: `64 MB` or more

Then follow the installation as in the opencore guide. Then, when you have macOS working:

###  NVIDIA GPU PATCHING (Post-install):

1. Get [KeplerPatcher](https://github.com/chris1111/Geforce-Kepler-patcher/releases/tag/V7)	
2. Open it and follow the instructions. SIP should already be disabled by the config.plist.
3. Reboot
4. Switch the current config.plist with the `config_nvidia.plist` by renaming the latter. 
5. Power off. 
6. Go to BIOS and set VGA boot device to NVIDIA VGA Controller. Switch your monitor cable now to the port of the Nvidia GPU.  
7. Boot
8. You now have full acceleration on the Nvidia GPU!

Any help for solving those few problems is welcome as well as my help for those struggling with this machine. 

Don't forget to set your own platform info.




