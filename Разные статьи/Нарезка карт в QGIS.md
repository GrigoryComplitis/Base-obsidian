после запуска открывается окно, создаем новый проект, выбираем 1 кнопку во 2 ряду  

![](https://complitech.aspro.cloud/files/download/a6e8e10d-f70b-11ee-919e-fa163e2ff576)

далее выбираем XYZ tiles -> hibrid

![](https://complitech.aspro.cloud/files/download/1c291f4e-f70c-11ee-919e-fa163e2ff576)

Окроется карта мира, дальше нужно приближать до нужного объекта

Если hybrid нет, то выполнить:  
создать подключение  

![](https://complitech.aspro.cloud/files/download/4cdf5cb5-3787-11ef-919e-fa163e2ff576)

  
задать имя вставить ссылку на гибрид в "адрес" [https://mt1.google.com/vt/lyrs=y&x=%7Bx%7D&y=%7By%7D&z=%7Bz%7D  
](https://mt1.google.com/vt/lyrs=y&x=%7Bx%7D&y=%7By%7D&z=%7Bz%7D)

![](https://complitech.aspro.cloud/files/download/ca79a5ec-3787-11ef-919e-fa163e2ff576)

задать макс. уровень масштаба 20 и нажать "ок"  

ВНИМАНИЕ!!! НАРЕЗКУ ПРОВОДИТЬ МЕЖДУ 9 И 20 СЛОЯМИ(ЗУМОМ)

![](https://complitech.aspro.cloud/files/download/90c1c20f-f70c-11ee-919e-fa163e2ff576)

как нашли нужный объект и настроили зум, начинаем резать, для этого в меню справа вводим xyz и выбираем Generate XYZ tiles(Directory)

![](https://complitech.aspro.cloud/files/download/b4054021-f70d-11ee-919e-fa163e2ff576)

далее в поле координат указываем 2 вариант 

![](https://complitech.aspro.cloud/files/download/09689c7f-f70e-11ee-919e-fa163e2ff576)

zoom выставляем минимум 9(не меньше) максимум 20 и в конце окна выбираем директорию

![](https://complitech.aspro.cloud/files/download/58e542cf-f70e-11ee-919e-fa163e2ff576)

и нажимаем run

нарезка идет примерно полчаса

![](https://complitech.aspro.cloud/files/download/974bd401-f70e-11ee-919e-fa163e2ff576)

после нарезки файлы карты будут выглядеть так

![](https://complitech.aspro.cloud/files/download/baf3693c-f710-11ee-919e-fa163e2ff576)
нарезанную карту(папки с 9 по 20) именно в таком виде помещаем в клиент сентинела map /resources/titles/satellite

![](https://complitech.aspro.cloud/files/download/87df3f5d-f711-11ee-919e-fa163e2ff576)