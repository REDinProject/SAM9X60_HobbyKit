# SAM9X60_HobbyKit
## Buildroot
**Get Buildroot for AT91 sources**
```bash
mkdir ~/Linux4Microchip
cd ~/Linux4Microchip

git clone https://github.com/linux4sam/buildroot-at91.git -b linux4sam-2022.10
git clone https://github.com/linux4sam/buildroot-external-microchip.git -b linux4microchip-2022.10

cd buildroot-external-microchip/
git checkout linux4microchip-2022.10 -b buildroot-external-microchip-linux4microchip-2022.10
cd ../buildroot-at91/
git checkout linux4sam-2022.10 -b buildroot-at91-linux4sam-2022.10
```
**Build the rootfs image**
```bash
export PATH=/usr/sbin:/usr/bin:/sbin:/bin
cd ~/Linux4Microchip/buildroot-at91/
BR2_EXTERNAL=../buildroot-external-microchip/ make sam9x60_curiosity_graphics_defconfig make

ls ./output/images/
```
**Adding/removing packages from the rootfs**
```bash
make menuconfig
```
**Configure the U-Boot or Linux kernel**
```bash
make uboot-menuconfig
make linux-menuconfig
```
**Rebuild**
```bash
make uboot-rebuild
```
```bash
make linux-rebuild
make dt-overlay-mchp-rebuild
```  
**Build the SDK (optional)**
```bash
export PATH=/usr/sbin:/usr/bin:/sbin:/bin
cd ~/Linux4Microchip/buildroot-at91/
make sdk

ls ./output/images/
```

**Install the SDK (optional)**
```bash
cd ~/Linux4Microchip/
tar -xvf arm-buildroot-linux-gnueabi_sdk-buildroot.tar.gz
./arm-buildroot-linux-gnueabi_sdk-buildroot/relocate-sdk.sh
find ./arm-buildroot-linux-gnueabi_sdk-buildroot -name arm-buildroot-linux-gnueabi-gcc
```

## Cross-compiler and Execute program
**Compile the executable file for SAM9X60 MPU**
```bash
~/Linux4Microchip/buildroot-at91/output/host/bin/arm-buildroot-linux-gnueabi-gcc test.c -o test
```

**Add executable permissionsm (Platform)**
```bash
chmod +x ./test
```
**Execute program (Platform)**
```bash
./test
```

## Transfer file
### Send using XMODEM
**Waiting to receive (Platform)**  
```bash
rx test
```
**[Tera Term]** -> File -> Transfer -> XMODEM -> Send...  

### Send via Ethernet
```bash
scp test root@192.168.1.1:/root
```
