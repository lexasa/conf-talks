# Разница в подходах `graphql-compose` и `Prisma`

**[Prisma](https://www.prisma.io/)** - вы описываете схему, и вам генерируется бэкенд и GraphQL API. Вам практически не нужен админ.
**[Graphql-compose](https://graphql-compose.github.io/)** - вы сами настраиваете базы данных и пишете свой бэкенд, а потом уже из своих моделей генерируете GraphQL API.

C `Prisma` можно очень быстро получить рабочий GraphQL сервер, хоть в виде SaaS, так и в виде Docker контейнеров для собственной оркестрации. Но вот при дальнейшем рефакторинге, миграции данных или допилке какого-то серверного функционала вы можете столкнуться с проблемами. `Prisma` это полноценный фреймворк с большим комьюнити и как минимум 10-тью постоянными разработчиками по состоянию на июнь 2018, а также инвестициями в размере $5 млн на развитие их SaaS сервиса.

В свою очередь `graphql-compose` это просто toolkit, который позволяет вам удобнее объявлять GraphQL схему. На базе этого тулкита, вам будет напорядок легче написать свою GraphQL-схему, нежели используя стандартный [graphql-js](https://github.com/graphql/graphql-js) синтаксис. На базе `graphql-compose` написан ряд плагинов/генераторов, к примеру [graphql-compose-mongoose](https://github.com/graphql-compose/graphql-compose-mongoose) который генерирует кучу GraphQL типов и resolver'ов из mongoose моделей. Потом вы уже сами достраиваете свою схему, используя сгенерированные типы и методы, складывая их как кубики лего. Вы сами рулите своим сервером, моделями и развертыванием; ничего этого в `graphql-compose` нет. По состоянию на сентябрь 2018 всего 1 разработчик и 3-4 контрибьютера. Комьюнити очень слабое. Никакой финансовой поддержки и пиара в интернетах.

`Prisma` подошла к принципу [Api First](https://medium.com/adobetech/three-principles-of-api-first-design-fa6666d9f694) буквально, т.е. подменяет собой не только принцип взаимодействия клиента с сервером только через API. Но и полностью решает за вас то, как будет построен ваш сервер. Если вы строите что-то большое и сложное, и в будущем оно будет постоянно меняться и разрастаться, то я бы не рекомендовал вам использовать Prisma. Но если вам надо очень быстро получить рабочий сервер, и дальнейшие проблемы решать только по мере их поступления - то Prisma идеальный выбор для стартаперов. В конце концов, сперва надо быстро заработать денег, а потом можно нанять команду, которая все перепишет.

## Где `Prisma` просто порвет рынок через пару лет?

Все знаете что такое Wordpress? А слышали что-нибудь про [GraphQL CMS](https://graphcms.com/)? Так вот доля сайтов в интернетах написанных на Wordpress по некоторым оценкам составляет 30%. И обычно это небольшие сайты с кучей плагинов под свои задачи. Так вот с подходом Prisma такие плагины станет писать "как два байта переслать". А ровно на кучу небольших клиентов и заточен весь SaaS сервис призмы и их инвестиции.

## В сухом остатке

Коротко подходы таковы:

- `Prisma` описываете схему API -> генерируется бэкенд
- `graphql-compose` описываете бэкенд -> генерируете API

Я считаю что бэкенд может быть настолько большим и сложным, что его API это просто вершина айсберга. И вот по этой "вершине айсберга" оптимально сгенерировать весь бекенд под все задачи вашего продукта просто нереально.

> PS. Пожелаем призме, откушать побольше рынок у Wordpress. Ну а мне, со своим graphql-compose когда-нибудь выйти на консалтинг и коммерческую поддержку, по построению GraphQL API для больших организаций.