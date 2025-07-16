# Новая инфраструктура:
# [https://github.com/OCCWO/infra/blob/main/README.md](https://github.com/OCCWO/infra/blob/main/README.md)

## Пакеты
![UML Diagram](https://www.plantuml.com/plantuml/png/SoWkIImgAStDuUMABaXCpavCJuqlBSdCSIWpr3FICubLqDMrKu3B9EVdfMMcG-ICOedIaf6ObvAJYj22fAaejI2VH7jmQoaeoY_99qb7OMbgQIf9Ef1zYU8J5AFmUmL9Lt9YSWRfkYfpeMum08exfEQb02CF0000)
*1.2 - minor update*

## Архитектура
Проект построен на основе микросервисной архитектуры, каждый сервис отвечает за определённый функционал и взаимодействует с остальными через gRPC, Consul и очереди сообщений (RabbitMQ). Все сервисы логируют информацию через Fluent и используют Consul для определения адресов, что позволяет масштабировать их горизонтально.

![UML Diagram](https://www.plantuml.com/plantuml/png/ZLNDQjmm4BuR_0vYBsaFeIzGIY0a4AZ1YGyz5grN2IQsR2HvcwK4akPK2Wtq0VeCsz8bctIRliBeZJgMx5t_h9RknPfllXdDIDze3wIYGfLPwdjx1Bx33_qPvlgUw5lzIT_eEtZ2xvs-WJb2iAnWMC1AV_4ztojeV4al61cTy7D1fH9bh4h1HkIZxn7ynNbMv9nnHKPdR9B84Q6IY6erzDFnE571gQKOOy09Swak18jEtnfMOSrXhiESop8rdDWi1umZFird91JvrSpGM6KFyz2iv1Dg4zcrxrrt6e-Oc2OnazjQbjRtlX0vCcppDHPQQ5V8D9amqOinc3CeAzhq87HdPq8cKdMIMyWP4ekiJJyy2vpK3spSfhvZOoVrF4bPctkCjfCi6U-TI6IG_fKSNIacE4r9D9EAPLkl9g3YagaYfR7TFzlO0svK5aMQuFdOhHjhg1Q4kPBa1NRywbZaN65vBwruhAkk5EVi6pp079QmWcVuXVFqQERg9yxNlU_LRBA__wOHflaOe7q10zISzORHTgqlU4FTvQvjGzdCMLUzE-DRb6QQtT7sthVurrFdZgrqxlOs4kdDKAVqPXPtSNhj1U5_U7jzTsCwBLV6zgEszNVIDGyrFEklA9u_AA45GUqu58LEVKiGd-CZ_WGBHF_2Ryl0Y1KisnM-hdRgJCDQyBqpgz-Y0opG_7ly0m00)



### Основные компоненты и технологии:
- Proxy: Envoy для маршрутизации запросов между клиентом и микросервисами.
- Cache: Redis для кэширования данных.
- Queue: RabbitMQ для взаимодействия между сервисами через топики.
- Process Engine: Camunda для выполнения бизнес-процессов.
- Database: PostgreSQL, размещённая в облаке, для хранения данных.
- Frontend: Angular проект, собранный в Docker контейнере и обслуживаемый Nginx.

### Взаимодействие клиентов:
- Клиенты обращаются к Nginx, который маршрутизирует запросы к соответствующим микросервисам (например, service_crm или service_web) через Envoy и gRPC.
- Основной поток данных направляется в service_persist для работы с базой данных.



# Список микросервисов
### [service_process](https://github.com/carpetti/service_process)
  Основной сервис для обработки сложных бизнес-процессов. Поддерживает следующие процессы:
  - Создание связок товаров между собой.
  - Отложенное создание сущности-связи с маркетплейсами (сохранение внешних ID и других данных).
  - Создание пакетов товаров (упаковка и quantity) для товаров, которые имеют соответствующие флаги от поставщика.
  - Создание новых товаров.
  - Обновление существующих товаров.
  - Алгоритм отложенной публикации данных на service_mp с использованием модели данных.
  - Циклический запуск процесса:
    + Сборка каталога для создания новых товаров.
    + Создание общих категорий и спецификаций товаров.
    + Генерация YML-выгрузок и общих документов.
    + Генерация индивидуальных документов для каждого товара.
  - Сбор и генерация отчётов, метрик, статистики и каналов взаимодействия между микросервисами.

### [service_mp](https://github.com/carpetti/service_mp)
  Обрабатывает взаимодействие с маркетплейсами:
  - Синхронизация данных о товарах и заказах.
  - Публикация данных из service_process через очереди RabbitMQ.
  - Сохранение чеков и документов через service_file.

### [service_crm](https://github.com/carpetti/service_crm), service_web
  Отвечает за обработку клиентских данных:
  - Управление пользовательскими данными, заказами и историями взаимодействий.
  - Взаимодействие с service_persist для хранения данных.
  - Обработка пользовательских запросов.

### [service_file](https://github.com/carpetti/service_file)
  Управление файлами:
  - Обработка файлов для хранения в облаке или локальном файловом хранилище.
  - Генерация документов и YML-выгрузок.

### [service_provider](https://github.com/carpetti/service_provider)
  Работа с поставщиками:
  - Получение данных о товарах и их обновление.

### [service_persist](https://github.com/carpetti/service_persist)
  Основной сервис для работы с базой данных (мс entity).

### [service_sender](https://github.com/carpetti/service_sender)
  Отправка уведомлений:
  - Уведомления через Telegram, email и VK.

### [service_moderation](https://github.com/carpetti/service_moderation)
  Модерация товаров через AI (Gemeni \ GPT o4-mini):
  - Метод модерации товара по указанному промпту.
  - Метод создания описания товара из набора характеристик.

# Модули и пакеты
### Общие пакеты
- package_config: Конфигурационные данные для всех сервисов pb.
- package_proto: proto модели.
- package_util: Утилиты и вспомогательные функции для обработки данных.
- package_cache: of Redis.
- package_queue: of RabbitMQ.
- package_repo: Работа с репозиториями proto.
- package_handle: интерцепторы, хендлеры + дискавери.
- package_yml: Генерация YML-выгрузок.

### Системные компоненты
- system_queue: RabbitMQ - брокер. 
- system_proxy: Envoy.
- system_consul: discovery.
- system_cache: Redis.
- system_logger: Fluent - логирование.

> ACF-FEKOZ-2024-2025 | OCCWO

Репозиторий экосистемы (экземпляр): https://github.com/OCCWO/infra

