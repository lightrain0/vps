
###V2ray 
v2ray.sh /usr/local/v2ray/config.json
VLESS + WS + TLS 端口：8443
服务: v2ray.service
配置文件：见config.json
###XRay
安装： bash -c "$(curl -L https://github.com/XTLS/Xray-install/raw/main/install-release.sh)" @ install
xray run -config /usr/local/etc/xray/config.json
VLESS + XTLS + REALITY 端口：18443
服务: xray.service
配置文件：
{
    "inbounds": [
        {
            "port": 18443,
            "protocol": "vless",
            "settings": {
                "clients": [
                    {
                        "id": "59a6aa38-285d-430d-a5e1-aed39322bf20", 
                        "flow": "xtls-rprx-vision"
                    }
                ],
                "decryption": "none"
            },
            "streamSettings": {
                "network": "tcp",
                "security": "reality",
                "realitySettings": {
                    "show": false,
                    "dest": "www.microsoft.com:443",
                    "xver": 0,
                    "serverNames": [
                        "www.microsoft.com"
                    ],
                    "privateKey": "SDVkAyOUqtIbp681DZSJN0_ynnkaOOcN47FDaiYrqW8",
                    "shortIds": [
                        "5e999147" 
                    ]
                }
            }
        }
    ],
    "outbounds": [
        {
            "protocol": "freedom",
            "tag": "direct"
        }
    ]
}
配置文件检查：
xray run -test /usr/local/etc/xray/config.json
Key:
 ./xray x25519
PrivateKey: SDVkAyOUqtIbp681DZSJN0_ynnkaOOcN47FDaiYrqW8
Password: lcShmXVSTx7rRbkvHS3JNvIXs53XmurqFkVClvneCEk
Hash32: baBD3uJFE_taMrFtZuXwsP9Slb4vzITnLDUwW6MgjiI
shareID:
openssl rand -hex 4
5e999147
###客户端：
类型: VLESS
地址: 你的服务器 IP
端口: 18443
UUID: 你填在 config.json 里的那个
传输方式: tcp
TLS: 开启
流控 (Flow): xtls-rprx-vision
Reality: 开启
SNI: www.microsoft.com
PublicKey: lcShmXVSTx7rRbkvHS3JNvIXs53XmurqFkVClvneCEk
Short ID: 5e999147
