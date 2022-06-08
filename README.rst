.. role:: shell(code)
   :language: shell

Разработка REST API-сервиса посредством языка Python
===========
Приложение упаковано в Docker-контейнер

Внутри Docker-контейнера доступны две команды: :shell:`analyzer-db` — утилита
для управления состоянием базы данных и :shell:`analyzer-api` — утилита для 
запуска REST API сервиса.

Как использовать?
=================
Как применить миграции:

.. code-block:: shell

    docker run -it \
        -e ANALYZER_PG_URL=postgresql://user:hackme@localhost/analyzer \
        timofeevadaria/coursework analyzer-db upgrade head

Как запустить REST API сервис локально на порту 8081:

.. code-block:: shell

    docker run -it -p 8081:8081 \
        -e ANALYZER_PG_URL=postgresql://user:hackme@localhost/analyzer \
        timofeevadaria/coursework

Все доступные опции запуска любой команды можно получить с помощью
аргумента :shell:`--help`:

.. code-block:: shell

    docker run timofeevadaria/coursework analyzer-db --help
    docker run timofeevadaria/coursework analyzer-api --help


Разработка
==========

Быстрые команды
---------------
* :shell:`make` Отобразить список доступных команд
* :shell:`make devenv` Создать и настроить виртуальное окружение для разработки
* :shell:`make postgres` Поднять Docker-контейнер с PostgreSQL
* :shell:`make lint` Проверить синтаксис и стиль кода с помощью `pylama`_
* :shell:`make clean` Удалить файлы, созданные модулем `distutils`_
* :shell:`make test` Запустить тесты
* :shell:`make sdist` Создать `source distribution`_
* :shell:`make docker` Собрать Docker-образ
* :shell:`make upload` Загрузить Docker-образ на hub.docker.com

Как подготовить окружение для разработки?
-----------------------------------------
.. code-block:: shell

    make devenv
    make postgres
    source env/bin/activate
    analyzer-db upgrade head
    analyzer-api

После запуска команд приложение начнет слушать запросы на 0.0.0.0:8081.


Как запустить нагрузочное тестирование?
---------------------------------------
Для запуска `locust`_ необходимо выполнить следующие команды:

.. code-block:: shell

    make devenv
    source env/bin/activate
    locust

После этого станет доступен веб-интерфейс по адресу http://localhost:8081

.. _locust: https://locust.io
