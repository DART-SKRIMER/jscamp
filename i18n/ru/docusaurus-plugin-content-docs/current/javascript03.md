---
id: javascript03
title: Переменка
sidebar_label: Переменка
---

import YouTube from 'react-youtube'

![@serverSerrverlesskiy](/img/javascript/headers/03.jpg)

## Переменные

Переменные 🔔 (Variables, сокращенно `var`) — это контейнер 📦 для таких значений, как числа, используемые в сложении ➕ , или строка, которую мы могли бы использовать как часть предложения, а также другие типы данных с которыми мы познакомимся позже.

![Container](https://media.giphy.com/media/0T0FUiZl51VPCLsqLR/giphy.gif)

## Видео

<YouTube videoId="gCqxA_JOtmw" />

## Объявление переменной

![Announcement](https://media.giphy.com/media/cYaBD8kxE4PZudHBRA/giphy.gif)

Чтобы использовать переменную, вы сначала должны ее создать🏗️, или, если быть точнее, объявить🗣️ переменную. Чтобы сделать это, мы вводим ключевое🗝️ слово `var`, за которым следует имя, которое вы хотите дать своей переменной. Приведённая ниже инструкция создаёт🏗️ (другими словами: объявляет🗣️ или определяет) переменную с именем «message»:

```jsx live
function learnJavaScript() {
  var message = ''

  return message
}
```

Здесь мы создаем переменную 🔔 `message`. В настоящее время ⏱️ она не содержит значение, если сказать точней, то переменная содержит пустую строку.

## Присвоение значения переменной

![Memory](https://media.giphy.com/media/3o6ZtafpgSpvIaKhMI/giphy.gif)

Как только переменная 🔔 объявлена, ей можно присвоить значение. Для этого пишется 🖊️ имя переменной 🔔 , затем следует знак равенства `=`, а за ним значение, которое вы хотите присвоить. Например 👇 :

```jsx live
function learnJavaScript() {
  var message
  message = 'My name is ...'
  //Мы можем получить к ней доступ, используя имя переменной
  return message
}
```

В `RESULT` значение, которое вы назначили переменной 🔔 , возвращаемой в консоли. Поиграйтесь 🎮 со значениями переменной 🔔 , например дополните выражение своим именем.

Для краткости можно совместить объявление переменной 🔔 и запись 🖊️ в одну строку 👇 :

```jsx live
function learnJavaScript() {
  var message = 'Hello!' // определяем переменную и присваиваем ей значение
  return message
}
```

## Обновление переменной

![Update](https://media.giphy.com/media/FP47IFqWyXfdKYU6VG/giphy.gif)

Одна из особенностей переменных 🔔 — их значение может меняться.
Когда переменной 🔔 присваивается значение, вы можете изменить (обновить) это значение, просто указав другое значение. Давайте взглянем на простой пример 👇 :

```jsx live
function learnJavaScript() {
  var message = 'Bob' // сейчас message Bob
  message = true // а теперь message true
  message = 35 // и в итоге message 35

  return message
}
```

Еще одна особенность переменных 🔔 заключается в том, что они могут содержать практически все, а не только строки и числа. Переменные 🔔 могут также содержать сложные данные и даже целые функции. Об этом вы узнаете больше при дальнейшем изучении курса.

:::tip На заметку!
Мы говорим, что переменные содержат значения. Это важное различие. Переменные не являются самими значениями! Они представляют собой контейнеры📦 для значений. Представьте, что они похожи на маленькие картонные коробки📦, в которых вы можете хранить вещи.
:::

![Variables](https://mdn.mozillademos.org/files/13506/boxes.png)

![Hello World](https://media.giphy.com/media/26his8ERHOSxKuWw8/giphy.gif)

## Правила именования переменных

![Rules](https://media.giphy.com/media/XK8I8Am1gSe17MiJ2m/giphy.gif)

Вы можете назвать переменную 🔔 как угодно, но есть ограничения. Как правило, вы должны придерживаться только латинских символов (0-9, a-z, A-Z) и символа подчеркивания.

- Не рекомендуется использование других символов, потому что они могут вызывать ошибки или быть непонятными для международной аудитории.
- Не используйте символы подчеркивания в начале имен переменных 🔔 - это используется в некоторых конструкциях JavaScript для обозначения конкретных вещей.
- Не используйте числа в начале переменных 🔔 . Это недопустимо и приведет к ошибке.
- Общепринято придерживаться так называемый "lower camel case"(верблюжийРегистр - camelCase - называется так из-за "горбов" которые образуют первые буквы слов), где вы склеиваете несколько слов, используя строчные буквы для всего первого слова, а затем заглавные буквы последующих слов. Мы использовали это для наших имен переменных 🔔 в этой статье.
- Делайте имена переменных 🔔 такими, чтобы было интуитивно понятно, какие данные они содержат. Не используйте только отдельные буквы / цифры или большие длинные фразы.
- Переменные 🔔 чувствительны к регистру, так что `myage` и `myAge` - разные переменные 🔔 .
- И последнее - вам также нужно избегать использования зарезервированных слов JavaScript в качестве имен переменных 🔔 - под этим мы подразумеваем слова, которые составляют фактический синтаксис JavaScript! Таким образом, вы не можете использовать слова типа var, function, let, и for для имен переменных 🔔 . Браузеры распознают их как разные элементы кода, и поэтому возникают ошибки.

## Список зарезервированных слов

![Reserved](https://media.giphy.com/media/3o6Mb3eci7bVDKBR2o/giphy.gif)

Этими словами мы не можем называть переменные 🔔 , так как они зарезервированы в языке JavaScript.
`break`, `case`, `catch`, `class`, `const`, `continue`, `debugger`, `default`, `delete`, `do`, `else`, `export`, `extends`, `finally`, `for`, `function`, `if`, `import`, `in`, `instanceof`, `new`, `return`, `super`, `switch`, `this`, `throw`, `try`, `typeof`, `var`, `void`, `while`, `with`, `yield`

## Свободная типизация

![Freedom](https://media.giphy.com/media/6901DbEbbm4o0/giphy.gif)

JavaScript - это «свободно типизируемый язык👅», что означает, что в отличие от некоторых других языков👅 вам не нужно указывать, какой тип данных будет содержать переменная 🔔 (например, числа, строки, массивы и т. д.).

Например, если вы объявите переменную 🔔 и присвоите ей значение, заключенное в кавычки, браузер будет обрабатывать переменную 🔔 как строку 👇 :

```jsx live
function learnJavaScript() {
  var myString = 'Hello'
  // Она все равно будет строкой, даже если содержит числа, поэтому будьте осторожны:
  var myNumber = '500' // упс, это все еще строка (string)

  myNumber = 500 // так-то лучше, теперь это число (number). Удалите эту строчку и посмотрите на тип данных.

  return typeof myNumber
}
```

## Устаревшее ключевое слово "var"

![Old](https://media.giphy.com/media/3orieJI3IdkKWIsAGA/giphy.gif)

Обычно `var` не используется в современных скриптах, но всё ещё может скрываться в старых. Связано это с тем, что он ведет себя не однозначно, поэтому вместо `var` мы будем использовать `let` для переменных 🔔 , а `const` для постоянных - констант.

🔔 Переменка закончилась, бежим на следующий урок!

## Проблемы?

![Problem](https://media.giphy.com/media/xTiTnGeUsWOEwsGoG4/giphy.gif)

Пишите в [Discord](https://discord.gg/6GDAfXn) или телеграмм [чат](https://t.me/jscampapp), а также подписывайтесь на наши [новости](https://t.me/javascriptapp)

![JavaScript Camp](/img/bandlink.png)

## Вопросы:

![Question](https://media.giphy.com/media/l0HlRnAWXxn0MhKLK/giphy.gif)

Что такое переменные?

1. Контейнеры для значений
2. Переменные значения
3. Латинские буквы

Что могут содержать переменные?

1. Только строки и числа
2. Все типы данных
3. Только сложные данные и функции

Как прописать команду присвоения переменной?

1. `var`
2. `var` [название переменной] =
3. `var` [название переменной]

Как обновить переменную?

1. Переменную нельзя обновить
2. Указать другое значение переменной
3. Задать специальную команду

Чего нет в правилах именования переменных?

1. Числа в начале переменных
2. Не использовать зарезервированные слова
3. Придерживаться латинских символов

Как прописать значение переменной, чтобы браузер обрабатывал переменную как строку?

1. Без кавычек
2. В кавычках
3. В скобках

Какое ключевое🗝️ слово мы не используем для определения переменных?

1. `let`
2. `const`
3. `var`

Какой вид заглавных букв (т.е. регистр) следует использовать в именах переменных в JavaScript?

1. case
2. camel
3. camelCase

Это допустимый синтаксис JavaScript? Если нет, то почему?

```jsx
let myMood = \"Curious about JavaScript\" \n let myMood = \"Excited to use my new superpowers\"\n myMood
```

1. Вторая переменная без `let`
2. Действительно
3. SyntaxError

Что означает один знак равенства в утверждении?

1. Сравнить
2. Значение присваивается переменной
3. Равенство

Какое ключевое слово следует использовать для создания любой переменной, которая, как вы знаете, не будет изменена?

1. `let`
2. `const`
3. `var`

Когда следует использовать ключевое слово `var` в собственном коде?

1. Никогда
2. Всегда
3. Часто

Для того чтобы понять, на сколько вы усвоили этот урок, пройдите тест в [мобильном приложении](http://onelink.to/njhc95) нашей школы по этой теме.

![Sumerian school](/img/app.jpg)

## Ссылки:

1. [MDN web docs](https://developer.mozilla.org/ru/docs/Learn/JavaScript/Первые_шаги/Variables)
2. [Код для подростков: прекрасное руководство по программированию для начинающих, том 1: Javascript - Jeremy Moritz ](https://www.amazon.com/Code-Teens-Beginners-Programming-Javascript-ebook/dp/B07FCTLVPC)
3. [JavaScript.ru](https://learn.javascript.ru/types)

## Contributors ✨

Thanks goes to these wonderful people ([emoji key](https://allcontributors.org/docs/en/emoji-key)):

<table>
  <tr>
    <td align="center"><a href="https://fullstackserverless.github.io/"><img src="https://avatars0.githubusercontent.com/u/6774813?v=4?s=200" width="200px;" alt=""/><br /><sub><b>Dmitriy Vasilev</b></sub></a><br /> <a href="https://github.com/gHashTag/react-native-village/commits?author=gHashTag" title="Documentation">📖</a></td>
    <td align="center"><a href="https://github.com/Resoner2005"><img src="https://avatars1.githubusercontent.com/u/75675814?v=4?s=200" width="200px;" alt=""/><br /><sub><b>Resoner2005</b></sub></a><br /><a href="https://github.com/gHashTag/react-native-village/issues?q=author%3AResoner2005" title="Bug reports">🐛 🎨 🖋</a></td>
  </tr>

</table>

[![Become a Patron!](/img/logo/patreon.jpg)](https://www.patreon.com/bePatron?u=31769291)

<!-- ## Супер команда console.log()

Перед тем как продолжить, я познакомлю вас с супер секретной и супер полезной командой `console.log()`, которую вы будете очень и очень часто использовать во время разработки программ.
Так вот, чтобы вывести в консоль отладочную информацию только для разработчиков (пользователи её увидеть не смогут; как вы знаете, большинство людей не подозревает даже о существовании самой консоли, а не то что о секретных «логах»!), напишите:

```javascript
console.log('Совершенно секретно! Только для разработчиков!')
````

Как видно из названия функции, мы выводим в консоль «лог» (то есть информацию о работе системы). Этой доброй суперспособностью разработчики пользуются постоянно. Скажем, когда у вас были сообщения об ошибках, вы видели в консоли именно это — интерпретатор выдавал («логгировал») в консоль информацию о работе системы, чтобы вы могли прочесть и исправить нужные параметры. Словом, очень полезная штука. Вам не раз и не два придётся прибегнуть к помощи console.log, так что запомните эту функцию!

```javascript
console.log('Выведите любое сообщение, какое пожелаете')
console.log('просто введите сюда какую-нибудь ' + 'строку')
var сообщение = 'А ещё в качестве аргумента можно использовать переменные!'
console.log(сообщение)
var чтоНужноИзучить = 'JavaScript'
console.log('Я изучу ' + чтоНужноИзучить) -->

```

```
