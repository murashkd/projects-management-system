Система управления проектами
============================
Основаная цель: разработать систему управления проктами

Блоки задач
-----------
- Разработка модуля application
- Разработка модуля dto
- разработка модуля buisness
- разработка модуля web

Модуль application
===========
Cодержит класс конфигурации MainApplication.java, помеченый аннотацией @SpringBootApplication

Модуль web
===========
Содержит классы контроллеров. 

Методы контроллеров служат для обработки веб-запросов. Они взаимодействуют с сервисным уровнем, чтобы завершить работу, которую необходимо выполнить. 
После завершения обработки объектом сервисного уровня контроллер отвечает за обновление 
и создание объекта model и выбирает представление, которое пользователь увидит следующим, в качестве ответа.

EmployeeController
------------------
Реализуемые сервисы

**Создание сотрудника**

- Запрос: POST/employee

- Метод запроса: POST

- URL сервиса: /employee


**Изменение сотрудника**

- Запрос: PUT/employee/{:id}

- Метод запроса: PUT

- URL сервиса: /employee/{:id}


**Удаление сотрудника**

- Запрос: DELETE/employee/{:id}

- Метод запроса: DELETE

- URL сервиса: /employee/{:id}


**Получение карточки сотрудника**

- Запрос: GET/employee/{:id}

- Метод запроса: GET

- URL сервиса: /employee/{:id}


**Поск сотрудников**

- Запрос: GET

- Метод запроса: GET

- URL сервиса:

ProjectController
------------------
Реализуемые сервисы

**Создание проекта**

- Запрос: POST/project

- Метод запроса: POST

- URL сервиса: /project

**Изменение проекта**

- Запрос: PUT/project/{:id}

- Метод запроса: PUT

- URL сервиса: /project/{:id}


**Перевод в другое состояние проекта**

- Запрос: PUT/project/status/{:id}

- Метод запроса: PUT

- URL сервиса: /project/status/{:id}

**Поск проектов**

- Запрос: GET

- Метод запроса: GET

- URL сервиса: ?
  EmployeeController

TaskController
------------------
...

TeamController
------------------
...

AuthenticationController
-------------------------
...

Модуль buisness
================

models
--------
Содержит классы сущностей.
Сущности в JPA — это не что иное, как POJO, представляющие данные, 
которые могут быть сохранены в базе данных. Сущность представляет собой таблицу, 
хранящуюся в базе данных. Каждый экземпляр сущности представляет собой строку в таблице.

Сотрудник(Employee)
--------------------

| Наименование поля | Тип поля |                                                         Комментарий |
|-------------------|:--------:|--------------------------------------------------------------------:|
| id                |   UUID   |                       Уникальный идентификатор сотрудника в системе |
| position          |  Строка  |                              Должнось сотрудника. Обязательное поле |
| account           |    ?     |                                Учетная запись. Не Обязательное поле |
| lastname          |  Строка  |                               Фамилия сотрудника. Обязательное поле |
| firstname         |  Строка  |                                   Имя сотрудника. Обязательное поле |
| middlename        |  Строка  |                           Отчество сотрудника. Не обязательное поле |
| Email             |  Строка  |                              Email сотрудника. Не обязательное поле |
| status            |  Строка  | Фиксированый набор значений(Активный, Удаленный). обязательное поле |

Проект(Project)
-------------------

| Наименование поля | Тип поля |                                                                                        Комментарий |
|-------------------|:--------:|---------------------------------------------------------------------------------------------------:|
| Код проекта/id    |   UUID   |                                                                   Уникальный идентификатор проекта |
| projectName       |  Строка  |                                                            Наименование проекта. Обязательное поле |
| description       |  Строка  |                                                                               Не обязательное поле |
| projectStatus     |  Строка  | Фиксированный список статусов(Черновик, В раззработке,В тестировании, Завершен). Обязательное поле |

Команда(Team)
-------------------

| Наименование поля    | Тип поля | Комментарий |
|----------------------|:--------:|------------:|
| Код/id               |   UUID   |      |
| Руководитель проекта |    |         |
| Аналитик             |    |          |
| Разработчик          |    |           |
| Тестировщик          |    |          |

Задача(Task)
-------------------
| Наименование поля             |   Тип поля   |                                                                           Комментарий |
|-------------------------------|:------------:|--------------------------------------------------------------------------------------:|
| id                            |     UUID     |                                                       Уникальный идентификатор задачи |
| taskName                      |    Строка    |                                                Наименование задачи. Обязательное поле |
| description                   |    Строка    |                                                 Описание задачи. не обязательное поле |
| executor                      |   Employee   | Исполнитель задачи сотрудник.Не обязательное поле.Только сотрудник в статусе активный |
| Трудозатраты                  |   Integer    |                                                                                    $1 |
| Крайний срок                  |   Employee   |                                                                                    $1 |
| Статус                        | Перечесление |                                                                                    $1 |
| Автор задачи                  |              |                                                                                    $1 |
| Дата создания                 |              |                                                                                    $1 |
| Дата последнего<br/>изменения |              |                                                                                    $1 |

Services
------
В модуле services находится бизнес-логика приложения
Мы используем аннотацию @Service , чтобы указать, что класс принадлежит этому уровню.
Аннотация @Service используется с классами, которые предоставляют некоторые бизнес-функции.
Контекст Spring автоматически обнаружит эти классы, когда используется конфигурация на основе аннотаций и сканирование путей к классам.

    
Repositories
------------
Содержит интерфейсы которые используют JPA Entity для взаимодействия с ней. репозиторий
обеспечивает основные операции по поиску, сохранения, удалению данных.


dto
----
Содержит классы dto, которые являются объектами для передачи данных. Данными являются поля в классе.
Dto обеткты не содержат методы, только поля, геттеры/сеттеры, и конструкторы.
