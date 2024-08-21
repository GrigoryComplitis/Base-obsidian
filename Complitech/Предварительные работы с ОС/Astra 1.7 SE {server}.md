**Установка nvidia, docker и доп либ.**

> [!danger] 
> ВЫПОЛНЯТЬ ПОД ПОЛЬЗОВАТЕЛЕМ(НЕ ROOT), КОТОРЫЙ БУДЕТ РАБОТАТЬ ДАЛЬШЕ В СИСТЕМЕ. СТАВИТЬ ВСЕ НА ОДНОМ ПОЛЬЗОВАТЕЛЕ, А РАБОТАТЬ С ДРУГОГО - НЕДОПУСТИМО. 

**Работа с репозиториями:**

> [!attention] 
> ЕСЛИ ЕСТЬ ИНТЕРНЕТ: 

В source list (/etc/apt/sources.list) закомментировать CD-ROM и всё, что там ещё есть и добавить(если пишет что невозможно установить безопасным способом, то вместо https в ссылках указать http):

> [!todo] 
> \#Основной репозиторий
> <span style="color: #f4a448">*deb <a href="https://dl.astralinux.ru/astra/stable/1.7_x86-64/repository-main/" target="_blank">https://dl.astralinux.ru/astra/stable/1.7_x86-64/repository-main/</a>;     1.7_x86-64 main contrib non-free*</span>
>
> \#Оперативные обновления основного репозитория
> <span style="color: #f4a448">*deb <a href="https://dl.astralinux.ru/astra/stable/1.7_x86-64/repository-update/" target="_blank">https://dl.astralinux.ru/astra/stable/1.7_x86-64/repository-update/</a>;   1.7_x86-64 main contrib non-free*</span>
> 
> \#Базовый репозиторий
> <span style="color: #f4a448">*deb <a href="https://dl.astralinux.ru/astra/stable/1.7_x86-64/repository-base/" target="_blank">https://dl.astralinux.ru/astra/stable/1.7_x86-64/repository-base/</a>;     1.7_x86-64 main contrib non-free*</span>
>
> \#Расширенный репозиторий
> <span style="color: #f4a448">*deb <a href="https://dl.astralinux.ru/astra/stable/1.7_x86-64/repository-extended/" target="_blank">https://dl.astralinux.ru/astra/stable/1.7_x86-64/repository-extended/</a>;    1.7_x86-64 main contrib non-free*</span>
> 
> \#Расширенный репозиторий (компонент astra-ce)
> <span style="color: #f4a448">*deb <a href="https://dl.astralinux.ru/astra/stable/1.7_x86-64/repository-extended/" target="_blank">https://dl.astralinux.ru/astra/stable/1.7_x86-64/repository-extended/</a>;    1.7_x86-64 astra-ce*</span>




> [!attention] 
> ЕСЛИ НЕТ ИНТЕРНЕТА
 
Скопировать файлы репозиториев в папку в файловой системе. Например: 

> [!todo] 
> <span style="color: #f4a448">*sudo mkdir /Документы/AstraRepos *</span>

Cоздать папки для репозиториев:

> [!todo] 
> <span style="color: #f4a448">*sudo mkdir /opt/repo_base/
sudo mkdir /opt/repo_extended/ *</span>

Распаковываем файлы репозиториев в указанные папки:

> [!todo] 
> <span style="color: #f4a448">*sudo tar xvf /home/\<user\>/Документы/astra\ repos/base-1.7.3-03.11.2022_15.53.tgz -C /opt/repo_base/
sudo tar xvf /home/\<user\>/Документы/astra\ repos/extended-1.7.3.ext1.3--23.11.2022_19.59.tgz -C /opt/repo_extended/*</span> 

Прописываем пути для фалов репозиторий:

> [!todo] 
> <span style="color: #f4a448">*sudo nano /etc/apt/sources.list*</span>

В файл добавляем строки:
> [!todo] 
> <span style="color: #f4a448">*deb file:/opt/repo_base 1.7_x86-64 main contrib non-free
> deb file:/opt/repo_extended 1.7_x86-64 main contrib non-free*</span> 

(ОПЦИОНАЛЬНО для тех пользователей, у кого нет диска с репозиториями) необходимо закомментировать строку, добавив в начало символ #

> [!todo] 
> <span style="color: #f4a448">*\#deb cdrom:[OS Astra Linux 1.7.0 1.7_x86-64 DVD ]/ 1.7_x86-64 contrib main non-free *</span>


> [!info] 
> После проброса репозиториев из любого способо прописать
>  <span style="color: #f4a448">*sudo apt update && sudo apt upgrade*</span>


**УСТАНОВКА ЯДРА 5.15**

> [!todo] 
> <span style="color: #f4a448">*sudo apt install linux-5.15
sudo reboot*</span> 

> [!info] 
> Чтобы ядро точно установилось раздел /boot должен иметь размет минимум 1Gb, с запасом можно сделать 3Gb. 

Если существует файл /etc/X11/xorg.conf, переименовать его (или просто удалить).

Дале необходимо запретить запуск драйверов Nouveau: 

> [!todo] 
> <span style="color: #f4a448">*sudo nano /etc/modprobe.d/blacklist.conf*</span>

добавить строчки:

> [!todo] 
> <span style="color: #f4a448">*blacklist nouveau
> options nouveau modeset=0*</span> 

и в файле: 

> [!todo] 
> <span style="color: #f4a448">*sudo nano /etc/initramfs-tools/modules*</span> 

закомментировать строчку 

> [!todo] 
> <span style="color: #f4a448">*\#nouveau modeset=1*</span> 

после чего выполнить команду

> [!todo] 
> <span style="color: #f4a448">*sudo update-initramfs -u -k all*</span> 



**Драйвер nvidia:**

Проверка Secure boot:
> [!todo]
> <span style="color: #f4a448">*sudo mokutil --sb-state*</span>

> [!info] 
> если статус enabled, то необходимо отключить SecureBoot в BIOS. 

Установка драйвера nvidia:

Установите драйвер версии 510 (ДЛЯ ВИДЕОКАРТ НИЖЕ 4 ПОКОЛЕНИЯ)с помощью следующей команды:
> [!todo] 
> <span style="color: #f4a448">*sudo apt install nvidia-detect-510
> nvidia-detect
> sudo apt install -y nvidia-driver-510 --no-install-recommends *</span>

Для установки 535 драйверов на сервер Астры, нужно перейти  по ссылке https://us.download.nvidia.com/XFree86/Linux-x86_64/535.86.05/NVIDIA-Linux-x86_64-535.86.05.run , затем ввести команды(уточнение, для карты 4080 msi cтавить дрова 550 и выше, если это не сервер, на сервер в любом случае идут дрова 535):

> [!todo] 
> <span style="color: #f4a448">*sudo apt install gcc && sudo apt install cmake
> sudo sh ./NVIDIA-Linux-x86_64-535.86.05.run*</span> 

После установки драйвера выполните перезагрузку системы:
> [!todo] 
> <span style="color: #f4a448">*sudo reboot*</span> 

проверить работоспособность установленного драйвера:
> [!todo] 
> <span style="color: #f4a448">*nvidia-smi*</span> 


**Установка дополнительного ПО**

Предварительно необходимо установить:
> [!todo] 
> <span style="color: #f4a448">*sudo apt install -y curl, mc, net-tools *</span>
> 
> <span style="color: #f4a448">*sudo apt install -y qml-module-qtquick-controls2 libgstreamer1.0-dev libgstreamer-plugins-base1.0-dev libgstreamer-plugins-bad1.0-dev gstreamer1.0-plugins-base gstreamer1.0-plugins-good gstreamer1.0-plugins-bad gstreamer1.0-plugins-ugly gstreamer1.0-libav gstreamer1.0-tools gstreamer1.0-x gstreamer1.0-alsa gstreamer1.0-gl gstreamer1.0-gtk3 gstreamer1.0-qt5 gstreamer1.0-pulseaudio libqt5websockets5-dev qtquickcontrols2-5-dev qtdeclarative5-private-dev qtbase5-private-dev qml-module-qt-labs-qmlmodels qml-module-qtquick-shapes libqt5multimedia5-plugins libqt5serialport5 libqt5serialport5-dev*</span>

после установки библиотек, необходимо ввести в консоль:

> [!todo] 
> <span style="color: #f4a448">*sudo ln -s /usr/lib/x86_64-linux-gnu/libxcb-util.so.0 /usr/lib/x86_64-linux-gnu/libxcb-util.so.1*</span> 


**Установка утилит nvidia:**

> [!todo] 
> <span style="color: #f4a448">*distribution=\$(. /etc/os-release;echo \$ID\$VERSION_ID)
> curl -s -L https://nvidia.github.io/nvidia-docker/gpgkey | sudo apt-key add -
> curl -s -L https://nvidia.github.io/nvidia-docker/$distribution/nvidia-docker.list | sudo tee /etc/apt/sources.list.d/nvidia-docker.list
> sudo apt update
> sudo apt install -y nvidia-container-toolkit
> sudo apt install -y nvidia-docker2
> sudo usermod -aG docker ${USER}
> su - $USER
> sudo reboot*</span>

**Установка Docker-Remote:**

> [!todo] 
> <span style="color: #f4a448">*sudo mkdir /etc/systemd/system/docker.service.d
> sudo echo -e "[Service]\nExecStart=\nExecStart=/usr/sbin/dockerd -H fd:// -H tcp://0.0.0.0:2375" > docker_override.conf
> sudo mv docker_override.conf /etc/systemd/system/docker.service.d/.
> sudo chown root:root /etc/systemd/system/docker.service.d/docker_override.conf
> sudo systemctl daemon-reload
> sudo systemctl restart docker.service*</span> 



**ПРОВЕРКА РАБОТОСПОСОБНОСТИ**

docker:
> [!todo] 
> <span style="color: #f4a448">*docker ps*</span> 

должно вывести пустую таблицу

docker-compose:
> [!todo] 
> <span style="color: #f4a448">*docker-compose -v*</span>

должно вывести версию
	
nvidia-docker2:
> [!todo] 
> <span style="color: #f4a448">*nvidia-docker -v*</span> 

должно вывести версию

nvidia driver-535:
> [!todo] 
> <span style="color: #f4a448">*nvidia-smi*</span> 

должно вывести таблицу о видеокарте

docker-remote:
> [!todo] 
> <span style="color: #f4a448">*sudo netstat -lntp | grep dockerd *</span>

должно вывести что-то типа этого:
> [!info] 
> tcp   0    0 127.0.0.1:2375   0.0.0.0:*  LISTEN   3758/dockerd 
> В случае если не сработало и выдаёт ошибку демона, удалить override.conf, и повторить всё с первого пункта



ПОСЛЕ ЗАВЕРШЕНИЯ ПОДГОТОВИТЕЛЬНЫХ РАБОТ МОЖНО ПЕРЕХОДИТЬ К УСТАНОВКЕ НЕОБХОДИМОГО ПО
	
	[[Сервер VMS]]
    [[Сервер Sentinel R]]
	[[ROI]]
	[[LPR]]
	[[FNV]]