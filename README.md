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
- git <details>
        <summary>подробнее...</summary>
        Необходим для клонирования репозитория, хотя вы можете и скачать архивом.<br/>
        Для Windows git доступен тут https://git-scm.com/<br/>
        Для Linux от root выполнить установку. Для Debian подобных (Ubuntu) `apt install git` 
        или Для Red Hat подобных (CentOS) `yum install git`<br/>
        Если Вы не root, то попробуйте команду `sudo -i`, которая поможет выполнить команды Выше от root.
    </details>
- docker <details>
        <summary>подробнее...</summary>
        Для создания контейнеров с нужными сервисами. Сразу содержит и docker-compose, т.е. отдельно установки 
        не требует.<br/>
        Для Windows docker доступен тут https://www.docker.com/<br/>
        Для Linux от root выполнить установку. Для Debian подобных (Ubuntu) `apt install docker`
        или Для Red Hat подобных (CentOS) `yum install docker`<br/>
        Если Вы не root, то попробуйте команду `sudo -i`, которая поможет выполнить команды Выше от root.<br/>
        Так же стоит обратить внимание на инструкцию по установке https://losst.ru/ustanovka-docker-na-ubuntu-16-04
    </details>


## Установка и запуск
1) В корневой директории будущего проекта, где уже будут храниться исполняемые файлы, необходимо выполнить команду в терминале:
    <details>
        <summary>подробнее...</summary>
        - Если Вы в Windows, и устанавливали git по вышеуказанной ссылке со значениями по умолчанию, 
        то в любой директории проводника в контекстном меню есть пункт "Git BASH Here".<br/>
        - Если Вы в Windows, то можете в проводнике перейти в нужную директорию, зажать Shift и правую кнопку мыши, 
        где в контекстном меню будет пункт "Открыть окно CMD здесь" или "Открыть окно PowerShell здесь".<br/>
        - Если Вы в Linux, то, скорее всего, Вы знаете, что делать, используйте команду "cd" в терминале для перехода 
        в директорию Вашего нового проекта.<br/>
        - Обратите внимание на точку в конце, она означает, что файлы скачаются в директорию, из которой
        выполняется команда. Если Вы находитесь в директории проекта, но хотите установить в под директорию,
        то используйте вместо точки название/путь до вложенной директории, к примеру:<br/>
        `git clone https://github.com/oleg-mordvintsev/docker-compose-nginx-php.git directoryInner/directory`
    </details>
    
>`git clone https://github.com/oleg-mordvintsev/docker-compose-nginx-php.git .`  

2) После того, как git получил необходимые файлы, надо запустить проект сследующей командой:
    <details>
        <summary>подробнее...</summary>
        - up - Создать и запустить контейнеры<br/>
        - --build - Создать или пересоздать контейнеры<br/>
        - --remove-orphans - Удаляем контейнеры с сервисами проекта, которых нет в Compose файле
    </details>

>`docker-compose up --build --remove-orphans`  


---




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
