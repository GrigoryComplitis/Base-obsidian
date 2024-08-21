Скачать каталог со скриптами: {вставить актуальную ссылку}

> [!todo] 
> <span style="color: #f4a448">*wget -O - http://download.faceneurovision.com/roi/x86/install.tar | cat | tar x*</span> 

Установить драйвер Nvidia, для этого перейти в каталог со скриптами и запустить скрипт (по окончанию сервер будет перезагружен):

> [!todo] 
> <span style="color: #f4a448">*cd install
 > ./nvidia_driver.sh *</span>

(Или установить вручную версию драйвера 535 или новее.)

Зайти в каталог со скриптами и запустить скрипт для установки необходимого для работы ROI ПО (по окончанию сервер будет перезагружен)

> [!todo] 
> <span style="color: #f4a448">*cd install 
> ./install.sh*</span> 

Зайти в каталог со скриптами и запустить скрипт докер. По окончанию работы скрипта будут установлено и запущено ПО ROI.  
  Примечание, если опускаем контейнеры, нужно в папке ROI запустить docker compose сначала в core потом в docker.

> [!todo] 
> <span style="color: #f4a448">*cd install 
./docker.sh*</span> 

Открываем файл .env и вбиваем команду: docker pull <всё_после_= > - и так с каждым образом в файле .env

Создание базы данных:  
> [!todo] 
> <span style="color: #f4a448">*docker cp update_db.sql roi_db:/
> docker exec -it roi_db psql -U postgres -d region_of_interest -a -f update_db.sql*</span> 

Если не запускается контейнер roi_server, при этом высвечивает ошибки сети roi_net, то нужно дописать:  
> [!todo] 
> <span style="color: #f4a448">*docker network create --subnet 172.50.0.0/16 roi_net*</span> 

