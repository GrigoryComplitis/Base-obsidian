1. Выключить камеры в вебе

2. Опустить контейнеры: docker-compose down

4. При замене файлов убрать лишние символы и переименовать env в .env

3. Удалить старую сеть 
> [!todo] 
> <span style="color: #f4a448">*docker network rm mail_net*</span>

4. Создать новую 
> [!todo] 
> <span style="color: #f4a448">*docker network create --subnet 172.51.0.0/16 mail_net*</span>

5. Скачать недостающие образы из .env: 
> [!todo] 
> <span style="color: #f4a448">*docker load -i "image"*<span>

или забрать актуальные образы со стенда с помощью
> [!todo] 
> <span style="color: #f4a448">*docker save -o ".img" "image\_name" 

в папке, где образы прописать:
> [!todo] 
> <span style="color: #f4a448">*for img in \*.img; do docker load -i "$img"; done*</span> 

6. Подменить файлы и запустить контейнеры: docker-compose up -d