# freqtrade-kucoin-proxy
Kucoin proxy for freqtrade that is using websockets to maintain candlestick/klines data in memory, thus having great
performance and reducing the amount of API calls to the Kucoin API. All other calls are proxied as usual.

### download
1. ```cd ~/freqtrade/```
2. ```wget https://github.com/mikekonan/freqtrade-proxy/releases/download/v1.0.11/freqtrade-proxy-linux-amd64```
3. ```sudo chmod +x freqtrade-proxy-linux-amd64```

### making it as service for autostart
1. ```cd /etc/systemd/system``` 
2. ```sudo nano prox-service.service``` 
3. ```copy the text below, in it```
```
[Unit]
Description=proxy freq autostart

[Service]
User=root
ExecStart=/root/freqtrade/freqtrade-proxy-linux-amd64 -port 8089
Restart=always

[Install]
WantedBy=multi-user.target
```
4. ```ctrl+s,ctrl+x```
5. ```sudo systemctl daemon-reload```

### starting the proxy service
6. ```sudo systemctl start prox-service.service```
### check for status
7. ```sudo systemctl status prox-service.service```


#### change config.json in root/freqtrade

```
    "exchange": {
        "name": "kucoin",
        "key": "",
        "secret": "",
        "ccxt_config": {
            "enableRateLimit": false,
            "timeout": 60000,
            "urls": {
                "api": {
                    "public": "http://127.0.0.1:8089/kucoin",
                    "private": "http://127.0.0.1:8089/kucoin"
                }
            }
        },
        "ccxt_async_config": {
            "enableRateLimit": false,
            "timeout": 60000
```

### Author: 
https://github.com/mikekonan/freqtrade-proxy
