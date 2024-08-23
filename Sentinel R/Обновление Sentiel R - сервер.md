1. Скачать актуальный архив серверного ПО из чата стенда/ проекта 
2. опустить контейнеры
> [!todo] 
> <span style="color: #f4a448">*docker-compose down*</span> 
3. перейти в каталог ./images и залоадить новые образы из архива:
> [!todo] 
> <span style="color: #f4a448">*for img in *.img; do docker load -i "$img"; done*</span>  

4. Передобавить конфиги и docker-compose.yml в каталогах
5. Обновить базу данных(перед этим поднять контейнеры) , если апдейтов базы несколько, то применять последовательно от меньшего к большему:
> [!todo] 
> <span style="color: #f4a448">*docker exec -it sentinel_db bash 
>    psql -U postgres -h 127.0.0.1 -p 5432 -d sentinel -f "/opt/db_backup/upd\_название файла"*</span>
