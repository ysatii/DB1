# DB1
Домашнее задание к занятию «Базы данных»



# Домашнее задание к занятию «Базы данных, их типы» - Мельник Юрий Александрович


## Задание 1

### СУБД
## Кейс

Крупная строительная компания, которая также занимается проектированием и девелопментом, решила создать правильную архитектуру для работы с данными. Ниже представлены задачи, которые необходимо решить для каждой предметной области.

Какие типы СУБД, на ваш взгляд, лучше всего подойдут для решения этих задач и почему?

1. `Бюджетирование проектов с дальнейшим формированием финансовых аналитических отчётов и прогнозирования рисков. СУБД должна гарантировать целостность и чёткую структуру данных.`
 
	1. `Хеширование стало занимать длительно время, какое API можно использовать для ускорения работы?`
 
2. `Под каждый девелоперский проект создаётся отдельный лендинг, и все данные по лидам стекаются в CRM к маркетологам и менеджерам по продажам. Какой тип СУБД лучше использовать для лендингов и для     CRM? СУБД должны быть    гибкими и быстрыми.`
	1. `Можно ли эту задачу закрыть одной СУБД? И если да, то какой именно СУБД и какой реализацией?`

3. `Отдел контроля качества решил создать базу по корпоративным нормам и правилам, обучающему материалу и так далее, сформированную согласно структуре компании. СУБД должна иметь простую и понятную структуру.`
	1. `Можно ли под эту задачу использовать уже существующую СУБД из задач выше и если да, то как лучше это реализовать?`
	
	
	
	
	

## Решение 1
1. ` `
 





## Задание 2
## Транзакции


2.1. `Пользователь пополняет баланс счёта телефона, распишите пошагово, какие действия должны произойти для того, чтобы транзакция завершилась успешно. Ориентируйтесь на шесть действий.`  

2.1*. `Какие действия должны произойти, если пополнение счёта телефона происходило бы через автоплатёж?`  


## Решение 2

2. `Пользователь пополняет баланс счёта телефона, распишите пошагово, какие действия должны произойти для того, чтобы транзакция завершилась успешно. Ориентируйтесь на шесть действий.`  
 Машина 1  
 ![alt text](https://github.com/ysatii/Keepalived/blob/main/img/image2.jpg)  
 Машина 2  
 ![alt text](https://github.com/ysatii/Keepalived/blob/main/img/image2_1.jpg)

2. `Установим сервис на обе машины`
 ```
 sudo apt-get install keepalived
 ```  
 ![alt text](https://github.com/ysatii/Keepalived/blob/main/img/image2_2.jpg)

3. `Произвдем настройку конфигурационных файлов`  
 Сервер1 , мастер к виду   
  ```
  vrrp_instance VI_1 {
    	state MASTER
    	interface enp0s3
    	virtual_router_id 15
    	priority 255
    	advert_int 1

    	virtual_ipaddress {
          	10.0.2.100/24
    	}
 }
 
 ```  
  ![alt text](https://github.com/ysatii/Keepalived/blob/main/img/image2_3.jpg)  
 Сервер 2, бэпап к виду   
 ```
 
 vrrp_instance VI_1 {
    	state BACKUP
    	interface enp0s3
    	virtual_router_id 15
    	priority 200
    	advert_int 1

    	virtual_ipaddress {
          	10.0.2.100/24
    	}

 }
 
 ```
 
 ![alt text](https://github.com/ysatii/Keepalived/blob/main/img/image2_4.jpg)  
 
4. `Произведем запуск сервисов`  
 Сервер 1, мастер  
 ![alt text](https://github.com/ysatii/Keepalived/blob/main/img/image2_5.jpg)  
 ![alt text](https://github.com/ysatii/Keepalived/blob/main/img/image2_6.jpg)  
 
 Сервер 2, бэкап   
 ![alt text](https://github.com/ysatii/Keepalived/blob/main/img/image2_7.jpg)  
 ![alt text](https://github.com/ysatii/Keepalived/blob/main/img/image2_8.jpg)  
 Заметим что плаващий  10.0.2.100 только на сервер1, но с сервер 2 пинг проходит на 10.0.2.100 
 
5. `Произведем проверку сервиса Keepalived`  
 Остановим сервис на сервер1 и проверим адреса  
 ![alt text](https://github.com/ysatii/Keepalived/blob/main/img/image2_9.jpg)  
 
 Произведем пинг с сервер 1 на плавающий 10.0.2.100  
 ![alt text](https://github.com/ysatii/Keepalived/blob/main/img/image2_10.jpg)  
 
 Сервис на второй машине перешол в состояние мастер
 ![alt text](https://github.com/ysatii/Keepalived/blob/main/img/image2_11.jpg)  
 
 Запустим сервис снова на первой машине  
 ![alt text](https://github.com/ysatii/Keepalived/blob/main/img/image2_12.jpg) 
 сервер 1 Мастер восстановил свою работоспособность! 
 
6. `установим nginx  на оба сервера!`  
 ```
 sudo apt-get install nginx
 ```
 ![alt text](https://github.com/ysatii/Keepalived/blob/main/img/image2_13.jpg)  
 
7. `произведем проверку работоспособности nginx, проверим работу сервиса nginx на плавающем ip `
 Изменим страницу по умолчанию для первого сервера, ip 10.0.2.15  
 ![alt text](https://github.com/ysatii/Keepalived/blob/main/img/image2_14.jpg)  
 
 Для второго сервера сервера, ip 10.0.2.4  
 ![alt text](https://github.com/ysatii/Keepalived/blob/main/img/image2_15.jpg)  
 
 Проверим доступность на всех ip адресах
 на сервер 1  
 ![alt text](https://github.com/ysatii/Keepalived/blob/main/img/image2_16.jpg)  
 
 На сервер 2  
 ![alt text](https://github.com/ysatii/Keepalived/blob/main/img/image2_17.jpg)  

 и на плавающем ip  
 ![alt text](https://github.com/ysatii/Keepalived/blob/main/img/image2_18.jpg)  
 Как и ожидалось плавающий ip это сервер 1
 
8. `отслеживание работоспособности проверка состояния nginx.` 
 Приведем конфигурационный файл сервера 1 к виду
 ```
 vrrp_track_process check_nginx {
   	process "nginx"}

 vrrp_instance VI_1 {
    	state MASTER
    	interface enp0s3
    	virtual_router_id 15
    	priority 255
    	advert_int 1

    	virtual_ipaddress {
            	10.0.2.100/24
    	}
    	track_process {
            	check_nginx
    	}
 
 }
 ```
 ![alt text](https://github.com/ysatii/Keepalived/blob/main/img/image2_19.jpg)  
 
 Приведем конфигурационный файл  сервера 2 к виду
 ```
 vrrp_track_process check_nginx {
   	process "nginx" }

 vrrp_instance VI_1 {
    	state BACKUP
    	interface enp0s3
    	virtual_router_id 15
    	priority 200
    	advert_int 1

    	virtual_ipaddress {
            	10.0.2.100/24
    	}
    	track_process {
               	check_nginx
    	}

 }
 ```
 
 ![alt text](https://github.com/ysatii/Keepalived/blob/main/img/image2_20.jpg)  
 
 Перезапустим сервисы
 
 ```
 sudo systemctl restart keepalived
 ```
 Сервер 1  
 ![alt text](https://github.com/ysatii/Keepalived/blob/main/img/image2_21.jpg)  

 Сервер 2  
 ![alt text](https://github.com/ysatii/Keepalived/blob/main/img/image2_22.jpg)  
 
 Принудительно остановим nginx на первом сервере 1 и проверим работоспособность
 
 ![alt text](https://github.com/ysatii/Keepalived/blob/main/img/image2_23.jpg)  
 ![alt text](https://github.com/ysatii/Keepalived/blob/main/img/image2_24.jpg)  
 
 Работоспособность на сервере2 

 ![alt text](https://github.com/ysatii/Keepalived/blob/main/img/image2_25.jpg)  
 ![alt text](https://github.com/ysatii/Keepalived/blob/main/img/image2_26.jpg)  
 
 Плавающий IP переместился на сервер 2  
 
9. `отслеживание файла index.html, в случаи его отсутствия осуществляем перенос плающего IP`  
  
 Листинг /home/lamer/check_nginx.sh"
 ```
 #!/bin/bash
 if [[ $(netstat -tuln | grep LISTEN | grep :80) ]] && [[ -f /var/www/html/index.html ]]; then
        exit 0
 else
        exit 1
 fi
 ```
 Приведен файл настроек сервер 1 к виду   
 
 ```
  vrrp_script check_script {
      script "/home/lamer/check_nginx.sh"
      interval 3
  }

#vrrp_track_process check_nginx {
#       process "nginx"}

 vrrp_instance VI_1 {
    	state MASTER
    	interface enp0s3
    	virtual_router_id 15
    	priority 255
    	advert_int 1

    	virtual_ipaddress {
          	10.0.2.100/24
    	}
#        track_process {
#	        check_nginx
        
#        }       
        track_script {
                   check_script
        }
 
 }

 ```  
 Перезапустим сервис   
 
 ```
 sudo systemctl status keepalived
 ```  
 ![alt text](https://github.com/ysatii/Keepalived/blob/main/img/image2_27.jpg)  
 ![alt text](https://github.com/ysatii/Keepalived/blob/main/img/image2_28.jpg)  
 
 Принудительно выключаем ngnix делая недоступным порт 80 на сервер 1  
 ![alt text](https://github.com/ysatii/Keepalived/blob/main/img/image2_29.jpg)  
 
 Запустим nginx, видим что сервис вернул   keepalived свою работоспособность не сервер 1  
 ![alt text](https://github.com/ysatii/Keepalived/blob/main/img/image2_30.jpg)  
 
 Просмиотрим лог  
 ![alt text](https://github.com/ysatii/Keepalived/blob/main/img/image2_31.jpg)  
 
 Удалим файл /var/www/html/index.html   
 Сервер 1, nginx в работе  
 ![alt text](https://github.com/ysatii/Keepalived/blob/main/img/image2_32.jpg)  
 
 Сервер 2 в работе  
 ![alt text](https://github.com/ysatii/Keepalived/blob/main/img/image2_33.jpg)  
 
 При этом плавающий ип стал работать на сервер2  
 ![alt text](https://github.com/ysatii/Keepalived/blob/main/img/image2_34.jpg)  
 
 Создадим файл index.html и проверим сотояние Keepalived на сервере 1
 ![alt text](https://github.com/ysatii/Keepalived/blob/main/img/image2_35.jpg)  
 
 Работа сервиса возвращена!
 9. `Листинги `  
  -  конфигурационный файл сервер1  [файла](https://github.com/ysatii/Keepalived/blob/main/keepalived.conf_server1) 
  -  конфигурационный файл сервер2  [файла](https://github.com/ysatii/Keepalived/blob/main/keepalived.conf_server2) 
  - скрипт для проверки состояния порта 80, и файла index.html [файла](https://github.com/ysatii/Keepalived/blob/main/check_nginx.sh) 
