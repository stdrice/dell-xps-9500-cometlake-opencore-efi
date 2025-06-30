# OpenCore EFI for Dell XPS 9500 (Comet Lake)
![img](https://files.catbox.moe/a94ha8.png)

# Specs
| Component | Specs |
| --------- | ----- |
| **Model** | Dell XPS 9500 |
| **SMBIOS** | MacBookPro16,1 |
| **macOS** | Sonoma (14), Sequoia (15) |
| **CPU** | Intel Core i7-10750H |
| **iGPU** | Intel UHD Graphics 630 |
| **dGPU** | NVIDIA GeForce GTX 1650Ti Mobile |
| **SSD** | Micron 2300s |
| **Display** | 1920x1200 |
| **Wi-Fi** | Intel Killer AX1650s |
| **Touchpad** | I2C Touchpad |
| **Soundcard** | Realtek ALC3281/ALC289 (layout-id: `13`) |
| **Fingerprint** | Shenzhen Goodix |

# Working
- iGPU with Graphics Acceleration
- Wi-Fi, Bluetooth
- Audio
- Multi display
- Keyboard, touchpad
- Brightness key
- USB ports
- Camera, microphone
- Sleep (S4 Sleep, actually hibernate)
- iServices
- You tell me

# Not working
- AirDrop (Intel wifi, itlwm)
- DRM barely working
- dGPU (NVIDIA Turing)
- S3 Sleep (Dell quirkiness)
- Fingerprint, Face unlock (No Apple T2 chip on Hackintosh)
- You tell me

# How to use?
- Setup BIOS:

| Setting | Option |
| ------- | ------ |
| SATA Operation | AHCI |
| Secure Boot | Disabled |
| Intel SGX | Disabled |
| SMM Security Migration | Disabled |
| Absolute/Computrace | Disabled |
| VT-d/VT for direct I/O | Disabled |

- Mod BIOS using [grub shell](https://github.com/XDleader555/grub_setup_var/releases) / [How to do](https://linustechtips.com/topic/1323151-dell-xps-9700-undervolting-the-complete-guide/)
```
setup_var PchSetup 0x16 0x00 # Disable RTC Memory Lock
setup_var CpuSetup 0x3E 0x00 # Disable CFG Lock
setup_var CpuSetup 0xDA 0x00 # Disable Overclocking Lock
```
- Clone this repo
- Copy EFI folder to your USB/EFI partition
- [Follow this guide](https://dortania.github.io/OpenCore-Post-Install/universal/iservices.html) to generate SMBIOS and fix iServices
- Use these commands to fix sleep
```
sudo pmset -a hibernatemode 25
sudo pmset -a standby 1
sudo pmset -a powernap 1
sudo pmset -a sleep 1
sudo pmset -a standbydelaylow 1
sudo pmset -a standbydelayhigh 1
sudo pmset -a womp 0
sudo pmset -a proximitywake 0
```
- Install [HeliPort](https://github.com/OpenIntelWireless/HeliPort) to control Wi-Fi
