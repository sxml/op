![OPhub logo](/logo.png)


# Automatically Build OpenWrt

The latest version of the OpenWrt firmware is automatically compiled every Monday, which can be downloaded in [Action](https://github.com/ophub/op/actions). Will be updated to latest in every Monday [Releases](https://github.com/ophub/op/releases). For detailed information about each firmware, please refer to the README.md file of each model. The currently supported router models are: 

- [Linksys WRT1900ACS](https://github.com/ophub/op/tree/master/router/linksys_wrt1900acs)
- [Linksys WRT3200ACM](https://github.com/ophub/op/tree/master/router/linksys_wrt3200acm)
- [Linksys WRT32X](https://github.com/ophub/op/tree/master/router/linksys_wrt32x)
- [x64](https://github.com/ophub/op/tree/master/router/x64)
- [Phicomm N1](https://github.com/ophub/op/tree/master/router/phicomm_n1)

## Usage

* Related script usage instructions:

There are currently two DIY scripts in the root directory of the warehouse: `diy-part1.sh`, `diy-part2.sh` and `.config`, which are executed before and after the update and installation of ` ./scripts/feeds update && ./scripts/feeds install `. You can write the instructions for modifying the source code into the script, such as modifying `the default IP , Host name, theme, add/remove software package...`, etc. If the additional software package has the same name as the existing software package in the OpenWrt source code, the software package with the same name in the Open­Wrt source code needs to be deleted, otherwise the packages in Open­Wrt will be compiled first. It will automatically traverse all files in the `package` directory when compiling.


Just put the `feeds.conf.default` file into the root directory of the warehouse, it will overwrite the relevant files in the Open­Wrt source directory. Create a new `files` directory under the root directory of the warehouse, and put the customized related files in the same directory structure as OpenWrt, and the OpenWrt configuration will be overwritten during compilation.


Set `SSH_ACTIONS: true` to use tmate to connect to the `GitHub Actions` virtual server environment. You can directly perform the `make menuconfig` operation to generate the compilation configuration, or any customized operation. After triggering the workflow, wait for the `SSH connection to Actions` step to be executed on the `Actions` page, and then the following three lines of messages will be displayed: 1.` To connect to this session copy-n-paste the following into a terminal or browser: `, 2.***` ssh Y26QenMRd@nyc1.tmate.io `***, 3.***` https://tmate.io/t/Y26QenMRd `***. Then copy the `SSH connection command` and paste it into `the terminal` for execution, or copy `the link` to open it in `the browser` and use `the web terminal`. enter the command: ***` cd openwrt && make menuconfig `*** for personalized configuration (The web terminal may encounter a black screen, just press ***`Ctrl+C`***). After completion, press the shortcut key ***` Ctrl+D `*** or execute the ***` exit `*** command to exit, and the subsequent compilation work will proceed automatically.

* router/${firmware} Function description of related files in each firmware package:

| Folder/file name | Features |
| ---- | ---- |
| .config | Firmware related configuration, such as firmware kernel, file type, software package, luci-app, luci-theme, etc. |
| files | Create a files directory under the root directory of the warehouse and put the relevant files in. You can use custom files such as network/dhcp/wireless by default when compiling. |
| feeds.conf.default | Just put the feeds.conf.default file into the root directory of the warehouse, it will overwrite the relevant files in the OpenWrt source directory. |
| diy-part1.sh | Execute before updating and installing feeds, you can write instructions for modifying the source code into the script, such as adding/modifying/deleting feeds.conf.default. |
| diy-part2.sh | After updating and installing feeds, you can write the instructions for modifying the source code into the script, such as modifying the default IP, host name, theme, adding/removing software packages, etc. |


## .github/workflow/${workflows_file}.yml files related environment variable description:

| Environment variable | Features |
| ---- | ---- |
| REPO_URL | Source code warehouse address |
| REPO_BRANCH | Source branch |
| FEEDS_CONF | Custom feeds.conf.default file name |
| CONFIG_FILE | Custom .config file name |
| DIY_P1_SH | Custom diy-part1.sh file name |
| DIY_P2_SH | Custom diy-part2.sh file name |
| SSH_ACTIONS | SSH connection Actions function. Default false |
| UPLOAD_BIN_DIR | Upload the bin directory (all ipk files and firmware). Default false |
| UPLOAD_FIRMWARE | Upload firmware catalog. Default true |
| UPLOAD_RELEASE | Upload firmware to release. Default true |
| UPLOAD_COWTRANSFER | Upload the firmware to CowTransfer.com. Default false |
| UPLOAD_WERANSFER | Upload the firmware to WeTransfer.com. Default failure |
| TZ | Time zone setting |
| ${{ secrets.GITHUB_TOKEN }} | 
1. control center → settings → Developer settings → Personal access tokens → Create token ( Name:GITHUB_TOKEN, Select: public_repo, Copy GITHUB_TOKEN's content). 
2. op code center  → settings → Secrets → Add a new secret → ( Name:RELEASES_TOKEN, Value: GITHUB_TOKEN's content). |

## Firmware information

| Name | Value |
| ---- | ---- |
| Default IP | 192.168.1.1 |
| Default username | root |
| Default password | password |
| Default WIFI name | OpenWrt |
| Default WIFI password | none |

## Catalog description

```shell script

 op
 ├── .github
 │   └── workflows                        
 │       ├── build-openwrt-linksys_wrt1900acs.yml      # Build Linksys WRT1900ACS firmware
 │       ├── build-openwrt-linksys_wrt3200acm.yml      # Build Linksys WRT3200ACM firmware
 │       ├── build-openwrt-linksys_wrt32x.yml          # Build Linksys WRT32X firmware
 │       ├── build-openwrt-x64.yml                     # Build X64 Virtual Machine firmware
 │       ├── build-openwrt-phicomm_n1.yml              # Build PHICOMM N1 firmware
 │       └── delete-older-releases.yml                 # Delete older releases
 │
 ├── router                                            # Related router Openwrt firmware codes 
 │   ├── linksys_wrt1900acs                            # Linksys WRT1900ACS related code files
 │   │   ├── .config                                   # config luci-app, luci-theme and other
 │   │   ├── diy-part1.sh                              # DIY script part 1(Before Update feeds)
 │   │   ├── diy-part2.sh                              # DIY script part 2(After Update feeds)
 │   │   └── README.md                                 # Instructions
 │   │
 │   ├── linksys_wrt3200acm                            # Linksys WRT3200ACM related code files
 │   │   ├── .config
 │   │   ├── diy-part1.sh
 │   │   ├── diy-part2.sh
 │   │   └── README.md
 │   │
 │   ├── linksys_wrt32x                                # Linksys WRT32X related code files
 │   │   ├── .config
 │   │   ├── diy-part1.sh
 │   │   ├── diy-part2.sh
 │   │   └── README.md
 │   │ 
 │   ├── x64                                           # x64 related code files
 │   │   ├── .config            
 │   │   ├── diy-part1.sh            
 │   │   ├── diy-part2.sh
 │   │   └── README.md
 │   │
 │   └── phicomm_n1                                    # PHICOMM N1 related code files
 │       ├── .config            
 │       ├── diy-part1.sh            
 │       ├── diy-part2.sh            
 │       ├── make                                      # Build script for PHICOMM N1
 │       ├── README.md
 │       │
 │       ├── armbian                                   # armbian related files
 │       │   ├── boot-common.tar.gz                    # Public startup file
 │       │   ├── firmware.tar.gz                       # armbian firmware
 │       │   └── phicomm-n1
 │       │       ├── kernel                            # Custom kernel folder 
 │       │       │   └── ${kernel}                     # Various versions of the kernel folder
 │       │       │       ├── kernel.tar.gz
 │       │       │       └── modules.tar.gz
 │       │       │
 │       │       └── root                              # Add your custom files(ROOTFS Partition)
 │       │    
 │       ├── build-n1-kernel                           # Build kernel for Phicomm-N1
 │       │   ├── make_use_img.sh                       # Use Flippy's *.img files build
 │       │   ├── make_use_kernel.sh                    # Use Flippy's kernel files build
 │       │   ├── README.md
 │       │   └── flippy
 │       │       ├── boot-${flippy_version}.tar.gz
 │       │       ├── dtb-amlogic-${flippy_version}.tar.gz
 │       │       ├── modules-${flippy_version}.tar.gz
 │       │       │ 
 │       │       └── or ${flippy_file} E.g: N1_Openwrt_*.img
 │       │     
 │       └── install-program                           # Install to emmc for PHICOMM N1
 │           ├── Makefile            
 │           └── files
 │               ├── fstab 
 │               ├── n1-install.sh                     # Install script
 │               ├── n1-update.sh                      # update script
 │               └── u-boot-2015-phicomm-n1.bin        # Recovery emmc partition script
 │
 ├── LICENSE                                           # LICENSE for OP
 └── README.md                                         # Instructions for OP
   
```
## Tips

The code Fork comes from the code bases of authors such as coolsnowwolf, P3TERX, tuanqing & flippy, etc.  I only did a simple router adaptability debugging. For more advanced usage, please go to the original author's github to learn.

## Acknowledgments

- [OpenWrt](https://github.com/openwrt/openwrt)
- [coolsnowwolf/lede](https://github.com/coolsnowwolf/lede)
- [Lienol/openwrt](https://github.com/Lienol/openwrt)

- [P3TERX/Actions-OpenWrt](https://github.com/P3TERX/Actions-OpenWrt)
- [tuanqing/mknop](https://github.com/tuanqing/mknop)

- [Mikubill/transfer](https://github.com/Mikubill/transfer)

## License

[OP](https://github.com/ophub/op/blob/master/LICENSE) © OPHUB
