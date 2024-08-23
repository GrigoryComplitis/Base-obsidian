1. Выключить камеры в вебе

2. Опустить контейнеры: docker-compose down

3. При замене файлов убрать лишние символы и переименовать env в .env

4. Удалить старую сеть 
> [!todo] 
> <span style="color: #f4a448">*docker network rm lpr_net*</span>

5. Создать новую 
> [!todo] 
> <span style="color: #f4a448">*docker network create --subnet 172.49.0.0/16 lpr_net*</span> 

6. Скачать недостающие образы из .env: 
> [!todo] 
> <span style="color: #f4a448">*docker load -i "image"*<span>

или забрать актуальные образы со стенда с помощью
> [!todo] 
> <span style="color: #f4a448">*docker save -o ".img" "image\_name"*</span>

в папке, где образы прописать:
> [!todo] 
> <span style="color: #f4a448">*for img in \*.img; do docker load -i "$img"; done*</span> 

7. Подменить файлы и запустить контейнеры: docker-compose up -d
  
