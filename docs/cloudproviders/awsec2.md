# AWS EC2

aws ec2 faq and some tips.


## Time sync when deny any outbound

在關閉所有對外連線的狀況下，VM 會無法進行時間同步。
AWS 預留了一個 Link-local address 可在此情況下提供時間同步的服務。

### Use chrony

1. Edit `/etc/chrony.conf`, and add following line.

```bash
server 169.254.169.123 prefer iburst minpoll 4 maxpoll 4
```


2. Restart the `chrony` daemon (`chronyd`).

```bash
$ sudo service chronyd restart
```


3. Verify that `chrony` is using the `169.254.169.123` IP address to synchronize the time.

```bash
$ chronyc sources -v
```


### Ref.

- 中文文件： https://docs.aws.amazon.com/zh_tw/AWSEC2/latest/UserGuide/set-time.html
- 原文文件： https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/set-time.html

