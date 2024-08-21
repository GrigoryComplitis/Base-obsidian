

Инструкция по установке FNVA (микросервер)

> [!attention] 
> Прошивка возможна только с Linux, с WINDOWS прошить НЕЛЬЗЯ. 
ЗАПРАШИВАТЬ У КЛИЕНТОВ ИНФОРМАЦИЮ ДЛЯ ПЕРЕПРОШИВКИ КОРОБКИ! 

1. Скачать архив с Google-диска на Ваш компьютер: [](https://drive.google.com/file/d/1ENuoowEaxBNBlc6mYgeMNiXb2SqhbYcd/view?usp=share_link)[https://drive.google.com/file/d/1kFzTrDRkSVLUPhnXdpfK7J--gdFj7xNx/view?usp=sharing](https://drive.google.com/file/d/1kFzTrDRkSVLUPhnXdpfK7J--gdFj7xNx/view?usp=sharing)

2. Перенести скаченный файл в корневую папку ПК. Ввести в терминал (командную строку):

> [!todo] 
> <span style="color: #f4a448">*sudo tar -xzvpf EN715-NX-R2.1.0.5.1.tar.gz*</span>

3. Прошиваем микросервер.

 На ПК(Linux), перейти в директорию Linux_for_Tegra
> [!todo] 
> <span style="color: #f4a448">*cd JetPack_5.1_Linux_JETSON_NX_TARGETS/Linux_for_Tegra*</span> 

**(если прошиваешь на данном компьютере первый раз, то установить доп. утилиты)**

> [!todo] 
> <span style="color: #f4a448">*sudo apt update && sudo apt install -y qemu-user-static libxml2-utils liblz4-tool binutils*</span>

4. Подключить микросервер к ПК с помощью кабеля Micro USB — USB.

Войти в режим восстановления (recovery mode):

Выключить питание -> нажать и удерживать кнопку восстановления (на дне устройства в технологическом отверстии, см. схему ниже) -> включить питание -> подождать 2 секунды -> отпустить кнопку восстановления

  

![](https://complitech.aspro.cloud/files/download/4f9d2e29-0142-11ee-a147-fa163e2ff576)

Запустить скрипт установки (уточнить):

> [!todo] 
> <span style="color: #f4a448">*cd install 
sudo ./install.sh*</span>

  

#### НАСТРОЙКА FNVA:  

**Все дальнейшие действия выполнять на самом сервере или удаленно подключиться к нему по ssh.**

1. Подключиться к FNV :  

(логин: nvidia, пароль: nvidia)

-напрямую к микросерверу подключиться через HDMI-кабель к монитору, а также подключить клавиатуру.

ИЛИ

ssh nvidia@0.0.0.0(необходимо указать ip-адрес присвоенный FNVA)

2. Отформатировать карточку:

> [!todo] 
> <span style="color: #f4a448">*sudo umount /dev/mmcblk1p1 && sudo mkfs.ext4 /dev/mmcblk1p1 *</span>

3. Перейти в каталог /tmp:

> [!todo] 
> <span style="color: #f4a448">*cd /tmp*</span> 

4. Скачать каталог со скриптами:

> [!todo] 
> <span style="color: #f4a448">*wget -O - [http://download.faceneurovision.com/fnv5/arm/install.tar](http://download.faceneurovision.com/fnv5/arm/install.tar) | cat | tar x*</span> 

5. Перейти в папку со скриптами и запустить ./install.sh для установки необходимого для работы FNV ПО (по  
окончанию сервер будет перезагружен)

> [!todo] 
> <span style="color: #f4a448">*cd install
./install.sh*</span>

6. После перезагрузки снова перейти в каталог /tmp  и заново скачать каталог со скриптами: 

> [!todo] 
> <span style="color: #f4a448">*cd /tmp
wget -O - [http://download.faceneurovision.com/fnv5/arm/install.tar](http://download.faceneurovision.com/fnv5/arm/install.tar) | cat | tar x*</span> 

7. Зайти в install $ cd install и запустить скрипт ./docker.sh (будут скачаны и запущены новые образы докера)

> [!todo] 
> <span style="color: #f4a448">*cd install
./docker.sh*</span> 

8. Желательно задавать ip-адрес всегда, так как в случае невыполнения данного пункта, при смене локальной сети, ip-адрес будет присвоен автоматически, что усложнит его определение на новом месте.    

Дефолтный ip-адрес

Если нужно поменять ip запустить

> [!todo] 
> <span style="color: #f4a448">*./ip_config.sh*</span> 

( или  

> [!todo] 
> <span style="color: #f4a448">*sudo nmcli connection modify "static" ipv4.addresses 0.0.0.0/24 ipv4.gateway 0.0.0.0 ipv4.method manual
sudo nmcli connection reload && sudo nmcli connection down "static" && sudo nmcli connection up "static"*<>

)

Подключиться по WEB интерфейсу, добавить сервер и активировать лицензию

Изменить hostname по шаблону FNVA_Порядковый_номер

При необходимости подключения платы ETW-01 нужно добавить в compose модуль ETW:

  module_etw:
	image: facenv/module_etw:arm
    restart: always
    network_mode: "host"
    depends_on:
      - "fnv"
    command: python3 manager.py --host $LOCAL_ADDRESS --port 5010
    logging:
      driver: "json-file"
      options:
        max-size: "50m"
        max-file: "5"


По FNVA ведётся учёт в этой таблице: https://docs.google.com/spreadsheets/d/13OTn8Xz-Ti_pXPJjqcc65Bt9GDu-JckCCqseG7LIAI8/edit#gid=0  
  
Примечание, если опускаем контейнеры, нужно в папке FNV запустить docker compose сначала в core потом в docker.

Ошибки, которые могут возникнуть:  
При попытке запустить ./install.sh может выдать use root for BSP  
В таком случае прописываем команду: 
> [!todo] 
> <span style="color: #f4a448">*sudo ROOTFS_ENC=1 ./tools/kernel_flash/l4t_initrd_flash.sh -p "-i ./ekb.key" --external-device nvme0n1p1 -c ./tools/kernel_flash/flash_l4t_nvme_rootfs_enc.xml --external-only -S 40GiB --showlogs --network usb0 jetson-xavier-nx-devkit-emmc nvme0n1p1*</span> 
  
Скорее всего команда с первого раза не сработает  
будет выдавать: "sudo apt-get install <service>"

В таком случае доустанавливаем и повторяем команду (может повторяться несколько раз), пока не пропадёт sudo apt-get ..  
Потом запускаем ./install.sh