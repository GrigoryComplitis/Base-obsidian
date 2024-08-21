Скачать каталог со скриптами: {вставить актуальную ссылку}

> [!todo] 
> <span style="color: #f4a448">*wget -O - [http://download.faceneurovision.com/fnv5/x86/install.tar](http://download.faceneurovision.com/fnv5/x86/install.tar) | cat | tar x*</span> 

Установить драйвер Nvidia, для этого перейти в каталог со скриптами и запустить скрипт (по окончанию сервер будет перезагружен):

> [!todo] 
> <span style="color: #f4a448">*cd install
>./nvidia_driver.sh*</span> 

(Или установить вручную версию драйвера 535 или новее.)

Зайти в каталог со скриптами и запустить скрипт для установки необходимого для работы FNV ПО (по окончанию сервер будет перезагружен)

> [!todo] 
> <span style="color: #f4a448">*cd install 
./install.sh*</span> 

Зайти в каталог со скриптами и запустить скрипт докер. По окончанию работы скрипта будут установлено и запущено ПО FNV.  
  Примечание, если опускаем контейнеры, нужно в папке FNV запустить docker compose сначала в core потом в docker.

> [!todo] 
> <span style="color: #f4a448">*cd install 
./docker.sh *</span>