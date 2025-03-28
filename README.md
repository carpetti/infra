# Carpetti
![UML Diagram](https://www.plantuml.com/plantuml/png/dLXVQzH047yFv3iivuEAz4NmfTHIFH4VB5IBb89Gqjms3Sq_DqdRGmGL5C47GLzyyZEKQl6ijlqAUz_8sTsOsztC9V4EZcHdV_kRcTsPsRbRomkF5MKSkKv-42QPnxoOCEeNNX94T6Lbb-vxXs7ALbV9IzSXy65fcOo6AKie8xVlkCuhrt6TwuH_urVJr_oC_u3lR_XUy0a_8_mFFCvXudBwXf_1yvHFuEsIdxfEhOOCSieEGv_kP2prQPuFY9UJIhQXH6HbPJtqMLf9mPvhzx8i2dsl2DC49OipdMSzMu32Px7ECMJn0YH7T5SdsQAx2v3iXH7LMHx2U04QsE33S4IPjSDIjWWTPNcO5mQR4Yr0bjF4icnJIhgesiBlYf_mSmYyjusGopp_m0lepZYEfCfgl1r7e6z33OIgW7bZT26ZMQglV0hZdalB8ZIKFeDnpwLmW8MXTaC8UYxsFN-VFazkvEEyeB4QtjJ9XaBIaspVIqPLJ5QYHrBIS_cBafQQBN9esF94IFewbYPxOM1u8YNOSXakNw0WoPYOVeGm4P4p_Q2YPlh934vb7cpxyHYifSbXEbPcgfaDCG5gDkL8Q8d2OB_OZKgAyO2XUHa1aNhHcOPIyXzKrM4oEWfpWwWwn9uyKHe4b07HGm0aXSxqM4xre88I1mH942R7v1QvbmHbv375T2JBNHT1LVY1PEZ5SC5uLIZKnHyba4VvcV-499_0JNCfi__Nz0qSxQdCV_lI8NpIg0b6w2-DqgDaQLNVIQ76kel-eRJCxyA85E_2o5Jk0bKsjODK9dQXP8PrwfE9f6q2NAHp87C1bZbDWEbvSzwqj3bld41pMcr-3H3NUEkkOW3JHmHXEOaWJ2yHWEac0Z3yHEOjHqMhqUee1Z0THH2MemZ2T1G1c8uY0CDHPDvoL7P3xOvW4CiJ36AwWY6CpCO0st5arX3LRRMREm_Mp6mKrYWbACekIYYeEgiPhchmEkp7KRRvEAgolePLVM2xHXnaASH1vcxXc7eREgyS0cyNig6ua9Y9k8Oc4d86mnCXSft1C0hXkXtKUk2YT9qZBTIr1WDiqxgD6b3NWTRvBK6Cr0pp3D1icmEnZstmuFwWvPhKSgCByoy8Et6sHJXC7MKNQZsRVmcgSLl-cYkxSPRbsctL6s7i948mCng2zIk_a97t7HgXa-bxqU4I_dtM_qxV6Vql_pL_kxG-jGEaEaVKHcpU24iCiDN82mjW55uKqJmG56M5DWgoAeI9SPs81W0W4Ts3GxmhFwxJ-16xJ7I10Cn-gYoJwftSM4z7PKHlYlcw1rucwfKCqpXB4oWZCprKr3kXNrYo1a_vvyvV)



# Архитектура
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
  Основной сервис для работы с базой данных:
  - мс entiy.

### [service_sender](https://github.com/carpetti/service_sender)
  Отправка уведомлений:
  - Уведомления через Telegram, email и VK.

### [process_adapter](https://github.com/carpetti/process_provider)

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

# Пакеты

![UML Diagram](https://www.plantuml.com/plantuml/png/SoWkIImgAStDuUMABaXCpavCJuqlBSdCSIWpr3FICufLqDMrKu3B9EVdfMMcm-I8qfAHc9UIauhGWgIfABKW7o9XJAmzkBKK5EMNv9Eaex0qjJIL91t8laJn2OfH-Bs2f2ivCJc3T5sLkL0t60357LBpKe2H1m00)
*1.2 - minor update*

# Потоки данных
### Клиентский поток
```
Клиент → Nginx (web) → service_crm → service_persist → DB.
Клиент → Nginx (web) → service_web → service_persist → DB.
```

### Поток процессов
```
service_process → service_file → Файловое хранилище/облако.
service_process → service_provider (через топики RabbitMQ) → Поставщики.
service_process → service_persist → DB.
service_process → service_sender (через топики RabbitMQ) → Telegram/Email/VK.
service_process → service_mp (через топики RabbitMQ) → Маркетплейсы (Ozon, Wildberries, Yandex, Sber).
service_process → Camunda (process) → Запуск процессов.
```

### Взаимодействие сервисов
```
service_provider → service_process (через RabbitMQ).
service_provider → service_persist (через gRPC).
service_mp → service_persist (через gRPC).
service_mp → service_process (через RabbitMQ и gRPC).
service_mp → service_file (через gRPC).
```



> ACF-FEKOZ-2024-2025
