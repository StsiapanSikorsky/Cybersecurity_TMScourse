# Домашнее задание 6 - Криптография
1) Изучить этапы, методы и протоколы IPSec  
- IKE Phase 1  
- IKE Phase 2
- IPSec framework protocols
- HTTP и HTTPS
2) SSH Best Practice
- На VM Ubuntu (KaliLinux) настроить SSH по лучшим практикам
- Сгенерировать на Windows host или KaliLinux VM (ssh-keygen) приватный и публичный ключ, добавить публичный ключ (замок) ssh-add либо scp на Ubuntu VM, где настроить ssh
- Подключиться к Ubuntu VM используя приватный ключ
3) WriteGuard VPN
- Развернуть Ubuntu с 2 сетевыми интерфейсами (один в интернет, другой во внутреннюю сеть в которую подключены WindowsServer и KaliLinux). Настроить на ней возможность подключения по RDP и SSH с WindowsServer на срок неделю
- Установить и настроить WireGuardVPN на Ubuntu
- Установить агент VPN Wireguard на хост машину
- Установить VPN соединение между хостовой машиной и Ubuntu с VPN Wireguard 

### Дополнительные ссылки:
[Что такое IPSec и принцип работы](https://networklessons.com/cisco/ccie-routing-switching/ipsec-internet-protocol-security)  
[Лучшие практики по настройке SSH](https://wiki.merionet.ru/articles/luchshie-praktiki-po-zashhite-ssh-podklyucheniya)  
[Установка и конфигурация WireguardVPN Ubuntu](https://habr.com/ru/sandbox/189100/)  
[Отличие и безопасность HTTP и HTTPS](https://www.cloudflare.com/ru-ru/learning/ssl/why-is-http-not-secure/)  