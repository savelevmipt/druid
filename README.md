# Apache Druid
Druid is a high performance, real-time analytics database that delivers sub-second queries on streaming and batch data at scale and under load.

Apache Druid is used to power real-time analytics applications that require fast queries at scale and under load on streaming and batch data. Druid features a unique distributed architecture across its ingestion, storage, and query layer to handle the scale needed for large aggregations with the performance needed for applications.

![image](https://github.com/savelevmipt/druid/assets/100207961/f68914f9-ff06-4943-a38f-cc75e7eb624b)

Druid is a services-based architecture that consists of independently scalable services for ingestion, querying, and orchestration, each of which can be fine-tuned to optimize cluster resources for mixed use cases and workloads. For example, more resources can be directed to Druid’s query service while providing less resources to ingestion as workloads change. Druid services can fail without impact on the operations of other services.

A Druid deployment is a scalable cluster of commodity hardware with node types that serve specific functions. In a small configuration, all of these nodes can run together on a single server (or even a laptop). For larger deployments, one or more servers are dedicated to each node type and can scale to thousands of nodes for higher throughput requirements.


## История развития СУБД

Разработка начата в 2011 году (авторы - Эрик Четтер / Eric Tschetter, Фанжин Йенг/Fangjin Yang, Джан Мерлино/Gian Merlino и Вадим Огиветский/Vadim Ogievetsky) для решения аналитических задач в компании Metamarkets.

Исходный код открыт под лицензией GPL license в октябре 2012 и переведен на лицензию Apache License в феврале 2015.

## Инструменты для взаимодействия с СУБД

C druid можно взаимодействовать через web console на http://localhost:8888.
<img width="1280" alt="image" src="https://user-images.githubusercontent.com/100207961/237010418-37547833-303b-43d0-8303-41ff38f0bdd0.png">

## Какой database engine используется в вашей СУБД?

Druid использует собственный database engine, который называется Apache Druid. Он был разработан для обработки и анализа больших объемов данных в реальном времени и предоставляет мощные возможности для агрегации, фильтрации и группировки данных. Druid поддерживает различные источники данных, включая потоковые данные, данные из баз данных и файловых систем, а также интегрируется с различными инструментами анализа данных.

## Как устроен язык запросов в вашей СУБД? Разверните БД с данными и выполните ряд запросов. 

Apache Druid supports two query languages: Druid SQL and native queries.
Druid translates SQL queries into its native query language. 
Native queries in Druid are JSON objects and are typically issued to the Broker or Router processes.

Загрузим данные из файла
<img width="975" alt="image" src="https://user-images.githubusercontent.com/100207961/237014053-984ce1e1-37c4-4c31-bdd8-310050439247.png">

Язык запросов SQL достаточно привычен 
<img width="1280" alt="image" src="https://user-images.githubusercontent.com/100207961/237027153-75d2385c-725d-47d5-bb37-03f82875c9e8.png">
<img width="1280" alt="image" src="https://user-images.githubusercontent.com/100207961/237027313-7fe5dbed-cf07-4b6e-b141-fc3501d65fd7.png">
<img width="1280" alt="image" src="https://user-images.githubusercontent.com/100207961/237029448-c6a2c271-acf1-4b06-9d44-76fde89f8e8e.png">

Интерфейс очень приятный и красивый.

<img width="1280" alt="image" src="https://user-images.githubusercontent.com/100207961/237030360-15fcfa01-41ad-4505-a872-c6f22025836c.png">



## Возможно ли распределение файлов БД по разным носителям?
You can use segment partitioning and sorting within your Druid datasources to reduce the size of your data and increase performance.

One way to partition is to load data into separate datasources. This is a perfectly viable approach that works very well when the number of datasources does not lead to excessive per-datasource overheads.

## На каком языке/ах программирования написана СУБД?

Druid написан на Java.

## Какие типы индексов поддерживаются в БД? Приведите пример создания индексов.

The Apache Druid indexing service is a highly-available, distributed service that runs indexing related tasks.

Indexing tasks create (and sometimes destroy) Druid segments. The indexing service has a master/slave like architecture.

The indexing service is composed of three main components: a Peon component that can run a single task, a Middle Manager component that manages Peons, and an Overlord component that manages task distribution to MiddleManagers. Overlords and MiddleManagers may run on the same process or across multiple processes while MiddleManagers and Peons always run on the same process.

Tasks are managed using API endpoints on the Overlord service. Please see Overlord Task API for more information.


Apache Druid supports the following types of native batch indexing tasks:

* Parallel task indexing (index_parallel) that can run multiple indexing tasks concurrently. Parallel task works well for production ingestion tasks.
* Simple task indexing (index) that run a single indexing task at a time. Simple task indexing is suitable for development and test environments.
This topic covers the configuration for index_parallel ingestion specs.



## Как строится процесс выполнения запросов в вашей СУБД?

![image](https://user-images.githubusercontent.com/100207961/237051254-7045bc40-8f78-4bae-a567-02779d1498a7.png)

В обработке запросов участвуют ноды трёх видов: broker, realtime и historical. Запрос приходит в broker, который знает, на каких нодах какие сегменты находятся. Он распределяет запрос по historical (и realtime) нодам, хранящим нужные сегменты. Historical ноды также распараллеливают вычисления насколько это возможно, отправляют результаты брокеру, а тот отдает их клиенту. Благодаря сочетанию этой схемы с колоночным хранением данных Druid может очень быстро обрабатывать большие объемы информации.


## Есть ли для вашей СУБД понятие «план запросов»? Если да, объясните, как работает данный этап.

Да, план запросов есть, его можно открыть и посмотреть 
<img width="1280" alt="image" src="https://user-images.githubusercontent.com/100207961/237032483-fc2662b6-5a60-4d57-b040-7d85df5b7873.png">

Add "EXPLAIN PLAN FOR" to the beginning of any query to get information about how it will be translated. In this case, the query will not actually be executed. Refer to the Query translation documentation for more information on the output of EXPLAIN PLAN.

<img width="655" alt="image" src="https://github.com/savelevmipt/druid/assets/100207961/b5ecc473-c027-44b9-83a8-0e9c20706af1">
<img width="649" alt="image" src="https://github.com/savelevmipt/druid/assets/100207961/5afd9afe-4705-456e-8dfa-be0c182f8dca">
<img width="656" alt="image" src="https://github.com/savelevmipt/druid/assets/100207961/9f4221f8-513c-493d-82d7-a1d1e185b933">


## Поддерживаются ли транзакции в вашей СУБД? Если да, то расскажите о нем. Если нет, то существует ли альтернатива?

On the ingestion side, Druid's primary ingestion methods are all pull-based and offer transactional guarantees. This means that you are guaranteed that ingestion using these methods will publish in an all-or-nothing manner:

* Supervised "seekable-stream" ingestion methods like Kafka and Kinesis. With these methods, Druid commits stream offsets to its metadata store alongside segment metadata, in the same transaction. Note that ingestion of data that has not yet been published can be rolled back if ingestion tasks fail. In this case, partially-ingested data is discarded, and Druid will resume ingestion from the last committed set of stream offsets. This ensures exactly-once publishing behavior.
* Hadoop-based batch ingestion. Each task publishes all segment metadata in a single transaction.
* Native batch ingestion. In parallel mode, the supervisor task publishes all segment metadata in a single transaction after the subtasks are finished. In simple (single-task) mode, the single task publishes all segment metadata in a single transaction after it is complete.

## Какие методы восстановления поддерживаются в вашей СУБД. Расскажите о них.

Репликация данных: Все данные в Druid копируются настраиваемое количество раз, поэтому сбой одного сервера не влияет на запрос.

Автоматическое резервное копирование данных: Druid автоматически выполняет резервное копирование всех данных индекса в файловую систему, такую ​​как HDFS. Вы можете потерять весь кластер Druid и быстро восстановить данные из этой резервной копии.


## Расскажите про шардинг в вашей конкретной СУБД. Какие типы используются? Принцип работы.

![image](https://user-images.githubusercontent.com/100207961/237036284-235ceec2-4a50-498d-ba91-2cf121ca52b7.png)

Druid is a services-based architecture that consists of independently scalable services for ingestion, querying, and orchestration, each of which can be fine-tuned to optimize cluster resources for mixed use cases and workloads. For example, more resources can be directed to Druid’s query service while providing less resources to ingestion as workloads change. Druid services can fail without impact on the operations of other services.

A Druid deployment is a scalable cluster of commodity hardware with node types that serve specific functions. In a small configuration, all of these nodes can run together on a single server (or even a laptop). For larger deployments, one or more servers are dedicated to each node type and can scale to thousands of nodes for higher throughput requirements.

Master Nodes govern data availability and ingestion

Query Nodes accept queries, manage execution across the system, and return the results

Data Nodes execute ingestion workloads and queries as well as store queryable data

In addition, Druid utilizes a deep storage layer - cloud object storage or HDFS - that contains an additional copy of each data segment. It enables background data movement between Druid processes and also provides a highly durable data source to recover from system failures.


## Возможно ли применить термины Data Mining, Data Warehousing и OLAP в вашей СУБД?

Druid is primarily used for business intelligence (OLAP) queries on event data.

Sub-second OLAP Queries Druid’s unique architecture enables rapid multi-dimensional filtering, ad-hoc attribute groupings, and extremely fast aggregations.

Druid is a good fit if you have the following requirements:

1. You are building an application that requires fast aggregations and OLAP queries
1. You want to do real-time analysis
1. You have lots of data (trillions of events, petabytes of data)
1. You need a data store that is always available with no single point of failure

### Is Druid a data warehouse?

Apache Druid is a new type of database to power real-time analytic workloads for event-driven data, and isn’t a traditional data warehouse. Although Druid incorporates architecture ideas from data warehouses such as column-oriented storage, Druid also incorporates designs from search systems and timeseries databases. Druid's architecture is designed to handle many use cases that traditional data warehouses cannot.

Druid offers the following advantages over traditional data warehouses:

* Much lower latency for OLAP-style queries
* Much lower latency for data ingest (both streaming and batch)
* Out-of-the-box integration with Apache Kafka, AWS Kinesis, HDFS, AWS S3, and more
* Time-based partitioning, which enables performant time-based queries
* Fast search and filter, for fast slice and dice
* Minimal schema design and native support for semi-structured and nested data



## Какие методы защиты поддерживаются вашей СУБД? Шифрование трафика, модели авторизации и т.п.

<img width="708" alt="image" src="https://user-images.githubusercontent.com/100207961/237055592-4f3b9df8-b0c6-4413-9d97-3b780363022e.png">


### Authentication and authorization
You can configure authentication and authorization to control access to the Druid APIs. Then configure users, roles, and permissions, as described in the following sections. Make the configuration changes in the common.runtime.properties file on all Druid servers in the cluster.

Within Druid's operating context, authenticators control the way user identities are verified. Authorizers employ user roles to relate authenticated users to the datasources they are permitted to access. You can set the finest-grained permissions on a per-datasource basis.

The following graphic depicts the course of request through the authentication process:

![image](https://user-images.githubusercontent.com/100207961/237055230-2d9e1ff8-331c-4848-a28b-b4e42695977f.png)


## Какие сообщества развивают данную СУБД? Кто в проекте имеет права на коммит и создание дистрибутива версий? Расскажите об этих людей и/или компаниях.

Druid is a community-led project and we are delighted to receive contributions of anything from minor fixes to big new features.

<img width="719" alt="image" src="https://user-images.githubusercontent.com/100207961/237056250-cf0216ae-a589-4380-9070-b4e582da055c.png">

Основной вклад вносит компания Imply. Также много участников из компании Alibaba

Imply is a company of developers, innovators, problem solvers, and mavericks, passionate about helping developers drive the next generation of analytics innovation. We are backed by Thoma Bravo, Andreessen Horowitz (a16z), Bessemer Venture Partners, Tiger Global Management, Khosla Ventures, and Geodesic Capital.

We are proud that developers at companies of all sizes – from startups to Fortune 100 enterprises – choose Imply to build real-time analytics applications.

Alibaba - китайская публичная компания, работающая в сфере интернет-коммерции, владелец веб-порталов Taobao.com, Tmall, Alibaba.com, AliExpress и ряда других.

## Создайте свои собственные данные для демонстрации работы СУБД. 
Загрузим данные через терминал
<img width="1099" alt="image" src="https://github.com/savelevmipt/druid/assets/100207961/d8d708de-af8d-4704-b44e-b59dd359b4c9">
<img width="882" alt="image" src="https://github.com/savelevmipt/druid/assets/100207961/3caa90dc-d387-46a5-8a26-20a37f75ca6e">

## Как продолжить самостоятельное изучение языка запросов с помощью демобазы. Если демобазы нет, то создайте ее.
Демобаза есть, она включена в стандартный пакет. <img width="655" alt="image" src="https://github.com/savelevmipt/druid/assets/100207961/d61159c9-2833-475a-badc-0efc16db4512">
Выше была произведена работа с демобазой
## Где найти документацию и пройти обучение

Документация доступна на официальном сайте druid https://druid.apache.org/docs/latest/design/

Найти большое количество видеоуроков по druid можно на канале https://www.youtube.com/@Implydata/videos

## Как быть в курсе происходящего

Most discussion about Druid happens over Slack, GitHub, and the Apache Dev list, but those aren't the only way to interact with the Druid community. We also do chat, meetups, and more.

Check out the following resources if you're looking for help, to discuss Druid development, or just stay up to date:

Slack: Many users and committers are present on Apache Druid Slack. Use this link to join and invite others: https://druid.apache.org/community/join-slack. This is the perfect place to ask for help if you need it!
GitHub: Star us at apache/druid and use this to follow Druid development, raise issues, or contribute pull requests. If you're interested in development, please see the Contributing section below for details on our development process.
Development mailing list: dev@druid.apache.org for discussion about project development.
Twitter: Follow us on Twitter at @druidio.
