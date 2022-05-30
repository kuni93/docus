# AWS EC2

aws ec2 faq and some tips.


## Time sync when security group deny all outbound

在關閉所有對外連線或沒有網際網路的狀況下，VM 會無法進行時間同步。
AWS 預留了一個 Link-local address 可在此情況下提供時間同步的服務。

### Use chrony

1. Edit `/etc/chrony.conf`, and add following line.

```
server 169.254.169.123 prefer iburst minpoll 4 maxpoll 4
```


2. Restart the `chrony` daemon (`chronyd`).

```
$ sudo service chronyd restart
```


3. Verify that `chrony` is using the `169.254.169.123` IP address to synchronize the time.

```
$ chronyc sources -v
```


### Reference

- 正體中文： https://docs.aws.amazon.com/zh_tw/AWSEC2/latest/UserGuide/set-time.html
- English: https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/set-time.html

