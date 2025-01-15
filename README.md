# Домашнее задание к занятию "`Базы данных, их типы`"

---

## Задание 1. СУБД
### Кейс
Крупная строительная компания, которая также занимается проектированием и девелопментом, решила создать правильную архитектуру для работы с данными. Ниже представлены задачи, которые необходимо решить для каждой предметной области.

Какие типы СУБД, на ваш взгляд, лучше всего подойдут для решения этих задач и почему?

### 1.1. Бюджетирование проектов с дальнейшим формированием финансовых аналитических отчётов и прогнозирования рисков. СУБД должна гарантировать целостность и чёткую структуру данных.

### 1.1.* Хеширование стало занимать длительно время, какое API можно использовать для ускорения работы?

### 1.2. Под каждый девелоперский проект создаётся отдельный лендинг, и все данные по лидам стекаются в CRM к маркетологам и менеджерам по продажам. Какой тип СУБД лучше использовать для лендингов и для CRM? СУБД должны быть гибкими и быстрыми.

### 1.2.* Можно ли эту задачу закрыть одной СУБД? И если да, то какой именно СУБД и какой реализацией?

### 1.3. Отдел контроля качества решил создать базу по корпоративным нормам и правилам, обучающему материалу и так далее, сформированную согласно структуре компании. СУБД должна иметь простую и понятную структуру.

### 1.3.* Можно ли под эту задачу использовать уже существующую СУБД из задач выше и если да, то как лучше это реализовать?

### 1.4. Департамент логистики нуждается в решении задач по быстрому формированию маршрутов доставки материалов по объектам и распределению курьеров по маршрутам с доставкой документов. СУБД должна уметь быстро работать со связями.

### 1.4.* Можно ли к этой СУБД подключить отдел закупок или для них лучше сформировать свою СУБД в связке с СУБД логистов?

### 1.5.* Можно ли все перечисленные выше задачи решить, используя одну СУБД? Если да, то какую именно?

Приведите ответ в свободной форме.

### Ответ:

### 1.1 Бюджетирование проектов и финансовые отчёты
**Тип СУБД:** Реляционная СУБД, например, PostgreSQL или MySQL.

**Причина:** Реляционные СУБД обеспечивают целостность данных и строгую структуру. Они поддерживают транзакции, что критично для бюджетирования и финансовых отчётов. Механизмы транзакций и нормализации данных позволяют эффективно управлять данными и предотвращать их несоответствия.

**Хеширование:** Если хеширование стало занимать длительное время, то можно рассмотреть использование Redis в качестве кэша для ускорения операций хеширования. Redis поддерживает быструю работу с хэшами и может существенно ускорить процесс.

### 1.2 Лендинги и CRM
**Тип СУБД для лендингов:** NoSQL СУБД, например, MongoDB.

**Тип СУБД для CRM:** Реляционная СУБД или NoSQL, в зависимости от требований к структуре данных и производительности. PostgreSQL или MongoDB подойдут в зависимости от того, требуется ли строгая схема или гибкость.

**Причина:** Лендинги часто имеют неструктурированные или полуструктурированные данные, что делает NoSQL подходящим вариантом. Для CRM, если требуется сложный анализ и транзакции, реляционная СУБД будет предпочтительнее. Если гибкость и масштабируемость важнее, то NoSQL также будет хорошим выбором.

**Одна СУБД:** Теоретически, можно использовать одну СУБД для обеих задач. Например, MongoDB может использоваться и для лендингов, и для CRM, если есть готвоность работать с гибкой схемой. Однако для полного удовлетворения всех требований может потребоваться комбинация СУБД.

### 1.3 База норм и правил контроля качества
**Тип СУБД:** Реляционная СУБД (например, PostgreSQL).

**Причина:** Реляционные СУБД хорошо подходят для хранения структурированных данных с чёткими связями и иерархией. Это делает их удобными для организации данных о корпоративных нормах, правилах и обучающем материале.

**Использование существующей СУБД:** Можно использовать ту же реляционную СУБД, что и для бюджета (например, PostgreSQL). Она обеспечит целостность данных и структурированное представление.

### 1.4 Логистика и маршруты
**Тип СУБД:** Графовая СУБД, например, Neo4j.

**Причина:** Графовые СУБД отлично справляются с задачами, связанными с управлением сложными связями и маршрутизацией. Они позволяют быстро выполнять запросы, связанные с поиском оптимальных путей и распределением ресурсов.

**Подключение отдела закупок:** Если отдел закупок работает с данными, которые сильно зависят от логистики, можно подключить его к той же графовой СУБД, что и для логистики. Однако, если данные закупок имеют совершенно другую структуру, может быть целесообразно использовать отдельную СУБД и интегрировать её с логистической.

### 1.5 Одна СУБД для всех задач
**Тип СУБД:** Учитывая разнообразие задач, трудно найти одну СУБД, которая бы идеально подошла для всех сценариев. Выбор будет зависеть от приоритетов. Например:

PostgreSQL может использоваться для большинства реляционных задач и поддерживает гибкие типы данных.
MongoDB для неструктурированных данных и гибких схем.
Neo4j для задач, связанных с графовыми данными.

**Заключение:** Использование одной универсальной СУБД может привести к компромиссам в производительности и функциональности. На практике, комбинация специализированных СУБД для разных задач часто оказывается более эффективным решением.

---

## Задание 2. Транзакции
### 2.1. Пользователь пополняет баланс счёта телефона, распишите пошагово, какие действия должны произойти для того, чтобы транзакция завершилась успешно. Ориентируйтесь на шесть действий.

### 2.1.* Какие действия должны произойти, если пополнение счёта телефона происходило бы через автоплатёж?

Приведите ответ в свободной форме.

### Ответ:

### 2.1 Пополнение баланса счёта телефона

**1. Авторизация пользователя:**
Пользователь входит в систему (например, через веб-сайт или мобильное приложение) с использованием своих учетных данных (логин и пароль).
Система проверяет подлинность учетных данных и авторизует пользователя.

**2. Выбор суммы пополнения:**
Пользователь выбирает сумму, на которую хочет пополнить баланс телефона.
Система проверяет, чтобы выбранная сумма была допустимой (например, не ниже минимальной суммы пополнения).

**3. Выбор метода оплаты:**
Пользователь выбирает метод оплаты (например, кредитная карта, электронный кошелек).
Система отображает доступные методы оплаты и запрашивает данные для выбранного метода (например, номер кредитной карты).

**4. Проверка и резервирование средств:**
Система отправляет запрос на проверку и резервирование средств у платежного провайдера (например, банка или платежной системы).
Платежный провайдер проверяет наличие средств на счету пользователя и резервирует их для проведения транзакции.

**5. Пополнение баланса:**
Система обновляет баланс счёта телефона пользователя, добавляя выбранную сумму.
Транзакция записывается в базу данных для ведения учёта и отслеживания.

**6. Подтверждение и уведомление:**
Система отправляет пользователю подтверждение о успешном пополнении баланса (например, через SMS, email или пуш-уведомление).
Платежный провайдер снимает зарезервированные средства с счёта пользователя.

### 2.1.* Пополнение счёта телефона через автоплатёж

**1. Настройка автоплатежа:**
Пользователь настраивает автоплатёж в системе, указывая сумму пополнения, частоту платежей и метод оплаты.
Система сохраняет эти настройки и данные о методе оплаты в защищённом виде.

**2. Триггер автоплатежа:**
В назначенное время система автоматически инициирует автоплатёж в соответствии с настройками пользователя.

**3. Проверка и резервирование средств:**
Система отправляет запрос на проверку и резервирование средств у платежного провайдера (например, банка или платежной системы).
Платежный провайдер проверяет наличие средств на счету пользователя и резервирует их для проведения транзакции.

**4. Пополнение баланса:**
Система обновляет баланс счёта телефона пользователя, добавляя указанную в автоплатеже сумму.
Транзакция записывается в базу данных для ведения учёта и отслеживания.

**5. Подтверждение и уведомление:**
Система отправляет пользователю подтверждение о успешном пополнении баланса (например, через SMS, email или пуш-уведомление).
Платежный провайдер снимает зарезервированные средства с счёта пользователя.

**6. Обновление настроек автоплатежа:**
Система проверяет, не требуется ли обновление данных автоплатежа (например, если срок действия карты истекает).
При необходимости, система уведомляет пользователя о необходимости обновить данные.

**Заключение:**
Процесс пополнения баланса счёта телефона, будь то вручную или через автоплатёж, включает в себя проверку пользователя, выбор и проверку метода оплаты, резервирование и списание средств, обновление баланса и уведомление пользователя. Автоплатёж дополнительно требует настройки и регулярного триггера для автоматического инициирования платежей.

---

## Задание 3. SQL vs NoSQL
### 3.1. Напишите пять преимуществ SQL-систем по отношению к NoSQL.

### 3.1.* Какие, на ваш взгляд, преимущества у NewSQL систем перед SQL и NoSQL.

Приведите ответ в свободной форме.

### Ответ:

### 3.1 Пять преимуществ SQL-систем по отношению к NoSQL

**Целостность данных:**
SQL-системы обеспечивают строгую целостность данных благодаря поддержке ACID-транзакций (атомарность, согласованность, изоляция, долговечность). Это важно для критически важных приложений, где ошибки или несоответствия данных недопустимы.

**Строгая схема:**
SQL-системы используют заранее определённые схемы для структуры данных. Это позволяет обеспечить консистентность и предсказуемость данных, что упрощает их управление и анализ.

**Мощные возможности запросов:**
Язык SQL предоставляет мощные и гибкие средства для написания сложных запросов, включая соединения, агрегаты и подзапросы. Это позволяет выполнять сложные аналитические и отчетные операции.

**Широкая поддержка и экосистема:**
SQL-системы существуют уже несколько десятилетий и имеют широкую поддержку со стороны сообществ разработчиков, обширную документацию и множество инструментов для управления, мониторинга и анализа данных.

**Поддержка стандартов:**
SQL является стандартным языком для работы с реляционными базами данных. Это обеспечивает совместимость между различными системами и упрощает миграцию данных и приложений между ними.

### 3.1.* Преимущества NewSQL систем перед SQL и NoSQL

NewSQL системы сочетают в себе лучшие качества как традиционных SQL-систем, так и NoSQL-систем, предлагая следующие преимущества:

**Масштабируемость:**
NewSQL системы обеспечивают горизонтальную масштабируемость, подобно NoSQL системам, что позволяет обрабатывать большие объёмы данных и выдерживать высокие нагрузки.

**Поддержка ACID-транзакций:**
В отличие от многих NoSQL систем, NewSQL системы поддерживают ACID-транзакции, обеспечивая высокую целостность и согласованность данных, как в традиционных реляционных базах данных.

**Высокая производительность:**
NewSQL системы разработаны с учётом современных требований к производительности и могут предложить более высокую скорость обработки запросов и транзакций по сравнению с традиционными SQL-системами.

**Гибкость схемы:**
Некоторые NewSQL системы предлагают гибкость схемы, позволяя динамически изменять структуру данных, что является преимуществом по сравнению с традиционными реляционными СУБД.

**Совместимость с SQL:**
NewSQL системы поддерживают язык SQL, что упрощает переход на них для разработчиков, знакомых с традиционными реляционными базами данных. Это позволяет использовать существующие навыки и инструменты для работы с данными.

**Заключение:**
SQL-системы продолжают оставаться важными инструментами для работы с данными благодаря своей целостности, предсказуемости и мощным возможностям запросов. В то же время, NewSQL системы предлагают современные решения, сочетающие масштабируемость и гибкость NoSQL систем с традиционными преимуществами реляционных баз данных, что делает их привлекательными для современных высоконагруженных и критически важных приложений.

---

## Задание 4. Кластеры
Необходимо производить большое количество вычислений при работе с огромным количеством данных, под эту задачу выделено 1000 машин.

На основе какого критерия будете выбирать тип СУБД и какая модель распределённых вычислений здесь справится лучше всего и почему?

Приведите ответ в свободной форме.

### Ответ:

Для задачи с большими данными и множеством вычислений на 1000 машинах важно выбрать правильную базу данных и способ распределённых вычислений.

Критерии выбора базы данных:

**Масштабируемость:**
База данных должна легко увеличиваться, чтобы использовать все 1000 машин.

**Производительность:**
База данных должна быстро обрабатывать запросы и выполнять вычисления.

**Распределённое хранение:**
Данные должны храниться и обрабатываться на нескольких машинах одновременно.

**Устойчивость к отказам:**
База данных должна продолжать работать, даже если какие-то машины выйдут из строя.

**Поддержка сложных вычислений:**
База данных должна поддерживать сложные вычислительные задачи.

**Рекомендуемый тип базы данных:**
NewSQL (например, Google Spanner, CockroachDB) или распределённые NoSQL (например, Apache Cassandra, MongoDB) базы данных подойдут, потому что они хорошо масштабируются и производительны.

**Модель распределённых вычислений:**

Apache Hadoop: Хорош для обработки больших данных с помощью MapReduce.

Apache Spark: Быстрее и гибче, работает в памяти, что ускоряет обработку данных.

Google BigQuery: Быстрая платформа для анализа больших данных.

Dask: Инструмент для параллельных вычислений на Python.

**Заключение:**
Можно использовать Apache Spark вместе с NewSQL (Google Spanner или CockroachDB) или распределённой NoSQL (Apache Cassandra) базой данных. Spark обеспечит высокую производительность, а NewSQL или NoSQL базы данных помогут эффективно хранить и обрабатывать данные. Это обеспечит быстрые и надёжные распределённые вычисления.
