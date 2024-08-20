Установка nvidia, docker и доп либ.

ВЫПОЛНЯТЬ ПОД ПОЛЬЗОВАТЕЛЕМ(НЕ ROOT), КОТОРЫЙ БУДЕТ РАБОТАТЬ ДАЛЬШЕ В СИСТЕМЕ. СТАВИТЬ ВСЕ НА ОДНОМ ПОЛЬЗОВАТЕЛЕ, А РАБОТАТЬ С ДРУГОГО - НЕДОПУСТИМО.

Драйвер nvidia:

	Проверка Secure boot:
	sudo mokutil --sb-state
	если статус enabled, то необходимо отключить SecureBoot в BIOS.

	Установка драйвера nvidia:
	Для добавления graphics-drivers в систему выполните команду:
	sudo add-apt-repository ppa:graphics-drivers/ppa

	Проверьте рекомендуемую версию видеодрайвера командой:
	ubuntu-drivers devices

	и установите драйвер не ниже 535 версии с помощью следующей команды:
	sudo apt install -y ubuntu-drivers-common
	sudo apt install -y nvidia-common --no-install-recommends
	sudo apt install -y nvidia-driver-535 --no-install-recommends

	После установки драйвера выполните перезагрузку системы:
	sudo reboot

	проверить работоспособность установленного драйвера:
	nvidia-smi


Установка дополнительного ПО

	Предварительно необходимо установить:
	sudo apt install -y curl, mc, net-tools,
	 sudo apt install -y qml-module-qtquick-controls2 libgstreamer1.0-dev libgstreamer-plugins-base1.0-dev libgstreamer-plugins-bad1.0-dev gstreamer1.0-plugins-base gstreamer1.0-plugins-good gstreamer1.0-plugins-bad gstreamer1.0-plugins-ugly gstreamer1.0-libav gstreamer1.0-tools gstreamer1.0-x gstreamer1.0-alsa gstreamer1.0-gl gstreamer1.0-gtk3 gstreamer1.0-qt5 gstreamer1.0-pulseaudio libqt5websockets5-dev qtquickcontrols2-5-dev qtdeclarative5-private-dev qtbase5-private-dev qml-module-qt-labs-qmlmodels qml-module-qtquick-shapes libqt5multimedia5-plugins libqt5serialport5 libqt5serialport5-dev


Команда для работы с пультом во вьювере
	sudo usermod -aG dialout {$USER}

****ПРОВЕРКА РАБОТОСПОСОБНОСТИ****

docker:
	docker ps
	должно вывести пустую таблицу

nvidia-docker2:
	nvidia-docker -v
	должно вывести версию

nvidia driver-510:
	nvidia-smi
	должно вывести таблицу о видеокарте


ПОСЛЕ ЗАВЕРШЕНИЯ ПОДГОТОВИТЕЛЬНЫХ РАБОТ МОЖНО ПЕРЕХОДИТЬ К УСТАНОВКЕ НЕОБХОДИМЫХ КЛИЕНТОВ
	[[Клиент VMS]]
    [[Клиенты Sentinel R]]