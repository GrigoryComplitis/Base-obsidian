1. Скачать каталог со скриптами: {вставить актуальную ссылку}

_**wget -O -**_ [](http://download.faceneurovision.com/lpr/x86/install.tar "http://download.faceneurovision.com/lpr/x86/install.tar")_**[http://download.faceneurovision.com/lpr/x86/install.tar](http://download.faceneurovision.com/lpr/x86/install.tar)**_ _**| cat | tar x**_

2. Установить драйвер нвидиа, для этого перейти в каталог со скриптами: _**cd install,**_ запустить _**./nvidia_driver.sh**_ (по окончанию сервер будет перезагружен).

- Проверить поставилось ли всё корректно командой _**nvidia-smi**_ , если это свежая ОС, то на ней могут отсутствовать headers и команда даже после успешной установки драйвера может выдавать ошибку. В таком случае необходимо установить headers следующей командой _**sudo apt install linux-headers-$(uname -r)**_

3. Зайти в install _**cd install**_ и запустить _**./install.sh**_ для установки необходимого для работы LPR ПО (по окончанию сервер будет перезагружен)

4. Зайти в install _**cd install**_ и запустить _**./docker.sh**_. По окончаюнию работы скрипта будут установлено и запущено ПО LPR.