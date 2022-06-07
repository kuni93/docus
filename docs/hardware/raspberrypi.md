# Raspberry Pi

Raspberry Pi faq and some tips.


## SD card overclock

為了確保記憶卡的相容性，預設設定會限制性能較好記憶卡的讀寫速度，透過以下設定可以釋放更多性能。

:::danger WARNING!

以下步驟僅在 Raspberry Pi 3 B+ & Raspberry Pi OS (Raspbian) 64-bit 2022-04-04 版本測試及使用。且不保證所有硬體皆相容該設定，請自行評估相關操作的硬體損壞風險。

:::


### Step

1. Edit `/boot/config.txt`, and add following line.

```txt title='/boot/config.txt'
dtparam=sd_overclock=100
```

2. Reboot Raspberry Pi, and verify.

```bash
dmesg | grep "mmc0"
```

有出現類似下列訊息，即成功生效

```bash
[    3.252648] mmc0: overclocking to 100000000Hz
```

亦可透過 dd 測試速度是否有提昇

```bash
# write ~= 1 GB
dd if=/dev/zero of=test bs=1M count=1024

# read ~= 1 GB
dd if=test of=/dev/null bs=1M
```


## Free swap

部分型號記憶體較小，記憶體用量突增時同時有可能將 swap 吃滿（預設 100 MB）觸發到系統警報。
除了增加 swap 大小外，在確保記憶體充足時，可將 swap off & on 來手動排空 swap。


### Step

swap off & on

```bash
sudo dphys-swapfile swapoff && sudo dphys-swapfile swapon
```

亦可透過以下指令檢查記憶體跟 swap 的狀態

```bash
free -h
```

