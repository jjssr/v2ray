安装或卸载
温馨提醒，此脚本默认屏蔽一些不友好的网站！(仅限轮子相关)

要求：Ubuntu 16+ / Debian 8+ / CentOS 7+ 系统
推荐使用 Debian 9 系统，脚本会自动启用 BBR 优化。
备注：不推荐使用 Debian 8 系统，因为 Caddy 申请证书可能会出现一些莫名其妙的问题
我们推荐使用 搬瓦工VPS，稳定，快速，针对中国线路专门优化，无须担心跑路，服务好，并且支持退款。
在这里可以找到 搬瓦工 VPS 套餐大全 ，优惠码在这里： 搬瓦工 VPS 优惠码
使用 root 用户输入下面命令安装或卸载

bash <(curl -s -L https://git.io/v2ray.sh)
如果提示 curl: command not found ，那是因为你的 VPS 没装 Curl
ubuntu/debian 系统安装 Curl 方法: apt-get update -y && apt-get install curl -y
centos 系统安装 Curl 方法: yum update -y && yum install curl -y
安装好 curl 之后就能安装脚本了

备注：安装完成后，输入 v2ray 即可管理 V2Ray
如果提示你的系统不支持此脚本，那么请尝试更换系统
v2ray默认配置文件在/etc/v2ray/conf.json，我们只需编辑这个文件并添加一行就行了：

vim /etc/v2ray/config.json

{
  "log" : {
    "access": "/var/log/v2ray/access.log",
    "error": "/var/log/v2ray/error.log",
    "loglevel": "warning"
  },
  "inbound": {
    "port": 21xxx,
    "protocol": "vmess",
        "listen":"12.34.56.78", <------就是这一行
    "settings": {
      "clients": [
        {
          "id": "e59b0cba-204c-4d58-85a5-xxxxxxxxxxxxxxx",
          "level": 1,
          "alterId": 64
        }
      ]
    }
  },
  "outbound": {
    "protocol": "freedom",
    "settings": {}
  },
  "outboundDetour": [
    {
      "protocol": "blackhole",
      "settings": {},
      "tag": "blocked"
    }
  ],
  "routing": {
    "strategy": "rules",
    "settings": {
      "rules": [
        {
          "type": "field",
          "ip": [
            "0.0.0.0/8",
            "10.0.0.0/8",
            "100.64.0.0/10",
            "127.0.0.0/8",
            "169.254.0.0/16",
            "172.16.0.0/12",
            "192.0.0.0/24",
            "192.0.2.0/24",
            "192.168.0.0/16",
            "198.18.0.0/15",
            "198.51.100.0/24",
            "203.0.113.0/24",
            "::1/128",
            "fc00::/7",
            "fe80::/10"
          ],
          "outboundTag": "blocked"
        }
      ]
    }
  }
将上述listen碱性中的12.34.56.78替换成真实IP，保存。
