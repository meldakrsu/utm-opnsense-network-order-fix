# UTM + OPNsense (Apple Silicon) — Network Order Fix (WAN/LAN)

## Problem
OPNsense WAN/LAN doğru görünmesine rağmen:
- Windows internete çıkmıyordu
- OPNsense 8.8.8.8 ping fail / timeout olabiliyordu
- Web GUI erişimi tutarsızdı

## Root Cause
UTM’de **Network kartlarının sırası**, OPNsense’in `vtnet0/vtnet1` eşleşmesini etkiliyor.

## Fix
UTM’de OPNsense VM için network sırası şöyle olmalı:
- **Network (üstte)** = `Host Only`  → LAN
- **Network (altta)** = `Shared Network` → WAN

> Bu değişiklikten sonra:
> - OPNsense 8.8.8.8 ping aldı
> - Windows, 192.168.50.1’i pingleyebildi
> - Trafik düzgün şekilde firewall üzerinden aktı

## Screenshot

![UTM OPNsense network order](./images/utm-opnsense-network-order.png)
