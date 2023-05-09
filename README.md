# Apache Druid

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



## Возможно ли распределение файлов БД по разным носителям?
## На каком языке/ах программирования написана СУБД?
## Какие типы индексов поддерживаются в БД? Приведите пример создания индексов.
## Как строится процесс выполнения запросов в вашей СУБД?
## Есть ли для вашей СУБД понятие «план запросов»? Если да, объясните, как работает данный этап.
## Поддерживаются ли транзакции в вашей СУБД? Если да, то расскажите о нем. Если нет, то существует ли альтернатива?
## Какие методы восстановления поддерживаются в вашей СУБД. Расскажите о них.
## Расскажите про шардинг в вашей конкретной СУБД. Какие типы используются? Принцип работы.
## Возможно ли применить термины Data Mining, Data Warehousing и OLAP в вашей СУБД?
## Какие методы защиты поддерживаются вашей СУБД? Шифрование трафика, модели авторизации и т.п.
## Какие сообщества развивают данную СУБД? Кто в проекте имеет права на коммит и создание дистрибутива версий? Расскажите об этих людей и/или компаниях.
## Создайте свои собственные данные для демонстрации работы СУБД. 
## Как продолжить самостоятельное изучение языка запросов с помощью демобазы. Если демобазы нет, то создайте ее.
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
