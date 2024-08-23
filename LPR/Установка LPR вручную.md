1. Взять актуальные образы со стенда с помощью команды:
> [!todo] 
> <span style="color: #f4a448">*docker save -o *image* image.img*</span> 

> [!attention] 
> СОХРАНЕНИЕ В .IMG ОБЯЗАТЕЛЬНО! 

2. С той папки, в которой лежат эти образы произвести команду:
> [!todo] 
> <span style="color: #f4a448">*for img in \*.img; do docker load -i "$img"; done*</span> 

> [!info] 
> Команда самостоятельно загрузит все образы 