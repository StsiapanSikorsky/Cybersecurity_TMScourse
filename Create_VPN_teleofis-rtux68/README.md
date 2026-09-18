# Алгоритм создания канала VPN с модемом Teleofis rtux68

## Генерация сертификатов клиента и сервера:
1) Скачиваем [EasyRSA-3.2.6-win64.zip](https://github.com/OpenVPN/easy-rsa/releases )
2) Генерируем ключи и сертификаты
   - распаковываем архив
   - в его корне запускаем **openssl.exe**
   - запускаем **EasyRSA-Start.bat**
   - в открывшейся консоли по очереди прописываем команды:
   ~~~
   # 1. Инициализируем чистую структуру папок для ключей
	 ./easyrsa init-pki
	 # 2. Создаем Центр Сертификации (CA). 
	 # Программа попросит придумать пароль (запомните его!) и имя (нажмите Enter)
	 ./easyrsa build-ca

	 # 3. Генерируем параметры Диффи-Хеллмана (файл dh.pem для роутера)
	 ./easyrsa gen-dh

	 # 4. Создаем сертификат сервера без пароля (опция nopass) (запросит ввод yes и пароль)
	 ./easyrsa build-server-full server nopass

	 # 5. Создаем сертификат для Устройства №1 без пароля (запросит ввод yes и пароль)
	 ./easyrsa build-client-full client1 nopass

	 # 6. Создаем сертификат для Устройства №2 без пароля (запросит ввод yes и пароль)
	 ./easyrsa build-client-full client2 nopass
   ~~~
3) Для клиентов создаем файлы .ovpn используя следующий шаблон:
~~~
client
dev tun
proto udp
# Вместо БЕЛОГО_IP укажите ваш внешний IP модема TELEOFIS
remote ВАШ_БЕЛЫЙ_IP 1194
resolv-retry infinite
nobind
persist-key
persist-tun
remote-cert-tls server
cipher AES-256-GCM
verb 3

<ca>
...вставьте текст из файла pki\ca.crt...
</ca>

<cert>
...вставьте текст из файла pki\issued\client1.crt...
</cert>

<key>
...вставьте текст из файла pki\private\client1.key...
</key>
~~~
