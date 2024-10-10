# Тестовое задание в Robotics Center [Fullstack developer]

## Описание задания:
Вам необходимо разработать микросервисное приложение для управления очередью воспроизведения аудио. Приложение должно предоставлять функциональность для управления аудиофайлами, добавления их в очередь и воспроизведения. Одновременно может воспроизводиться только один звук. Пользователи могут добавлять звуки в очередь, удалять их и управлять воспроизведением. Очередь воспроизведения должна отображаться в реальном времени у всех пользователей. Пользователи могут добавлять звуки в очередь через веб-интерфейс.

### Схема приложения:
![Схема](/scheme.jpg)

### Основные требования:
- Воспроизведение: управление воспроизведением происходит через отдельный сервис, с использованием `gRPC`. Также необходимо реализовать заглушку, работающую через тот же контракт, но не воспроизводящую звуки, лишь эмулирующую воспроизведение. Предполагается, что контракт является python модулем, сгенерированным из proto-файла.

- Очередь аудио: пользователи могут добавлять звуки в очередь, которая формируется с использованием очереди внутри скрипта сервиса **player service**, либо в `Apache Kafka` или `RabbitMQ`

- Авторизация пользователей: через `JWT` токены с сохранением данных в базе данных (PostgreSQL).

- Очередь воспроизведения: должна отображаться в режиме реального времени у всех пользователей с использованием `WebSockets`. Каждый пользователь может добавлять новые звуки в очередь. По желанию может быть применен `Redis` для хранения данных о текущем состоянии очереди с определенным TTL.

- Фронтенд: должен быть реализован на `React`. Должен быть реализован функционал регистрации и авторизации, добавления звуков в очередь, отображения очереди в реальном времени и управления воспроизведением.

- Бэкенд: должен быть реализован на `FastAPI`. Для работы с базой данных используется `SQLAlchemy`. В случает, если выбрана реализация очереди через внутреннюю очередь, то взаимодействие с **player service** должно быть реализовано через `REST`.


### Требования к реализации:
Сервисы реализуются на языке `Python` с использованием `FastAPI` и `AsyncIO`. Для работы с базой данных используется `SQLAlchemy` ORM. Взаимодействие с сервисами воспроизведения должно быть организовано по `gRPC` с единым `protobuf` контрактом. Для хранения пользователей используется PostgreSQL. Авторизация пользователей должна выполняться через `JWT` токены. Для взаимодействия с фронтендом предполагается использование `WebSockets` и `REST API`. Контракты `REST API` должны быть описаны в формате `OpenAPI` и доступны через `Swagger UI`. Клиентская часть реализуется на `React`.
Для всех сервисов предполагается использование одного общего `Docker`-файла на базе **ubuntu:22.04** (допускается multi-stage сборка нескольких образов). Запуск всех сервисов должен быть организован через `docker-compose`.

### Дополнительные задания:
- Реализовать механизм кеширования данных о текущем состоянии очереди воспроизведения с использованием `Redis`. Кеширование должно быть реализовано с использованием TTL и обновляться при изменении состояния очереди.
- Вместо внутренней очереди использовать `Apache Kafka` или `RabbitMQ` для организации очереди воспроизведения.
- Реализовать CI пайплайн с использованием `GitHub Actions` или `GitLab CI`.
- В системе должна быть предусмотрена корректная обработка ошибок, таких как невалидные `JWT` токены, ошибки соединения с базой данных, сбои в воспроизведении звуков и недоступность сервисов.
- Написать тесты (юнит-тесты и интеграционные тесты) для всех ключевых компонентов системы.


## Критерии оценки:
- Чистота и структура кода.
- Соответствие задания требованиям.
- Использование указанных технологий.
- Обработка ошибок.
- Наличие тестов.


### Рекомендации:
Проект должен быть легко развернут с помощью `docker-compose up`. Все сервисы должны быть доступны через `localhost` на различных портах.  
Используйте асинхронные вызовы для всех операций, требующих IO.  
Обеспечьте корректную обработку ошибок, особенно при взаимодействии между микросервисами (gRPC, WebSockets).


## Технологический стек:
- FastAPI
- SQLAlchemy
- AsyncIO
- gRPC
- WebSockets
- JWT
- React
- PostgreSQL
- Docker, docker-compose

### Дополнительно
- Apache Kafka
- RabbitMQ
- Redis

## Обратная связь:
По всем вопросам по выполнению задания можно обращаться в Telegram:
- Дмитрий [@ra3vld](https://t.me/ra3vld)
- Ярослав [@atokagzx](https://t.me/atokagzx)
