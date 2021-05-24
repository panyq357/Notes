# 用windows启动盘的命令行重建EFI分区

首先，制作一个 windows 启动盘，镜像用微软官网上的就可以，如果电脑只剩一个 linux 能进的话，用 ``dd`` 命令直接制作也行。

然后，用这个启动盘启动，在进入到 windows 的安装界面时，不进行安装，而是按 ``Shift`` + ``F10``，启动命令行。（或者点“修复电脑”，再启动命令行也行。

在命令行中输入 ``diskpart``，回车，以启动 DISKPART 软件。

然后按步骤用下面的命令重建一个空的 EFI 分区。

```txt
diskpart
list disk
select disk <N1> # <N1> 是刚才列出的硬盘中电脑的硬盘对应的数字
list partition
select partition <N2> # 如果要新建一个 EFI 分区，<N2> 是代表要缩小的分区的数字（要从别的分区挤一点空间出来）。如果是覆盖原来的 EFI 分区，这里直接选原来的分区，后面的 shrink 和 create 操作也不用了。
shrink desired=100
create partition efi size=100
format quick fs=fat32
assign letter=s # 给刚建的 EFI 分区分个盘符，这里是 S
list partition # 最后记一下两个盘符：一个是原 Windows 的安装位置（通过分区大小判断），另一个是刚创建的 EFI 分区
exit
```

最后用下面的命令把启动 Windows 用的配置给复制进新的 EFI 分区内。

```
bcdboot X:\windows /s S: # 这里把 X 换成刚才记的原 Windows 的安装位置的盘符，S 就是刚创建的 EFI 分区的盘符
```

如果提示复制成功，则可以重启电脑了，重启后会自动进入 Windows。

如果提示错误，可能是盘符记错了，重新检查以下把。

参考：<https://www.tenforums.com/installation-upgrade/52837-moving-recreating-efi-partition-5.html?s=9b9d2b8107fc65df616011382408d563&__cf_chl_jschl_tk__=2d264d3b7502022fbdb9e0d925fba9f854215b87-1615508083-0-AZxZRDI2anqQdNAKiskILhu1XRH23ErLCQo8J3vNx9rvMJbTUu4y5RY3ApCOS_kZPWL1sOgDmJGr4oqVkR53twR5KTPtx_wYZyeUU2g9ihyX9kEdu2fy9kCEfNTzaJdEH5414xBHNPHYyMlXQbZeg_YgiiL_2bKG3KW5a3dIbnF-x6VGNFSU6G9Ngd3b6-Mpg2hECm5LlgNn4FfFNYmCvx0qiJlEQLSvq-5sZWvibj-85RuePgtL2wFlN3lMo0KyTmhFnuvjwqO4n7Qo53zzBg2RmpyYo_bvMvMHgVe2CKALGnzCI9a4Y5IGr47oOEfFcV0L2Zb2DNSp5K--mxjLl09nd69zD97XpbLhwwsKGbSIEYS1U-2BKIOqr2KRbK3geyfmcyRG62aO20IzUzXuAj_odPsy_m9bn-tQfQUIVxz_vCaWHN3ddVChLd0uLaFYIxBDrpLdWoMTGir4FpM835s>