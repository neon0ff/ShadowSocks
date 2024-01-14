# ShadowSocks
## ShadowSocks + V2Ray на базе Ubuntu Server

### 1. Обновляем список пакетов
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

### 5. Заполняем конфиг таким образом. Не забудьте изменить порт сервера и пароль на свой
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
### 6. Перезапускаем службы и добавляем в автозагрузку
```bash
sudo service shadowsocks-libev restart
```
```bash
sudo systemctl enable shadowsocks-libev
```
### 7. Проверяем статус службы
```bash
service shadowsocks-libev status
```

## ShadowSocks без V2Ray c помощью Docker-Compose
### 1. Изначально нам нужен сам Docker и Docker-Compose. Как его установить можно почитать [тут](https://totaku.ru/ustanovka-docker-i-docker-compose-na-ubuntu-22-04/)

### 2. Перейдем в домашнюю деректорию командой ```cd``` и создадим там папку
```bash
mkdir ShadowSocks
```

### 3. Перейдем в неё и скачаем файл docker-compose.yml
```bash
cd ShadowSocks
```

```bash
sudo wget https://github.com/neon0ff/ShadowSocks/blob/main/docker-compose.yml
```

### 4. Отредактируем в нем пароль (your_password) на свой
```bash
sudo nano docker-compose.yml
```

###. 5. Запускаем сборку
```bash
sudo docker compose up -d
```

### 6. Проверяем контейнер
```bash
sudo docker ps
```
