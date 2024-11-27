

# 首頁

> GXDE ISO Builder 探索筆記

| Link | GitHub |
| ---- | ------ |
| [ISO Builder 探索筆記](https://samwhelp.github.io/note-about-iso-builder/) | [GitHub](https://github.com/samwhelp/note-about-iso-builder) |
| [GXDE ISO Builder 探索筆記](https://samwhelp.github.io/note-about-gxde-iso-builder/) | [GitHub](https://github.com/samwhelp/note-about-gxde-iso-builder) |




## 主題

* [實作案例](#實作案例)
* [Boot ISO By GRUB](#boot-iso-by-grub)
* [GXDE OS / Live System](#gxde-os--live-system)
* [相關筆記](#相關筆記)




## 實作案例

| 原始實作案例 |
| ------- |
| [gxde-iso-builder](https://github.com/GXDE-OS/gxde-iso-builder) |


| 衍生實作案例 | 備註 |
| ---------- | ---- |
| [gxde-iso-builder-remix](https://github.com/samwhelp/gxde-iso-builder-remix) | 小幅調整，加入自訂設定機制 |
| [gxde-iso-builder-refactoring](https://github.com/samwhelp/gxde-iso-builder-refactoring) | 重構程式碼，加入自訂設定機制 |




## Boot ISO By GRUB

> 將產出的「iso檔案」放置到「`/opt/iso/gxde/latest/gxde.iso`」這個路徑

> 產生一個檔案「`/boot/grub/custom.cfg`」，內容如下

``` sh
menuentry "GXDE OS" --class Debian {
	set iso_file="/opt/iso/gxde/latest/gxde.iso"
	search --set=iso_partition --no-floppy --file $iso_file
	probe --set=iso_partition_uuid --fs-uuid $iso_partition
	set img_dev="/dev/disk/by-uuid/$iso_partition_uuid"
	loopback loop ($iso_partition)$iso_file

	set extra_option=""
	#set extra_option="components quiet splash"

	set locale_option=""
	#set locale_option="locales=en_US.UTF-8"
	#set locale_option="locales=zh_TW.UTF-8"
	#set locale_option="locales=zh_CN.UTF-8"
	#set locale_option="locales=zh_HK.UTF-8"
	#set locale_option="locales=ja_JP.UTF-8"
	#set locale_option="locales=ko_KR.UTF-8"

	set boot_option="${locale_option} ${extra_option}"
	linux	(loop)/live/vmlinuz boot=live buuid=${iso_partition_uuid} findiso=${iso_file} ${boot_option}
	initrd	(loop)/live/initrd.img
}
```

> 重新開機後，就會在「GRUB」的開機選單，看到「`GXDE OS`」這個選項。




## GXDE OS / Live System

| Account  | Value  |
| -------- | ------ |
| Username | `user` |
| Password | `live` |

若想要移除目前帳號的密碼，可以執行下面指令

``` sh
sudo passwd -d $(whoami)
```




## 相關筆記

| Link | GitHub |
| ---- | ------ |
| [GXDE 探索筆記](https://samwhelp.github.io/note-about-gxde/) | [GitHub](https://github.com/samwhelp/note-about-gxde) |




## Samwhelp

* [個人筆記](https://samwhelp.github.io/book/)
