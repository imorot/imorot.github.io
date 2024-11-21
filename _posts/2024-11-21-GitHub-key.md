---
title: "GitHub 2fa验证码生成"
permalink: "/GitHub/"
layout: post
---

```
pip3 install pyotp
```

```
import pyotp  
import time  
  
# 设置服务端密钥  
secret_key = "Github服务端生成的密钥（即二维码）"  
  
# 使用密钥和时间间隔（默认为 30 秒）创建一个 TOTP 对象  
totp = pyotp.TOTP(secret_key)  
  
# 生成当前的 OTP  
current_otp = totp.now()  
print(f"当前OTP: {current_otp}")
```
参考：https://www.cnblogs.com/v3ucn/p/17736955.html


GitHub的2fa验证，需要下载微软软件APP，
然后去扫码，或者输入一个key
，获取验证码。问题是还得下载单独的软件，
那为啥微软软件能给我生成验证码，这明明是两个不想干的软件
，
说白了就是，GitHub首次让我扫码时候，服务器存这个扫码时候码的key，会永久保存，
然后我验证器软件，输入一次或者扫码也会保留，所以这俩key一样，比如都是awslasml
，然后，基于时间的一次性密码TOTP
说白了就是202405051800登录时候
GitHub那边知道我key是多少，这个时间点key是
awslasml202405051800
然后我的验证器我之前也写了
awslasml
那自然就是成了
awslasml202405051800
。
问题是那我开启2fa时候 这个码出现了，就是相当于暴露了key可能。

参考：
https://medium.com/skyler-record/%E7%B0%A1%E8%BF%B0-opt-%E8%88%87-totp-b37b07bb31a0

https://joykeepsflowin.com/posts/about-otp-hotp-and-totp/

https://cavalloj.medium.com/totp-secret-extraction-from-qr-codes-ee097b4c687f

https://www.cnblogs.com/v3ucn/p/17736955.html
https://zhufan.net/2023/10/05/%E6%89%8B%E5%8A%A8%E5%AF%BC%E5%87%BA-microsoft-authenticator-%E4%B8%AD%E7%9A%84%E5%AF%86%E9%92%A5/
