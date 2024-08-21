Установка nvidia, docker и доп либ.

> [!danger] 
> ВЫПОЛНЯТЬ ПОД ПОЛЬЗОВАТЕЛЕМ(НЕ ROOT), КОТОРЫЙ БУДЕТ РАБОТАТЬ ДАЛЬШЕ В СИСТЕМЕ. СТАВИТЬ ВСЕ НА ОДНОМ ПОЛЬЗОВАТЕЛЕ, А РАБОТАТЬ С ДРУГОГО - НЕДОПУСТИМО. 

Драйвер nvidia:

Проверка Secure boot:
> [!todo]
> <span style="color: #f4a448">*sudo mokutil --sb-state*</span>

> [!info] 
> если статус enabled, то необходимо отключить SecureBoot в BIOS. 

Установка драйвера nvidia:
	Для добавления graphics-drivers в систему выполните команду:
> [!todo] 
> <span style="color: #f4a448">*sudo add-apt-repository ppa:graphics-drivers/ppa *</span>

Проверьте рекомендуемую версию видеодрайвера командой:
> [!todo] 
> <span style="color: #f4a448">*ubuntu-drivers devices*</span> 

и установите драйвер версии 535 с помощью следующей команды:
> [!todo] 
> <span style="color: #f4a448">*sudo apt install -y ubuntu-drivers-common
> sudo apt install -y nvidia-common --no-install-recommends
> sudo apt install -y nvidia-driver-535 --no-install-recommends *</span>

После установки драйвера выполните перезагрузку системы:
> [!todo] 
> <span style="color: #f4a448">*sudo reboot*</span> 

проверить работоспособность установленного драйвера:
> [!todo] 
> <span style="color: #f4a448">*nvidia-smi*</span> 

Установка Docker:  
> [!todo] 
> <span style="color: #f4a448">*curl -fsSL https://download.docker.com/linux/ubuntu/gpg(https://download.docker.com/linux/ubuntu/gpg) | sudo apt-key add - 
sudo add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu(https://download.docker.com/linux/ubuntu) $(lsb_release -cs) stable" 
sudo apt update
sudo apt install -y docker-ce docker-ce-cli containerd.io*</span> 

Установка дополнительного ПО

Предварительно необходимо установить:
> [!todo] 
> <span style="color: #f4a448">*sudo apt install -y curl, mc, net-tools *</span>
> 
> <span style="color: #f4a448">*sudo apt install -y qml-module-qtquick-controls2 libgstreamer1.0-dev libgstreamer-plugins-base1.0-dev libgstreamer-plugins-bad1.0-dev gstreamer1.0-plugins-base gstreamer1.0-plugins-good gstreamer1.0-plugins-bad gstreamer1.0-plugins-ugly gstreamer1.0-libav gstreamer1.0-tools gstreamer1.0-x gstreamer1.0-alsa gstreamer1.0-gl gstreamer1.0-gtk3 gstreamer1.0-qt5 gstreamer1.0-pulseaudio libqt5websockets5-dev qtquickcontrols2-5-dev qtdeclarative5-private-dev qtbase5-private-dev qml-module-qt-labs-qmlmodels qml-module-qtquick-shapes libqt5multimedia5-plugins libqt5serialport5 libqt5serialport5-dev*</span>


Установка утилит nvidia:

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

Установка Docker-Remote:

> [!todo] 
> <span style="color: #f4a448">*sudo mkdir /etc/systemd/system/docker.service.d
> sudo echo -e "[Service]\nExecStart=\nExecStart=/usr/bin/dockerd -H fd:// -H tcp://0.0.0.0:2375" > docker_override.conf
> sudo mv docker_override.conf /etc/systemd/system/docker.service.d/.
> sudo chown root:root /etc/systemd/system/docker.service.d/docker_override.conf
> sudo systemctl daemon-reload
> sudo systemctl restart docker.service*</span> 



****ПРОВЕРКА РАБОТОСПОСОБНОСТИ****

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



ПОСЛЕ ЗАВЕРШЕНИЯ ПОДГОТОВИТЕЛЬНЫХ РАБОТ МОЖНО ПЕРЕХОДИТЬ К УСТАНОВКЕ НЕОБХОДИМОГО ПО
	
	[[Сервер VMS]]
    [[Сервер Sentinel R]]
	[[ROI]]
	[[LPR]]
	[[FNV]]