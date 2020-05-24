# Seagem
SeaGem - рабочее название "морского проекта" (поиск и бронирование апартаментов в Крыму).  
Предыдущие названия: Morenaprokat.ru, Pojv.ru

## Copyright @
2016 - 2020 Коваленко А., Баулькин Р., Еловик Е.  
Разработчики - Свердлов М., Куликов С.  
Экспертиза - Мордвинцев О.  

## Технологии:
- Beckend: PHP-fpm-7.4, Symphony 4, Doctrine, MySQL 8
- Frontend: Wordpress

## Системные требования для локального развертывания
#### Внимание: компоненты ниже должны быть установлены в рабочей OS Linux (не в контейнерах)
- git
- docker
- docker-compose

## Инструкция по установке 
1) В рабочей Linux среде выполнить в терминале клонирование базового проекта из стартовой ветки:

>`git clone https://github.com/msverdlov/seagem/tree/Template-for-first-deploy-to-local-branch /home/seagem`  
  
2) Перейти в каталог:
>`cd /home/seagem`  

3) Отредактироватаь файл .env, вставить значение своих переменных.  
После добавить `.env` в файл .gitignoge  
  
4) Необходимо забилдить проект и тут же стартануть все сервисы  
   с удалением контейнеров которых больше нет в docker-compose.yml:
>`docker-compose up --build --remove-orphans`
##### После успешного завершения в консоле будет ответ:
> `Creating seagem-nginx   ... done`  
> `Creating seagem-php-cli ... done`  
> `Creating seagem-php-fpm ... done`  
> `Creating seagem-mysql ... done`  
  
####   Внимание: все последуюшие действия (пока сервисы подняты)  выполняются именно в контейнере
5) Перейти в каталог:
>`cd /home/seagem/docker/php-cli`  
  
6) Заходим в контейнер с php-cli:
> `docker exec -it seagem-php-cli bash`  
  
7) Создаем в контейнере проект Symfony с шаблонами для сайта:
> `composer create-project symfony/website-skeleton app`  
  
8) После установки выполняем несколько команд, чтобы избавиться от вложенности папок:
> `mv /symfony/app/* /symfony`  
> `mv /symfony/app/.* /symfony`  
> `rm -Rf app`  
  
9) Открываем в браузере `localhost` и если все установлено правильно  
видим **Welcome to Symfony 5.0.8**
