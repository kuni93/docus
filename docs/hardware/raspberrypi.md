# Raspberry Pi

Raspberry Pi faq and some tips.


## Free swap

部分型號記憶體較小，記憶體用量突增時同時有可能將 swap 吃滿（預設 100 MB）觸發到系統警報。
除了增加 swap 大小外，在確保記憶體充足時，可將 swap off & on 來手動排空 swap。


### swap off & on

透過以下指令關閉（排空）後重新開啟

```
$ sudo dphys-swapfile swapoff
$ sudo dphys-swapfile swapon
```

透過以下指令檢查記憶體跟 swap 的狀態

```
$ free -h
```

