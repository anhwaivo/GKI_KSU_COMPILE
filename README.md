things i changed :D :
- made susfs optional
- translated readme to english
- made the `kernel-a13-5.15.yml` only build for my phone's kernel version so if u want to fork, change the stuff in `kernel-a13-5.15.yml`

### This is a repository for automatically building GKI kernels

> For non-GKI kernels, you can try resources from [SukiSU Cloud Disk](https://alist.shirkneko.top), but they do not support OnePlus ColorOS 14 or 15.
>
> First-time users **must read** the following content carefully. Don’t waste others’ time due to laziness!
>
> Recent updates: 1. OnePlus 8 ELITE processor can use kernel 6.6 (untested). 2. Fixed compilation errors for these GKI versions: [5.10.(66, 81, 101), 5.15.(74, 94, 104)]
### Downloads
You can download your resources [here](https://github.com/zzh20188/GKI_KernelSU_SUSFS/releases).
1. About AnyKernel3.zip: Download and use directly!
- Then use flashing software, such as [HorizonKernelFlasher](https://github.com/libxzr/HorizonKernelFlasher/releases), to flash the kernel.
2. About boot.img: Download the one matching your kernel format (uncompressed, gz, lz4). Refer to [this section](https://kernelsu.org/en_US/guide/installation.html#install-by-kernelsu-boot-image) **Finding the appropriate boot.img**.
- Flash using [FASTBOOT](https://magiskcn.com/) or use flashing software to flash to the boot partition of the ROOT slot (e.g., AiWanJi, KernelFlasher).

### Supported Features
| Feature | Description |
| --- | --- |
| [KernelSU](https://kernelsu.org/en_US/) | Includes **Original, MKSU, SUKISU, NEXT** |
| [SUSFS4](https://gitlab.com/simonpunk/susfs4ksu) | Kernel-level patch to assist KSU hiding functionality |
| [BBR](https://blog.thinkin.top/archives/ke-pu-bbrdao-di-shi-shi-me) | TCP congestion control algorithm, making the network faster? |
| [Wireguard](https://zh.wikipedia.org/wiki/WireGuard) | Refer to the wiki link on the left |
| [LZ4KD](https://github.com/ShirkNeko/SukiSU_patch/tree/main/other) | ZRAM algorithm reportedly from HUAWEI source, ported by [YuncaiZhiFeng](http://www.coolapk.com/u/24963680) |

<details>

<summary>Also supports these algorithms, switchable in Scene’s ZRAM settings</summary>

### LZ4K, LZ4HC, deflate, 842, ~~zstdn~~, lz4k_oplus

</details>

### KSU Manager
After compilation, you’ll see files like `Next-Manager(12600)`. In simple terms, this is the ***latest manager*** uploaded alongside the kernel.
![Example](./assets/get_manager.gif)
Similarly, the [Release](https://github.com/zzh20188/GKI_KernelSU_SUSFS/releases) also includes the ***latest manager***!
![Release](./assets/release_manager.gif)

### Emergency Rescue Guide

> [!IMPORTANT]
> **Trigger Conditions**  
> Perform a rescue when the device fails to boot due to:  
> - Flashing an incorrect/incompatible kernel  
> - Kernel version mismatch (e.g., flashing a 5.10.66 kernel with version 233)  
1. Enter FASTBOOT mode

- Physical key combination: Power + Volume Down, or ADB command: `adb reboot bootloader`

2. Execute the flashing command
```bash
$ fastboot flash boot <full_boot.img_filename>
```
### Obtaining Original Images
1. Extract from existing firmware

- OTA package: Extract and use the [payload-dumper tool](https://magiskcn.com/payload-dumper-go-boot.html)

- Flash package: Directly extract to obtain boot.img

2. External resource acquisition

- Search community platforms: Model + original boot (e.g., XDA/CoolApk)

- [Mobile online extraction and remote acquisition](https://magiskcn.com/payload-dumper-compose.html)

> [!TIP]
> ### Kernel Version Compatibility Notes
> 
> **1. Cross-subversion flashing rules**  
> When the phone’s GKI main version is 5.10.x (e.g., 5.10.168), you can flash a kernel with a higher subversion of the same main version (e.g., 5.10.198).  
> About **X-lts** versions, e.g., `android12-5.10.X-lts-AnyKernel3.zip`:  
> - **X-lts** indicates a long-term support version (highest subversion, currently 5.10.236 in this example).  
> - LTS versions increase with GKI source updates, while other versions like 198 are permanently fixed.  
> - ⚠️ Note: LTS is the latest, but **latest ≠ most stable** (e.g., 6.6.x has auto-reboot bugs).  
> 
> **2. Kernel version spoofing method**  
> In the MT Manager terminal, execute:  
> ```bash
> uname -r | sed 's/^[^-]*//'
> ```  
> Copy the obtained version number and enter it into the Action compilation panel to spoof the kernel version.  
> 
> **3. Compilation optimization suggestions**  
> Modify the [configuration file](.github/workflows/kernel-a12-5.10.yml) (e.g., kernel-a12-5.10.yml):  
> - ▶️ Delete/comment out unnecessary GKI version configurations (**speeds up compilation**).  
> - ➕ Add specific GKI versions (refer to the [customization guide](https://www.coolapk.com/feed/62820671?shareKey=OGMxYmZmNTk0YzIxNjgxNzM1MzI~&shareUid=11253396&shareFrom=com.coolapk.market_15.2.2)).  
> - 📅 Kernel build time, refer to the comments around **line 490** in the [gki-kernel.yml](.github/workflows/gki-kernel.yml) file for modifications.

### More Content
Feel free to share your suggestions... I’ll give it a try!
