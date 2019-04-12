---
title: Взаимодействие со смарт-терминалом
keywords:
sidebar: evojava
permalink: draft_doc_app_integration_points.html
product: Java SDK
---

## О способах взаимодействия

Существует три способа взаимодействия со смарт-терминалом:

* События -- .
* Команды --
* Широковещательные сообщения --

## События {#events}

С помощью событий смарт-терминал сообщает установленным интеграционным приложениям о различных действиях пользователя: изменении позиций в чеке, разделении платежей, начислении скидок на чек и других.

После оповещения приложений, смарт-терминал ожидает результата обработки события.

Схема ниже показывает процесс распространения события в смарт-терминале.

{% include image.html file="EventSequenceDiagram.png" url="images/EventSequenceDiagram.png" caption="Жизненный цикл события, которое распространяет смарт-терминал." %}

{% include note.html content="Первое приложение, которое получает событие, смарт-терминал выбирает случайным образом." %}
{% include important.html content="Возможно нежелательное [зацикливание обработки одного события различными интеграционными приложениями](./draft_doc_app_integration_points.html#eventlooping)." %}

Для получения события, в элементе `<action>` intent-фильтра соответствующей [интеграционной службы](./TODO РАЗДЕЛ ПРО ИНТЕГРАЦИОННЫЕ КОМПОНЕНТЫ) вашего приложения требуется указать значение выбранной константы события.

Например, служба, которая обрабатывает событие начисления скидки на чек продажи, в манифесте приложения будет выглядеть так:

```xml
<service
  android:name=".MyDiscountService"
  android:enabled="true"
  android:exported="true">
  <intent-filter>
    <action android:name="evo.v2.receipt.sell.receiptDiscount"/>
  </intent-filter>
</service>
```

Для обработки событий требуется использовать соответствующие процессоры. Подробнее об использовании процессоров читайте в соответствующих руководствах.

Смарт-терминал распространяет следующие события:

* Намерение изменить позицию чека: [`BeforePositionsEditedEvent`](./). О том как обрабатывать событие, [читайте в разделе ""](./).
* Разделение платежей в чеке продажи: [`PaymentSelectedEvent`](./). О том как обрабатывать событие, [читайте в разделе ""](./).
* Начисление скидки на чек: [`ReceiptDiscountEvent`](./). О том как обрабатывать событие, [читайте в разделе ""](./).
* Разделение чека на печатные группы: [`PrintGroupRequiredEvent`](./). О том как обрабатывать событие, [читайте в разделе ""](./).
* Объединение позиций чека: [`PositionsMergeEvent`](./). О том как обрабатывать событие, [читайте в разделе ""](./).
* Передача оплаты чека продажи другому приложению (например, при выборе приложения "Комбооплата"): [`PaymentDelegatorEvent`](./). О том как обрабатывать событие, [читайте в разделе ""](./).
* Печать в чеке произвольных данных: [`PrintExtraRequiredEvent`](./). О том как обрабатывать событие, [читайте в разделе ""](./).
* Оплата различных чеков сторонними платёжными системами (в intent-фильтре указывайте значение константы родительского события [`PaymentSystemEvent`](./)):

   * Оплата чека продажи: [`PaymentSystemSellEvent`](./).
   * Отмена оплаты чека продажи: [`PaymentSystemSellCancelEvent`](./).
   * Оплата чека возврата: [`PaymentSystemPaybackEvent`](./).
   * Отмена оплаты чека возврата: [`PaymentSystemPaybackCancelEvent`](./).

   О том как обрабатывать события, [читайте в разделе ""](./).

### Зацикливание обработки события {#eventlooping}

Возможна ситуация, при которой событие будет обработано одним приложением, затем другим, а после опять попадёт на обработку первому приложению. Такого зацикливания следует избегать.

Для этого необходимо...**TODO**

## Команды {#commands}

Ваше приложение может отдавать смарт-терминалу команды, например, открыть чек или напечатать Z-отчёт. После обработки команды устройство возвращает соответствующий результат.

Для использования некоторых команд, в манифесте приложения, в элементе `<uses-permission />` необходимо указать соответствующее [разрешение](./ссылка на раздел о разрешениях в топике про манифест приложения).

Команды вызываются в коде операции или службы(**ТАК ЛИ ЭТО?**), например, следующим образом:

```java
//Команда открытия чека продажи и вызов метода process.
new OpenSellReceiptCommand(positionAddList, extra).process(context, callback);
```

Ваше приложение может отдавать смарт-терминалу следующие команды:

* Открыть чек:

   * Продажи: [`OpenSellReceiptCommand`](./)
   * Возврата: [`OpenPaybackReceiptCommand`](./)
   * Покупки: [`OpenBuyReceiptCommand`](./)
   * Возврата покупки: [`OpenBuybackReceiptCommand`](./)

* Напечатать чек:

   * Продажи: [`PrintSellReceiptCommand`](./)
   * Возврата: [`PrintPaybackReceiptCommand`](./)
   * Покупки: [`PrintBuyReceiptCommand`](./)
   * Возврата покупки: [`PrintBuybackReceiptCommand`](./)

   {% include note.html content="Команды печати чеков также используются для [отправки чеков по СМС и электронной почте](./)." %}

* Снять и напечатать Z-отчёт: [`PrintZReportCommand`](./). Подробнее о снятии и печати Z-отчёта [читайте в разделе "Печать Z-отчёта."](./)

## Широковещательные сообщения {#broadcasts}

Смарт-терминал автоматически рассылает *широковещательные сообщения* при возникновении различных событий: открытии чека продажи, сканировании штрихкода, открытии карточки товара и др.

Чтобы ваше приложение реагировало на такие события, подпишите его на получение соответствующих широковещательных сообщений. Для этого используйте *приёмники широковещательных сообщений* (`BroadcastReceiver`).

В `integration-library` все широковещательные сообщения поделены на группы. Для каждой из групп есть свой приёмник, который содержит методы обработки соответствующих сообщений. Всего таких приёмников восемь:

* [**SellReceiptBroadcastReceiver**](./integration-library/ru/evotor/framework/core/action/broadcast/SellReceiptBroadcastReceiver.html) – приёмник событий, связанных с чеком продажи.
* [**PaybackReceiptBroadcastReceiver**](./integration-library/ru/evotor/framework/core/action/broadcast/PaybackReceiptBroadcastReceiver.html) – приёмник событий, связанных с чеком возврата.
* [**BuyReceiptBroadcastReceiver**](./integration-library/ru/evotor/framework/core/action/broadcast/BuyReceiptBroadcastReceiver.html) – приёмник событий, связанных с чеком покупки.
* [**BuybackReceiptBroadcastReceiver**](./integration-library/ru/evotor/framework/core/action/broadcast/BuybackReceiptBroadcastReceiver.html) – приёмник событий, связанных с чеком возврата покупки.
* [**InventoryBroadcastReceiver**](./integration-library/ru/evotor/framework/core/action/broadcast/InventoryBroadcastReceiver.html) – приёмник событий, связанных с товароучётом.
* [**CashDrawerBroadcastReceiver**](./integration-library/ru/evotor/framework/core/action/broadcast/CashDrawerBroadcastReceiver.html) – приёмник событий, связанных с денежным ящиком.
* [**KktBroadcastReceiver**](./integration-library/ru/evotor/framework/kkt/event/handler/receiver/KktBroadcastReceiver.html) – приёмник событий, связанных с денежными операциями.
* [**ScannerBroadcastReceiver**](./integration-library/ru/evotor/framework/core/action/broadcast/ScannerBroadcastReceiver.html) – приёмник событий, связанных со сканером штрихкодов.

  Подробнее о работе со сканером штрихкодов читайте [здесь](./doc_java_barcode_scanner.html).

## Подписка приложения на сообщения

*Чтобы подписать приложение на получение сообщений:*

1. Создайте приёмник, унаследованный от соответствующего класса.

   Приёмник должен переопределять методы класса.

2. В манифесте приложения, в intent-фильтре приёмника, укажите какие события требуется получать.

## Пример

Приёмник `MyReceiver`, обрабатывающий сообщения об открытии и закрытии чека покупки:

```java
public class MyReceiver extends BuyReceiptBroadcastReceiver {

    @Override
    void  handleReceiptOpenedEvent(Context context, ReceiptOpenedEvent receiptOpenedEvent) {
      //Тело метода.
    };

    @Override
    void  handleReceiptClosedEvent(Context context, ReceiptClosedEvent receiptClosedEvent) {
      //Тело метода.
    };
};
```

Приёмник `MyReceiver` в манифесте приложения:

```xml
<receiver
    android:name=".MyReceiver"
    android:enabled="true"
    android:exported="true">
    <intent-filter>
        <action android:name="evotor.intent.action.receipt.buy.OPENED" />
        <action android:name="evotor.intent.action.receipt.buy.CLOSED" />
    </intent-filter>
</receiver>
```