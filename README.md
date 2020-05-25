# Docker-compose with PHP + NGINX
Это пустой проект для создания связки контейнеров докер сервисов (PHP и NGINX) с помощью docker-compose

## Copyright
Мордвинцев О.Ю.  

## Технологии:
- Docker
- Docker-compose
- Backend: php7.4-fpm
- Server: nginx

### Необходимые компоненты
Эти компоненты уже должны быть Вами установлены для локального ( на вашем ПК) развертывания.
- git (Для клонирования репозитория, хотя вы можете и скачать архивом. 
Программа git доступна тут [https://git-scm.com/](https://git-scm.com/ "git"))
- docker (Для создания контейнеров с нужными сервисами. Сразу содержит и docker-compose, т.е. отдельно установки 
не требует. Скачать docker можно тут [https://www.docker.com/](https://www.docker.com/ "docker")    )

## Установка и запуск
1) В корневой директории будущего проекта, где уже будут храниться исполняемые файлы, необходимо выполнить команду в терминале:
    <details>
        <summary>подробнее...</summary>
        - Если Вы в Windows, и устанавливали git по вышеуказанной ссылке со значениями по умолчанию, 
        то в любой директории проводника в контекстном меню есть пункт "Git BASH Here".
        - Если Вы в Windows, то можете в проводнике перейти в нужную директорию, зажать Shift и правую кнопку мыши, 
        где в контекстном меню будет пункт "Открыть окно CMD здесь" или "Открыть окно PowerShell здесь".
        - Если Вы в Linux, то, скорее всего, Вы знаете, что делать, используйте команду "cd" в терминале для перехода 
        в директорию Вашего нового проекта.
    </details>
>`git clone https://github.com/oleg-mordvintsev/docker-compose-nginx-php.git .`  
    <details>
        <summary>подробнее...</summary>
        Обратите внимание на точку в конце, она означает, что файлы скачаются в директорию, из которой 
        выполняется команда. Если Вы находитесь в директории проекта, но хотите установить в под директорию, 
        то используйте вместо точки название/путь до вложенной директории, к примеру: 
        `git clone https://github.com/oleg-mordvintsev/docker-compose-nginx-php.git directoryInner/directory` 
    </details>

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
