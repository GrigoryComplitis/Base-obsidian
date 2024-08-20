Прошивка 5.1.2  
[http://download.faceneurovision.com/fnv5/arm/JetPack_5.1.2_Linux_JETSON.tgz](http://download.faceneurovision.com/fnv5/arm/JetPack_5.1.2_Linux_JETSON.tgz)  
Установка докер и настройка окружения  
[http://download.faceneurovision.com/fnv5/arm/install/install.sh](http://download.faceneurovision.com/fnv5/arm/install/install.sh)


> ВНИМАНИЕ: прошивка возможна только с Linux, с WINDOWS прошить НЕЛЬЗЯ.

1. Скачать архив с **прошивкой 5.1.2** на Ваш компьютер [http://download.faceneurovision.com/fnv5/arm/JetPack_5.1.2_Linux_JETSON.tgz](http://download.faceneurovision.com/fnv5/arm/JetPack_5.1.2_Linux_JETSON.tgz)  
(если по ссылке скачивание прошивки невозможно, прошивку можно найти на жёстком диске HP или на ПК Asus в офисе)

2. Перенести скаченный файл в корневую папку ПК, с которого будете перепрошивать. Ввести в терминал (командную строку):

sudo tar -xzvpf EN715-NX-R2.3.0.5.1.2.tar

3. На ПК(Linux), перейти в директорию Linux_for_Tegra

cd JetPack_5.1.2_Linux_JETSON/Linux_for_Tegra

**(если прошиваешь на данном компьютере первый раз, то установить доп. утилиты)**

sudo apt update && sudo apt install -y qemu-user-static libxml2-utils liblz4-tool binutils 

4. Подключить микросервер к ПК с помощью кабеля Micro USB — USB.

Войти в режим восстановления (recovery mode):

Выключить питание -> нажать и удерживать кнопку восстановления (на дне устройства в технологическом отверстии, см. схему ниже) -> включить питание -> подождать 2 секунды -> отпустить кнопку восстановления

![](https://complitech.aspro.cloud/files/download/4f9d2e29-0142-11ee-a147-fa163e2ff576)

Запустить скрипт установки (уточнить):

cd install 
sudo ./install.sh

####   

## НАСТРОЙКА LPRA:

**Все дальнейшие действия выполнять на самом сервере или удаленно подключиться к нему по ssh.**

1. Подключиться к LPRA :  

(логин: nvidia, пароль: nvidia)

-напрямую к микросерверу подключиться через HDMI-кабель к монитору, а также подключить клавиатуру.

ИЛИ

ssh nvidia@0.0.0.0(необходимо указать ip-адрес присвоенный LPRA)

2. Отформатировать карточку:

sudo umount /dev/mmcblk1p1 && sudo mkfs.ext4 /dev/mmcblk1p1

3. Перейти в каталог /tmp:

cd /tmp

4. Скачать каталог со скриптами:

wget -O - [http://download.faceneurovision.com/fnv5/arm/install/install.sh](http://download.faceneurovision.com/fnv5/arm/install/install.sh)


5. Перейти в папку со скриптами и запустить ./install.sh для установки необходимого для работы LPRA ПО (по окончании сервер будет перезагружен)

cd install
./install.sh

6. Создать папку LPR и загрузить в неё файлы из вложений любым удобным способом. Создать сеть для контейнеров

mkdir ~/LPR
docker network create --subnet 172.49.0.0/16 lpr_net

7. Проверить актуальность версий образов в файле .env, добавить модуль для ETR:

  

docker-compose.yml  

version: '3.9'

services:
  module_etr:
    image: facenv/module_etr:v1.0.2_arm
    container_name: module_etr
    restart: always
    command: "python3 -m app"
    privileged: true
    env_file:
      - ./etr.env
    network_mode: "host"
    cap_add:
      - SYS_RAWIO
    logging:
      driver: "json-file"
      options:
        max-size: "100m"
        max-file: "2"

etr.env  

SERVER_HOST=<ip_address>
SERVER_PORT=5190
CONNECT_TYPE='http'
VENDOR_NAME='COMPLITECH_IM'
STATUSES='1,3'
DELAY_TIME=5

  

8. Запустить docker-compose. После успешного запуска необходимо применить обновление БД:

docker cp update_db.sql lpr_db:/ && docker exec -it lpr_db psql -U postgres -d lrp_db -a -f update_db.sql

9. При необходимости отдать микросервер заказчику следовать инструкции по подготовке микросервера к пилоту:



P.S. Если контейнер камеры не поднимается (камера из статуса "в аналитике" переходит в "нет доступа"), нужно убедиться, что образ камеры загружен из хаба. Если не загружен, то docker pull <имя образа>

Если контейнер камеры рестартует, нужно прочитать логи сервера (docker logs lpr_server)