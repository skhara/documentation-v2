---
title: О тарификации приложений
keywords:
summary:
sidebar: evomain
permalink: doc_app_tariffication.html
tags:
---

{% include important.html content="Цены, приведённые в разделе, являются ориентировочными. Каждый тариф модераторы Эвотора проверяют и согласуют отдельно." %}

## О тарификации приложений

Платная подписка на приложение является основным инструментом монетизации ваших приложений. Рассчитывайте стоимость подписки с учётом технической поддержки пользователей. Также учитывайте, что многие клиенты, например, муниципальные предприятия, не могут оплачивать подписку ежемесячно. Поэтому, мы рекомендуем включить в вашу тарифную линейку годовые подписки.

{% include note.html content="Скидка при оформлении годовых подписок не может превышать 10%." %}

Возможно также распространение приложения за разовую оплату, например, если приложение относится к категории *Драйверы*.

{% include tip.html content="Вы можете отдельно согласовать тарификацию своего приложения с Эвотором." %}

Ниже приводятся категории приложений и рекомендуемые способы их тарификации. Все возможные исключения необходимо согласовывать с Эвотором.

## Категории приложений

### 1С Интеграции и приложения, использующие токен в открытом виде
Приложения, использующие для авторизации единый токен доступа к функциям API (например, Товароучетный API 1C), имеют единую тарификацию. Это сделано, чтобы избежать подмены токена более дешевым. Тарифы данных приложений должны с указанными [здесь](https://market.evotor.ru/#/store/apps/86e792db-1253-45c0-97d4-20b4c2ef97a3).

Если вы хотите изменить тарификацию, необходимо обеспечить сохранность токена и поддержать авторизацию на стороне вашего сервиса.

### Учетные системы
Минимальная стоимость приложения категории учетных систем составляет 300 руб./месяц за кассу, с учётом соответствующих скидок.

Минимальная стоимость приложения, чей функционал ограничен редактированием товаров и получением информации о продажах, составляет 100 руб./месяц.

### Кассовые приложения
Минимальная стоимость приложения с функционалом необходимым для работы кассы составляет 50 руб/месяц.

### Платежные приложения и приложения финансовых сервисов
Платежные приложения и приложения финансовых сервисов как правило бесплатны для клиента и работают по модели разделения прибыли (*revenue sharing*).

### Приложения для использования кассы в качестве фискального принтера и другого функционала с ограничением дальнейшего использования по основному назначению
Минимальная стоимость приложения этой категории, а также приложения, значительно изменяющих функционал смарт-терминала, составляет 800 руб./месяц. Это вызвано тем, что изменение функций смарт-терминала снижает или блокирует монетизацию за счёт установки других приложений.

### Определенные типы API и доступ к данным
Определенные типы API как и доступ к данным в облаке Эвотор тарифицируются отдельно или требуют минимальной цены приложения. Все подобные изменения мы указываем в рамках этого раздела.

### Драйверы устройств
Минимальная стоимость для драйверов устройств, необходимых для торговли (весы, принтеры этикеток, экраны покупателей, принтеры чеков),  составляет 1000 рублей.

При этом, для цену платной подписки можно устанавливать ниже.

Стоимость драйверов устройств, распространяющихся с приложениями, может входить в стоимость подписки на приложение.

{% include note.html content="Если ваше приложение не относится к приведённым категории, его минимальная цена будет начинаться от 30 руб./месяц. Также вы можете отдельно согласовать тарификацию своего приложения с Эвотором." %}

### Заказная разработка {#CustomDevelopment}
Вы можете использовать REST API Облака Эвотор для разработки заказных решений для третьих лиц. При заказной разработке вы можете предложить компании заказчику оплатить только разработку, а само приложение обозначить как бесплатное. В этом случае вам необходимо учитывать, что любое использование нашего API платное и Эвотор будет ежемесячно взимать с вас оплату независимо от ваших договорённостей с заказчиком.

{% include important.html content="Каждый подобный случай необходимо согласовывать с Эвотором." %}

## Временные акции и возможности для продвижения
Для продвижения приложения вы можете продлевать или расширять функционал пробного периода. Продолжительность пробного периода использования приложения должна быть единой и независимой от тарифа, который выбрал пользователь.

Другие инструменты для продвижения, например, бесплатные версии, требуется согласовывать с Эвотором отдельно.

{% include warning.html content="Запрещено использовать демпинг и временное значительное снижение цены (не в рамках согласованных акций)." %}