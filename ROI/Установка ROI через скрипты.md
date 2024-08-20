- Скачать каталог со скриптами: {вставить актуальную ссылку}

	wget -O - _[http://download.faceneurovision.com/roi/x86/install.tar](http://download.faceneurovision.com/roi/x86/install.tar)_ | cat | tar x

- Установить драйвер Nvidia, для этого перейти в каталог со скриптами и запустить скрипт (по окончанию сервер будет перезагружен):

	`cd install
	`./nvidia_driver.sh

(Или установить вручную версию драйвера 535 или новее.)

- Зайти в каталог со скриптами и запустить скрипт для установки необходимого для работы ROI ПО (по окончанию сервер будет перезагружен)

	`cd install 
	`./install.sh

- Зайти в каталог со скриптами и запустить скрипт докер. По окончанию работы скрипта будут установлено и запущено ПО ROI.  
  Примечание, если опускаем контейнеры, нужно в папке ROI запустить docker compose сначала в core потом в docker.

	`cd install 
	`./docker.sh

- Открываем файл .env и вбиваем команду: docker pull <всё_после_= > - и так с каждым образом в файле .env

- Создание базы данных:  
	`docker cp update_db.sql roi_db:/` - скопировать файл update  
	`docker exec -it roi_db psql -U postgres -d region_of_interest -a -f update_db.sql` - применить изменения из файла

- Если не запускается контейнер roi_server, при этом высвечивает ошибки сети roi_net, то нужно дописать:  
	`docker network create --subnet 172.50.0.0/16 roi_net

