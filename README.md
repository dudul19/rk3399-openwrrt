<div align="center">

## `💤 Rongpin King RK3399 - OpenWRT 🌟` *

`made with 🤍 from Mr dudul`

---

**My Device Gweh**

</div>

## Install OpenWRT

### Bahan
- Install rkdeveloptool (https://wiki.radxa.com/Rock3/install/rockchip-flash-tools)
- Download loader [here](https://github.com/dudul19/rk3399-openwrt/main/rk3399_loader_v1.27.126.bin)
- Download fw

### Carra Install Frimware
- Colok usb type C ke device
- Tekan tombol reset sebelum colok power
- jalankan perintah dibawah

```
#### Cek device
sudo rkdeveloptool ld

#### Hapus bootloader
sudo rkdeveloptool db rk3399_loader_v1.27.126.bin

#### Flash image
sudo rkdeveloptool wl 0x0 <image.img>

#### Reset device
sudo rkdeveloptool rd
```

> Apabila tidak terdeteksi atau terkena maskroom saat `rkdeveloptool ld`, jumper pin **resistor** dan **grounding** yang ada digambar lalu colok power

## Fix Repositories
- Fix opkg update
```
cat << 'EOF' > /etc/opkg/distfeeds.conf
src/gz immortalwrt_core https://downloads.immortalwrt.org/releases/23.05.4/targets/armsr/armv8/packages
src/gz immortalwrt_base https://downloads.immortalwrt.org/releases/23.05.4/packages/aarch64_generic/base
src/gz immortalwrt_luci https://downloads.immortalwrt.org/releases/23.05.4/packages/aarch64_generic/luci
src/gz immortalwrt_packages https://downloads.immortalwrt.org/releases/23.05.4/packages/aarch64_generic/packages
src/gz immortalwrt_routing https://downloads.immortalwrt.org/releases/23.05.4/packages/aarch64_generic/routing
src/gz immortalwrt_telephony https://downloads.immortalwrt.org/releases/23.05.4/packages/aarch64_generic/telephony
EOF

sed -i 's/option check_signature/# option check_signature/g' /etc/opkg.conf
sed -i 's/downloads.immortalwrt.org/mirror.sjtu.edu.cn\/immortalwrt/g' /etc/opkg/distfeeds.conf
opkg update
```

## Fix Vnstat2
- Fix vnstat/ baandwith monitor reset jika reboot
```
mkdir /etc/vnstat
/etc/init.d/vnstat stop
rm -rf /etc/vnstat
cp -r /var/lib/vnstat /etc/vnstat

sed -i '/exit 0/i \
rm -rf /var/lib/vnstat\n\
ln -s /etc/vnstat /var/lib/vnstat\n\
/etc/init.d/vnstat restart\n' /etc/rc.local

rm -rf /var/lib/vnstat
ln -s /etc/vnstat /var/lib/vnstat
/etc/init.d/vnstat restart
```

## Tools Tambahan
- Bandix [here](https://github.com/dudul19/rk3399-openwrt/main/rk3399_loader_v1.27.126.bin)
- DW5821e Tools [here](https://github.com/dudul19/rk3399-openwrt/main/rk3399_loader_v1.27.126.bin)
- Tiny File Manager [here](https://github.com/dudul19/rk3399-openwrt/main/rk3399_loader_v1.27.126.bin)
- Latest Modem Manager [here](https://github.com/dudul19/rk3399-openwrt/main/rk3399_loader_v1.27.126.bin)

## Script IP Hunter
- Default ip hunter 10.1.xx - 10.16.xx dan 10.130.xx - 10.159.xx
- Lokasi simpan di /root
- Start
- Stop


#### Credit

 > - [MrDudul](https://t.me/dudulrealnofek)

<div align="center">

  `made with 🤍 from Mr Dudul`

</div>
