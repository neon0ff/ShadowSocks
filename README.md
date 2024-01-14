# ShadowSocks
## ShadowSocks + V2Ray на базе Ubuntu Server

### 1. Для начала обновляем список пакетов
```bash
sudo apt update && apt upgrade -y
```

### 2. Устанавливаем требуемые пакеты
```bash
sudo apt install shadowsocks-libev -y
```

### 3. Переходим в деректорию ShadowSocks'a и загружаем плагин V2Ray
```bash
cd /etc/shadowsocks-libev/
```
```bash
sudo wget https://github.com/neon0ff/ShadowSocks/blob/main/v2ray-plugin
```

### 4. Редактируем конфиг под наши параметры
```bash
sudo nano /etc/shadowsocks-libev/config.json
```

### 5. Заполняем конфиг таким образом. Не забудьте изменить порт сервара и пароль на свой
```bash
{
    "server":["0.0.0.0"],
    "mode":"tcp_and_udp",
    "server_port":15151,
    "local_port":1080,
    "password":"your_password",
    "timeout":300,
    "method":"xchacha20-ietf-poly1305",
    "nameserver":"8.8.8.8",
    "no_delay": true,
    "fast_open": true,
    "reuse_port": true,
    "plugin":"/etc/shadowsocks-libev/v2ray-plugin",
    "plugin_opts":"server"
}
```
### 6. Далее перехапускаем службы и добовляем в автозагрузку
```bash
sudo service shadowsocks-libev restart
```
```bash
sudo systemctl enable shadowsocks-libev
```
### После чего проверяем статус службы
```bash
service shadowsocks-libev status
```
