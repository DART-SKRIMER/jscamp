<<<<<<< refs/remotes/origin/master
---
id: notif-00
title: Push Notifications with AWS Amplify
sidebar_label: Push notifications
---


Push notifications play an important role in any application. This can dramatically increase user engagement.

![Push Notifications](/img/notification/00.png)

Setting up push notifications from scratch can be a little tricky. Fortunately, Amplify provides push notification services and SDKs for our apps. In this tutorial, we will learn how to integrate this service into our application.

![Step01](/img/steps/01.png)

## Create a new project ⚛️

```bash
npx react-native init amplifyPush
```

```bash
cd amplifyPush
```

In the root directory of the React Native project, initialize AWS Amplify

```bash
amplify init
```

We answer questions:

![Initialize Amplify](/img/notification/notif_amplify_init.png)

The project was initialized 🚀

## We add dependencies:

```bash
yarn add aws-amplify @aws-amplify/pushnotification
```

```bash
npm install --save aws-amplify @aws-amplify/pushnotification
```

We link the push notification dependency using the command:

```bash
react-native link @aws-amplify/pushnotification
```

:::caution To prevent this [error](https://github.com/aws-amplify/amplify-js/issues/5010) in the future, add the `netinfo` library. You can add it to your project with the following command (if you don't have one):

```bash
yarn add @react-native-community/netinfo
```

```bash
npm install --save @react-native-community/netinfo
```

:::

![Step02](/img/steps/02.png)

## Android - Setting up Firebase

1. Open [Firebase Console](https://console.firebase.google.com/).
2. Open or create a new project for further actions.
3. Select `Cloud Messaging` from the toolbar.

![Cloud Messaging](/img/notification/notif_cloud_messaging.png)

4.  Click on Android and follow these steps:

- Fill out the form and register the application. The `android package name` can be found in` android / app / build.gradle`. Stored in `applicationId` look like this:

```java
   gradle title="android/app/build.gradle"
      defaultConfig {
       applicationId "com.amplifypush"
      }
```

- Upload the config file to `android / app`.
- Add Firebase SDK. Consider `<project>` `android` and `<app-module>` `app`

  directory to react native project. Don't forget to add the latest version of `firebase-messaging` [from here](https://firebase.google.com/docs/android/setup#available-libraries) and `firebase-analytics` in `dependencies`

- Run the project in Android and you will see confirmation from Firebase. (you can skip this step). 5. Open `android / app / src / main / AndroidManifest.xml` and add the following code to `application`:

```xml
<!--[START Push notification config -->
        <!-- [START firebase_service] -->
        <service
            android:name="com.amazonaws.amplify.pushnotification.RNPushNotificationMessagingService">
            <intent-filter>
                <action android:name="com.google.firebase.MESSAGING_EVENT"/>
            </intent-filter>
        </service>
        <!-- [END firebase_service] -->
        <!-- [START firebase_iid_service] -->
        <service
            android:name="com.amazonaws.amplify.pushnotification.RNPushNotificationDeviceIDService">
            <intent-filter>
                <action android:name="com.google.firebase.INSTANCE_ID_EVENT"/>
            </intent-filter>
        </service>
        <receiver
            android:name="com.amazonaws.amplify.pushnotification.modules.RNPushNotificationBroadcastReceiver"
            android:exported="false" >
            <intent-filter>
                <action android:name="com.amazonaws.amplify.pushnotification.NOTIFICATION_OPENED"/>
            </intent-filter>
        </receiver>
    <!-- [END Push notification config -->
```

![Step03](/img/steps/03.png)

## Настройка Amplify для FCM

1. Add a push notification service using the following command in your project directory:

```bash
 amplify add notifications
```

2. Please select `FCM`:

```bash
 ? Choose the push notification channel to enable.
 APNS
 ❯ FCM
 Email
 SMS
```

3. Enter the exact name of the resource (or just hit enter without filling anything).
4. You will be asked for `ApiKey`. To do this, you need to follow these steps:

- Open [Firebase Console ](https://console.firebase.google.com/) and open the app you created in the previous steps.
- Click on the icon in the `Project Overview` section in the toolbar and select `Project settings`. ![Настройки проекта](/img/notification/notif_project_settings.png)
-Select the `Cloud Messaging` tab and copy the value `Server key`. ![Project settings](/img/notification/notif_api_key.png)

5. Insert the requested values for `ApiKey`.
6. After completing the configuration, run `amplify push`.

![Step04](/img/steps/04.png)

## iOS - Setting up

1. Install `@react-native-community/push-notification-ios`:

```bash
yarn add @react-native-community/push-notification-ios
```

```bash
npm install --save @react-native-community/push-notification-ios
```

2. Run the following command to iOS:

   ```bash
   cd ios && pod install && cd ..
   ```

3. Add iOS notifications with the command `amplify add notifications` :

   1. Choose `APNS`:

   ```bash
   ? Choose the push notification channel to enable.
      > APNS
      FCM
      Email
      SMS
   ```

   2. You will then be prompted for an authentication method. It is recommended to select a certificate.

   ```bash
   ? Choose authentication method used for APNs (Use arrow keys)
   > Certificate
   Key
   ```

   3. If you selected a certificate, you will be prompted for the path to the .p12 certificate. (You can use this [tutorial](https://mobincube.zendesk.com/hc/en-us/articles/200511933-How-to-get-the-p12-file-and-provisioning-profile-for-publishing-an-app-on-App-Store)).
   4. Run `amplify push`.

   5. Discover `.xcworkspace` with XCode.

    6. Select a project and select a project name in the `TARGETS` section. Select `Signing & Capabilities` and press the` + `in front of the` Capability`. Select `Background Mode - Remote Notifications`.

![Step05](/img/steps/05.png)

## Application setup

As stated earlier, `Analytics` needs to be integrated with notifications. This will help track notifications. Although custom properties can be used, it is recommended that you use the `aws-exports` file.

In `App.js` add the following configuration:

```js
...
import Amplify from 'aws-amplify'
import PushNotification from '@aws-amplify/pushnotification'
import awsconfig from './aws-exports'

Amplify.configure(awsconfig)

PushNotification.configure(awsconfig)
...
```

![Step06](/img/steps/06.png)

## Working with API

We usually want to send push notifications to specific users for various purposes. The API provides us with various methods to handle our users and push notifications.

## onRegister

Each device can be recognized with a push token, with which you can specify the device for which you want to receive a push notification. When the user opens the application for the first time, the pushed token is retrieved and stored on the device. You should be aware that this method may be called again in the future, so you should be prepared for this situation to update your data accordingly.

You can add the following code to `App.js`:

```js
PushNotification.onRegister(token => {
  console.log('in app registration', token)
  PushNotification.updateEndpoint(token)
})
```

**attention**: On Android, there might be a problem that this method will never be called! However [workaround](https://github.com/aws-amplify/amplify-js/issues/2643#issuecomment-523610933) can be like this wherever you need a token:

```js
...
import {NativeModules} from 'react-native'
...
NativeModules.RNPushNotification.getToken((token) => {
  console.log(`PushToken: ${token}`)
})
...
```

## onNotification

If you want to do something when a notification is received, the `onNotification` method is for actions based on the received notification. Keep in mind that the structure of notification objects is different from Android and iOS. On iOS, you [should](https://reactnative.dev/docs/pushnotificationios.html#finish) use the `finish` method. You can add the following code to `App.js`:

```js
...
import PushNotificationIOS from '@react-native-community/push-notification-ios'
...
PushNotification.onNotification((notification) => {
  console.log('in app notification', notification)
  if (Platform.OS === 'ios') {
    notification.finish(PushNotificationIOS.FetchResult.NoData)
  }
})
```

## onNotificationOpened

A common scenario is when a user opens a push notification, `onNotificationOpened` is called. `App.js` looks like this:

```js
PushNotification.onNotificationOpened(notification => {
  console.log('the notification is opened', notification)
})
```

## requestIOSPermissions

Push notification only works on a real device and will not receive any notifications unless the end user gives permission. `requestIOSPermissions` is needed to get this permission. It can be called without any parameters, or you can customize the object like this:

```js
PushNotification.requestIOSPermissions()
// or
PushNotification.requestIOSPermissions({
  alert: true,
  badge: true,
  sound: false
})
```

![Step07](/img/steps/07.png)

## Testing

First of all, we want to take a look at the file `App.js`.

```js
import React from 'react'
import { SafeAreaView, Platform, Text, NativeModules } from 'react-native'

import PushNotificationIOS from '@react-native-community/push-notification-ios'
import Analytics from '@aws-amplify/analytics'
import Amplify from 'aws-amplify'
import PushNotification from '@aws-amplify/pushnotification'
import awsconfig from './aws-exports'

Amplify.configure(awsconfig)
PushNotification.configure(awsconfig)

PushNotification.onRegister(async token => {
  console.log('in app registration', token)
  PushNotification.updateEndpoint(token)
})

// In case PushNotification.onRegister didn't work
NativeModules.RNPushNotification.getToken(token => {
  console.log(`PushToken: ${token}`)
})

PushNotification.onNotification(notification => {
  console.log('in app notification', notification)
  if (Platform.OS === 'ios') {
    notification.finish(PushNotificationIOS.FetchResult.NoData)
  }
})

PushNotification.onNotificationOpened(notification => {
  console.log('the notification is opened', notification)
})

const endpointId = Analytics.getPluggable('AWSPinpoint')._config.endpointId
console.log(`endpoint ID: ${endpointId}`)

if (Platform.OS === 'ios') {
  PushNotification.requestIOSPermissions()
}

const App: () => React$Node = () => {
  return (
    <SafeAreaView>
      <Text>Push Notification</Text>
    </SafeAreaView>
  )
}

export default App
```

Launching the project:

```bash
react-native run-android
```

```bash
react-native run-ios
```

To go further, we need one of the `endpoint ID` or` Push Token`. Explained in detail [here](https://docs.aws.amazon.com/pinpoint/latest/apireference/apps-application-id-endpoints.html) `endpoint` in `aws` services:

> `Endpoint` represents a destination to which you can send messages, such as a mobile device, email address, or phone number.

`Push Token` it is a unique identifier that is generated and assigned from `GCM` (Android) or` APNS` (iOS) to your application on a specific device.

The most obvious difference between the two is that the `endpoint` is generated from` aws` and defines the application on the device regardless of platform (iOS / Android). But the token, depending on the platform, is generated either from `Apple` or` Google`.

We use `console.log` for copying and save these keys for the next steps. Switch to development mode and copy the following values to the console:

![Tokens](/img/notification/notif_console_tokens.png)

While there are several ways to send a test push notification to a specific device, we'll explore the easiest way.

1. Run the following command at the root of the project:

```bash
amplify notification console
```

2. The application console will automatically open in the browser.
3. Select `Test messaging` in the left sidebar:

![Test messaging](/img/notification/notif_aws_notif_console.png)

4. In the `Channel` section, select `Push notifications`.

5. The `Destinations` section looks like this: ![Destinations](/img/notification/notif_testing_message_dest.png)

6. `Destination type` determines whether you want to use `Endpoint IDs` or` Device Tokens` (or `Push token` in the previous steps) in the next text input.

7. Insert the token you want to use based on the `Destination type`.

8. If you selected `Endpoint IDs` and used an endpoint, the` Push Notification Service` can automatically detect your device. Otherwise, if you used `Device token`, select` APNS` for IOS and `FCM` for Android.

9. You can fill in the `Message` section as shown below and click the button `Send message`. ![Destinations](/img/notification/notif_testing_message_message.png)

10. You will receive a success message as shown below. ![Success](/img/notification/notif_testing_message_success.png) After a couple of seconds, you will see a push notification on your device: ![Push notification result](/img/notification/notif_android_push_result.png)

## Done ✅

## Links:

[Amplify Docs](https://docs.amplify.aws/lib/push-notifications/getting-started/q/platform/js)

[Setting up Android Push Notifications with AWS Amplify](https://medium.com/@dantasfiles/setting-up-android-push-notifications-with-aws-amplify-e6334c6356d8)

[Testing Push Notifications with AWS Amplify & CLI](https://medium.com/@dantasfiles/testing-push-notifications-with-aws-amplify-9126bd621d3a)

[![Become a Patron!](/img/logo/patreon.jpg)](https://www.patreon.com/bePatron?u=31769291)
=======
---
id: notif-00
title: Push-уведомления с помощью AWS Amplify
sidebar_label: Push-уведомления
---

Push-уведомления играют важную роль в любом приложении. Это может значительно увеличить взаимодействие с пользователями.

![Push Notifications](/img/notification/00.png)

Настройка push-уведомлений с нуля может быть немного сложной. К счастью, Amplify предоставляет услуги push-уведомлений и SDK для наших приложений. В этом уроке мы узнаем, как интегрировать в наше приложение этот сервис.

![Step01](/img/steps/01.png)

## Создаем новый проект ⚛️

```bash
npx react-native init amplifyPush
```

```bash
cd amplifyPush
```

В корневой директории проекта React Native инициализируем AWS Amplify

```bash
amplify init
```

Отвечаем на вопросы:

![Initialize Amplify](/img/notification/notif_amplify_init.png)

Проект инициализацировался 🚀

## Ставим зависимости:

```bash
yarn add aws-amplify @aws-amplify/pushnotification
```

```bash
npm install --save aws-amplify @aws-amplify/pushnotification
```

Cвязываем зависимость push-уведомлений с помощью команды:

```bash
react-native link @aws-amplify/pushnotification
```

:::caution Чтобы предотвратить эту [ошибку](https://github.com/aws-amplify/amplify-js/issues/5010) в будущем, добавьте библиотеку `netinfo`. Вы можете добавить его в свой проект с помощью следующей команды (если у вас его нет):

```bash
yarn add @react-native-community/netinfo
```

```bash
npm install --save @react-native-community/netinfo
```

:::

![Step02](/img/steps/02.png)

## Android - Настройка Firebase

1. Откройте [Firebase консоль](https://console.firebase.google.com/).
2. Откройте или создайте новый проект для дальнейших действий.
3. Выберите `Cloud Messaging` на панели инструментов.

![Cloud Messaging](/img/notification/notif_cloud_messaging.png)

4.  Нажмите на Android и выполните следующие действия:

- Заполните форму и зарегистрируйте приложение. `Android package name` можно найти в `android/app/build.gradle`. Хранится в `applicationId` выглядеть так:

```java
   gradle title="android/app/build.gradle"
      defaultConfig {
       applicationId "com.amplifypush"
      }
```

- Загрузите файл конфигурации на `android/app`.
- Добавьте Firebase SDK. Рассмотрим `<project>` `android` и `<app-module>` `app`

  каталог в react native проект. Не забудьте добавить последнюю версию `firebase-messaging` [отсюда](https://firebase.google.com/docs/android/setup#available-libraries) а также `firebase-analytics` в `dependencies`

- Запустите проект в Android и вы увидите, подтверждение от Firebase. (вы можете пропустить этот шаг). 5. Открыйте `android/app/src/main/AndroidManifest.xml` и добавьте следующий код в `application`:

```xml
<!--[START Push notification config -->
        <!-- [START firebase_service] -->
        <service
            android:name="com.amazonaws.amplify.pushnotification.RNPushNotificationMessagingService">
            <intent-filter>
                <action android:name="com.google.firebase.MESSAGING_EVENT"/>
            </intent-filter>
        </service>
        <!-- [END firebase_service] -->
        <!-- [START firebase_iid_service] -->
        <service
            android:name="com.amazonaws.amplify.pushnotification.RNPushNotificationDeviceIDService">
            <intent-filter>
                <action android:name="com.google.firebase.INSTANCE_ID_EVENT"/>
            </intent-filter>
        </service>
        <receiver
            android:name="com.amazonaws.amplify.pushnotification.modules.RNPushNotificationBroadcastReceiver"
            android:exported="false" >
            <intent-filter>
                <action android:name="com.amazonaws.amplify.pushnotification.NOTIFICATION_OPENED"/>
            </intent-filter>
        </receiver>
    <!-- [END Push notification config -->
```

![Step03](/img/steps/03.png)

## Настройка Amplify для FCM

1. Добавьте службу push-уведомлений с помощью следующей команды в каталоге проекта:

```bash
 amplify add notifications
```

2. Выберите `FCM`:

```bash
 ? Choose the push notification channel to enable.
 APNS
 ❯ FCM
 Email
 SMS
```

3. Введите точное имя ресурса (или просто нажмите ввод, не заполняя ничего).
4. У вас спросят `ApiKey`. Для этого вам необходимо выполнить следующие шаги:

- Откройте [Firebase консоль ](https://console.firebase.google.com/) и откройте приложение, которое вы создали на предыдущих шагах.
- Нажмите на значок в разделе `Project Overview` на панели инструментов и выберите `Project settings`. ![Настройки проекта](/img/notification/notif_project_settings.png)
- Выберите вкладку `Cloud Messaging` и скопируйте значение `Server key`. ![Настройки проекта](/img/notification/notif_api_key.png)

5. Вставьте запрошенный значения для `ApiKey`.
6. После завершения настройки запустите `amplify push`.

![Step04](/img/steps/04.png)

## iOS - Настройка

1. Устанавливаем `@react-native-community/push-notification-ios`:

```bash
yarn add @react-native-community/push-notification-ios`
```

```bash
npm install --save @react-native-community/push-notification-ios
```

2. Выполните следующую команду для iOS:

   ```bash
   cd ios && pod install && cd ..
   ```

3. Добавьте уведомления iOS командой `amplify add notifications` :

   1. Выбирайте `APNS`:

   ```bash
   ? Choose the push notification channel to enable.
      > APNS
      FCM
      Email
      SMS
   ```

   2. Затем вам будет предложено ввести метод аутентификации. Рекомендуется выбрать сертификат.

   ```bash
   ? Choose authentication method used for APNs (Use arrow keys)
   > Certificate
   Key
   ```

   3. Если вы выбрали сертификат, вам будет предложено указать путь к сертификату .p12. (Вы можете использовать этот [туториал](https://mobincube.zendesk.com/hc/en-us/articles/200511933-How-to-get-the-p12-file-and-provisioning-profile-for-publishing-an-app-on-App-Store)).
   4. Запустите `amplify push`.

   5. Откройте `.xcworkspace` с помощью XCode.

   6. Выберите проект и выберите название проекта в разделе `TARGETS`. Выберите `Signing & Capabilities` и нажмите `+` перед`Capability`. Выберите `Background Mode - Remote Notifications`.

![Step05](/img/steps/05.png)

## Настройка приложения

Как было сказано ранее, `Analytics` должна быть интегрирована вместе с уведомлениями. Это поможет отследить уведомления. Хотя можно использовать пользовательские свойства, рекомендуется использовать файл `aws-exports`.

В `App.js` добавьте следующую конфигурацию:

```js
...
import Amplify from 'aws-amplify'
import PushNotification from '@aws-amplify/pushnotification'
import awsconfig from './aws-exports'

Amplify.configure(awsconfig)

PushNotification.configure(awsconfig)
...
```

![Step06](/img/steps/06.png)

## Working with API

Обычно мы хотим отправлять push-уведомления конкретным пользователям для различных целей. API предоставляет нам различные методы для обработки наших пользователей и push-уведомлений.

## onRegister

Каждое устройство может быть распознано с помощью push-токена, с помощью которого вы можете указать устройство, для которого вы хотите получить push-уведомление. Когда пользователь открывает приложение в первый раз, выдвинутый токен извлекается и сохраняется на устройстве. Вы должны знать о том, что этот метод может быть вызван снова в будущем, поэтому вы должны быть готовы к этой ситуации, чтобы обновить свои данные в соответствии с ним.

Вы можете добавить следующий код в `App.js`:

```js
PushNotification.onRegister((token) => {
  console.log('in app registration', token);
  PushNotification.updateEndpoint(token);
});
```

**attention**: В Android может быть проблема, что этот метод никогда не будет вызван! Однако [обходной путь](https://github.com/aws-amplify/amplify-js/issues/2643#issuecomment-523610933) может быть таким везде, где вам может понадобиться токен:

```js
...
import {NativeModules} from 'react-native'
...
NativeModules.RNPushNotification.getToken((token) => {
  console.log(`PushToken: ${token}`)
})
...
```

## onNotification

Если вы хотите что-то сделать, когда уведомление получено, метод `onNotification` для действий на основе полученного уведомления. Не забывайте, что структура объектов уведомлений отличается от Android и iOS. В iOS, Вам [следует](https://reactnative.dev/docs/pushnotificationios.html#finish) использовать метод `finish`. Вы можете добавить следующий код в `App.js`:

```js
...
import PushNotificationIOS from '@react-native-community/push-notification-ios'
...
PushNotification.onNotification((notification) => {
  console.log('in app notification', notification)
  if (Platform.OS === 'ios') {
    notification.finish(PushNotificationIOS.FetchResult.NoData)
  }
})
```

## onNotificationOpened

Распространенный сценарий - когда пользователь открывает push-уведомление, вызывается `onNotificationOpened`. `App.js` выглядет так:

```js
PushNotification.onNotificationOpened((notification) => {
  console.log('the notification is opened', notification);
});
```

## requestIOSPermissions

Push-уведомление работает только на реальном устройстве и не будет получать никаких уведомлений, если конечный пользователь не даст разрешение. `requestIOSPermissions` нужен для получения этого разрешения. Он может быть вызван без каких-либо параметров, или вы можете настроить объект следующим образом:

```js
PushNotification.requestIOSPermissions();
// or
PushNotification.requestIOSPermissions({
  alert: true,
  badge: true,
  sound: false,
});
```

![Step07](/img/steps/07.png)

## Тестирование

Прежде всего, мы хотим взглянуть на файл `App.js`.

```js
import React from 'react';
import {SafeAreaView, Platform, Text, NativeModules} from 'react-native';

import PushNotificationIOS from '@react-native-community/push-notification-ios';
import Analytics from '@aws-amplify/analytics';
import Amplify from 'aws-amplify';
import PushNotification from '@aws-amplify/pushnotification';
import awsconfig from './aws-exports';

Amplify.configure(awsconfig);
PushNotification.configure(awsconfig);

PushNotification.onRegister(async (token) => {
  console.log('in app registration', token);
  PushNotification.updateEndpoint(token);
});

// In case PushNotification.onRegister didn't work
NativeModules.RNPushNotification.getToken((token) => {
  console.log(`PushToken: ${token}`);
});

PushNotification.onNotification((notification) => {
  console.log('in app notification', notification);
  if (Platform.OS === 'ios') {
    notification.finish(PushNotificationIOS.FetchResult.NoData);
  }
});

PushNotification.onNotificationOpened((notification) => {
  console.log('the notification is opened', notification);
});

const endpointId = Analytics.getPluggable('AWSPinpoint')._config.endpointId;
console.log(`endpoint ID: ${endpointId}`);

if (Platform.OS === 'ios') {
  PushNotification.requestIOSPermissions();
}

const App: () => React$Node = () => {
  return (
    <SafeAreaView>
      <Text>Push Notification</Text>
    </SafeAreaView>
  );
};

export default App;
```

Запускаем проект:

```bash
react-native run-android
```

```bash
react-native run-ios
```

Чтобы идти дальше, нам нужен один из `endpoint ID` или `Push Token`. Подробно объяснено тут `endpoint` в `aws` услугах:

> `Endpoint` представляет пункт назначения, в который вы можете отправлять сообщения, например, на мобильное устройство, адрес электронной почты или номер телефона.

`Push Token` это уникальный идентификатор, который генерируется и присваивается от`GCM`(Android) или `APNS`(iOS) к вашему приложению в конкретном устройстве.

Наиболее очевидное различие между этими двумя заключается в том, что `endpoint` генерируется из `aws`, и определяет приложение в устройстве независимо от платформы (iOS / Android). Но токен в зависимости от платформы генерируется либо от `Apple` или `Google`.

Мы используем `console.log` для копирования и сохраняем эти ключи для следующих шагов. Перейдите в режим разработки и скопируйте в консоль следующие значения:

![Tokens](/img/notification/notif_console_tokens.png)

Хотя существует несколько способов отправки тестового push-уведомления на определенное устройство, мы изучим самый простой способ.

1. Выполните следующую команду в корне проекта:

```bash
amplify notification console
```

2. Консоль приложения будет автоматически открыта в браузере.
3. Выберите `Test messaging` в левой боковой панели:

![Test messaging](/img/notification/notif_aws_notif_console.png)

4. В разделе `Channel` , выберите `Push notifications`.

5. Раздел `Destinations` выглядит следующим образом: ![Destinations](/img/notification/notif_testing_message_dest.png)

6. `Destination type` определяет, хотите ли вы использовать `Endpoint IDs` или `Device Tokens`(или `Push token` в предыдущих шагах) в следующем вводе текста.

7. Вставьте токен, который хотите использовать, на основе `Destination type`.

8. Если вы выбрали `Endpoint IDs` и использовали конечную точку, то `Служба push-уведомлений` может автоматически обнаружить ваше устройство. В противном случае, если вы использовали `Device token`, для IOS выберите `APNS`, а для Android - `FCM`.

9. Вы можете заполнить раздел `Message`, как показано ниже, и нажать кнопку `Send message`. ![Destinations](/img/notification/notif_testing_message_message.png)

10. Вы получите сообщение об успехе, как показано ниже. ![Success](/img/notification/notif_testing_message_success.png) Через пару секунд Вы увидите push-уведомление на своем устройстве: ![Push notification result](/img/notification/notif_android_push_result.png)

## Done ✅

## Ссылки:

[Amplify Docs](https://docs.amplify.aws/lib/push-notifications/getting-started/q/platform/js)

[Setting up Android Push Notifications with AWS Amplify](https://medium.com/@dantasfiles/setting-up-android-push-notifications-with-aws-amplify-e6334c6356d8)

[Testing Push Notifications with AWS Amplify & CLI](https://medium.com/@dantasfiles/testing-push-notifications-with-aws-amplify-9126bd621d3a)

[![Become a Patron!](/img/logo/patreon.png)](https://www.patreon.com/bePatron?u=31769291)
>>>>>>> Создал вкладку Blogging
