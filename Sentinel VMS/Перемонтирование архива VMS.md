В случае если требуется примонтировать архив к другому разделу, требуется выполнить следующий порядок действий:

1. На web VMS освободить архив по кнопке "Освободить память":

![](https://complitech.aspro.cloud/files/download/deaae6e7-45ae-11ef-919e-fa163e2ff576)

2. Опустить контейнеры: docker-compose down

3. Отмонтировать архив нынешний, для этого посмотреть в docker-compose файле куда он примонтирован, обычно в /storage, командой: sudo umount /storage

4. Командой lsblk проверить произошло ли отмонтирование

5. Командой: sudo mount /dev/<что монтируем> /<куда монтируем>

6. В docker-compose.yml в разделе sentinelvms и sentinelvmsarchive поменять значения в тех же местах, где сейчас стоит /Video

![](https://complitech.aspro.cloud/files/download/c720e536-45af-11ef-919e-fa163e2ff576)

![](https://complitech.aspro.cloud/files/download/d153a1c8-45af-11ef-919e-fa163e2ff576)

7. Тоже самое сделать в конфиге, как на примере(изменить раздел path_storage):

![](https://complitech.aspro.cloud/files/download/ece9cb93-45af-11ef-919e-fa163e2ff576)