---
id: javascript23
title: Классы
sidebar_label: Классы
---

import YouTube from 'react-youtube'

![@serverSerrverlesskiy](/img/javascript/headers/23.jpg)

В JavaScript используется модель прототипного наследования: каждый объект наследует поля (свойства) и методы объекта-прототипа.

## class

Для определения класса используется ключевое🗝️ слово `class`:

```jsx
class MyClass {
  // методы класса
  constructor() { ... }
  method1() { ... }
  method2() { ... }
  method3() { ... }
  ...
}
```

Такой синтаксис📖 называется объявлением🗣️ класса.

![Class](https://media.giphy.com/media/cYaBD8kxE4PZudHBRA/giphy.gif)

:::note Методы в классе не разделяются запятой
Синтаксис📖 классов отличается от литералов объектов. Внутри классов запятые не требуются.
:::

Класс может не иметь названия. С помощью выражения класса можно присвоить класс переменной 🔔 :

```jsx
const UserClass = class {
  // тело класса
}
```

Классы можно экспортировать в виде модулей. Вот пример экспорта по умолчанию:

```jsx
export default class User {
  // тело класса
}
```

А вот пример именованного экспорта:

```jsx
export class User {
  // тело класса
}
```

Класс становится полезным, когда вы создаете экземпляр класса. Экземпляр — это объект, содержащий данные и поведение, описанные 🖊️
классом.

Оператор `new` создает🏗️ экземпляр класса в JavaScript таким образом: `instance = new Class()`.

Например, вы можете создать🏗️ экземпляр класса User 👤 с помощью оператора `new`:

```jsx
const myUser = new User()
```

`new User()` создает🏗️ экземпляр класса `User` 👤.

## Видео

<YouTube videoId="rR_ZHhkx_O0" />

## Инициализация: constructor()

![spangeBob](https://media.giphy.com/media/3oriNZoNvn73MZaFYk/giphy.gif)

`constructor(…)` это специальный метод в теле класса, который инициализирует экземпляр. Это место, где вы можете установить начальные значения для полей или выполнить любые настройки объектов.

В следующем примере конструктор устанавливает начальное значение поля `name`:

```jsx
class User {
  constructor(name) {
    this.name = name
  }
}
```

`constructor` класса `User` использует один параметр `name`, который используется для установки начального значения поля `this.name`.

Внутри конструктора значение `this` равно вновь созданному🏗️ экземпляру.

Аргументы, используемые для создания экземпляра класса, становятся параметрами конструктора 👇 :

```jsx live
function learnJavaScript() {
  class User {
    constructor(name) {
      name // => 'Jon Snow'
      this.name = name
    }
  }

  const user = new User('Jon Snow') //Здесь можно менять значение
  return user.name
}
```

Параметр `name` внутри конструктора имеет значение `Jon Snow`.

Если вы не определяете конструктор для класса, создается🏗️ конструктор по умолчанию. Конструктор по умолчанию является пустой функцией⚙️, которая не изменяет экземпляр.

В классе может быть только один метод с именем `constructor`.

## Отказ от классов

![rejection](https://media.giphy.com/media/l2SpUoAPo0CBOkyxq/giphy.gif)

Так как в курсе нашей школы мы учим разрабатывать мобильные приложения с помощью библиотеки [React](https://ru.reactjs.org), где нововведение [React Hooks](https://ru.reactjs.org/docs/hooks-intro.html) позволяет использовать состояние и другие возможности [React](https://ru.reactjs.org) без написания классов. Поэтому рассказывать о классах больше нет смысла, так как мы от них отказались.

## Проблемы?

![Problem](https://media.giphy.com/media/xTiTnGeUsWOEwsGoG4/giphy.gif)

Пишите в [Discord](https://discord.gg/6GDAfXn) или телеграмм [чат](https://t.me/jscampapp), а также подписывайтесь на наши [новости](https://t.me/javascriptapp)

![JavaScript Camp](/img/bandlink.png)

## Вопросы:

![Question](https://media.giphy.com/media/l0HlRnAWXxn0MhKLK/giphy.gif)

Какое ключевое🗝️ слово для определения класса?

1. `constructor()`
2. `class`
3. `this`

Методы внутри класса разделяются ли запятой.

1. `true`
2. `false`

Сколько методов `constructor()` может находится в одном классе?

1. Неограниченно
2. До десяти
3. Только один

<!-- Что такое геттеры и сеттеры?

1. Это поля
2. Это методы имитирующие поля
3. Это свойства поля

Наследуются ли частные поля и методы родительского класса, дочерним классом?

1. Да
2. Нет

Когда вызывается родительскй конструктор в дочернем классе?

1. Перед this
2. После this -->

Для того чтобы понять, на сколько вы усвоили этот урок, пройдите тест в [мобильном приложении](http://onelink.to/njhc95) нашей школы по этой теме.

![Sumerian school](/img/app.jpg)

<!--
## Геттеры и сеттеры

![Math](https://media.giphy.com/media/uWzbH8xJGIwOBPfzhc/giphy.gif)

Геттеры и сеттеры — это вычисляемые свойства. Это методы, имитирующие поля, но позволяющие читать и записывать 🖊️ данные.

Геттеры используются для получения данных, а сеттеры — для их изменения.

Пример:

```jsx
class User {
  #nameValue

  constructor(name) {
    this.name = name
  }

  get name() {
    return this.#nameValue
  }

  set name(name) {
    if (name === '') {
      throw new Error('Имя пользователя не может быть пустым')
    }
    this.#nameValue = name
  }
}

const user = new User('Печорин')
user.name // вызывается геттер, Печорин
user.name = 'Бэла' // вызывается сеттер

user.name = '' // Имя пользователя не может быть пустым
```

## Наследование: extends

![Throne](https://media.giphy.com/media/l1KVcMMxJJpks23cs/giphy.gif)

Классы в JavaScript поддерживают наследование с помощью ключевого🗝️ слова `extends`.

В выражении `class Child extends Parent { }` класс `Child` наследует от класса `Parent` конструктор, поля и методы.

Создадим🏗️ дочерний класс `ContentWriter`, расширяющий родительский класс `User` 👤:

```jsx
class User {
  name

  constructor(name) {
    this.name = name
  }

  getName() {
    return this.name
  }
}

class ContentWriter extends User {
  posts = []
}

const writer = new ContentWriter('Лермонтов')

writer.name // Лермонтов
writer.getName() // Лермонтов
writer.posts // []
```

`ContentWriter` наследует от `User` конструктор, метод `getName()` и поле `name`. В самом `ContentWriter` определяется новое поле `posts`.

Обратите внимание, что частные поля и методы родительского класса не наследуются дочерними классами.

### Родительский конструктор: super() в constructor()

![parents](https://media.giphy.com/media/QWMjLXYuRpl5cvCQ9r/giphy.gif)

Для того, чтобы вызвать конструктор родительского класса в дочернем классе, следует использовать специальную функцию⚙️ `super()`, доступную в конструкторе дочернего класса.

Пусть конструктор `ContentWriter` вызывает родительский конструктор и инициализирует поле `posts` 👇 :

```jsx live
function learnJavaScript() {
  class User {
    name

    constructor(name) {
      this.name = name
    }

    getName() {
      return this.name
    }
  }

  class ContentWriter extends User {
    posts = []

    constructor(name, posts) {
      super(name)
      this.posts = posts
    }
  }

  const writer = new ContentWriter('Лермонтов', ['Герой нашего времени'])
  writer.name // Лермонтов
  writer.posts // ['Герой нашего времени']

  return writer.name //name можно заменить на posts и посмотреть результат
}
```

`super(name)` в дочернем классе `ContentWriter` вызывает конструктор родительского класса `User`.

Обратите внимание, что в дочернем конструкторе перед использованием ключевого🗝️ слова `this` вызывается `super()`. Вызов `super()` "привязывает" родительский конструктор к экземпляру.

![super](https://media.giphy.com/media/10mTnPIEHNZpAs/giphy.gif)

```jsx
class Child extends Parent {
  constructor(value1, value2) {
    // не работает!
    this.prop2 = value2
    super(value1)
  }
}
```

## Пример

![math](https://media.giphy.com/media/3orieN7HEHI0tw8x5C/giphy.gif)

```jsx
class Animal { //Создание класса Animal. Классы называют с большой буквы

static type = 'ANIMAL' //При помощи ключевого слова static можно объявлять переменные внутри класса. Их можно вызвать только самим классом, т.е. Animal.type

  constructor(options) { //Конструктор принимает объект options
    this.name = options.name // Инициализация полей класса
    this.age = options.age
    this.hasTail = options.hasTail
  }

  voice() { //Метод для класса Animal. Можно вызвать у объекта cat как cat.voice()
    alert('I am Animal!')
  }
}

get ageInfo(){ //Создание геттера ageInfo
  return this.age * 7 //Если вызвать геттер у объекта cat, то получиться 5 * 7 = 35
}

set ageInfo(newAge) { //Создание сеттера ageInfo.
  this.age = newAge // Если выполнить у объекта cat команду cat.ageInfo = 8, то полю age присвоится значение 8
}

const cat = new Animal({ //Создание объекта при помощи класса Animal
  name: 'Cat',
  age: 5,
  hasTail: true
})
```

![Wow](https://media.giphy.com/media/3oriO13KTkzPwTykp2/giphy.gif) -->

<!-- ## Вопросы:

![Question](https://media.giphy.com/media/l0HlRnAWXxn0MhKLK/giphy.gif)

Для того чтобы понять, на сколько вы усвоили этот урок, пройдите тест в [мобильном приложении](http://onelink.to/njhc95) нашей школы по этой теме.

![Sumerian school](/img/app.jpg) -->

<!-- Сколько методов constructor() может находится в одном классе?

1. Неограниченно
2. До десяти
3. Только один

Что такое геттеры и сеттеры?

1. Это поля
2. Это методы имитирующие поля
3. Это свойства поля

Наследуются ли частные поля и методы родительского класса, дочерним классом?

1. Да
2. Нет

Когда вызывается родительскй конструктор в дочернем классе?

1. Перед this
2. После this -->

## Ссылки:

1.  [MDN web docs](https://developer.mozilla.org/ru/docs/Web/JavaScript/Reference/Classes)
2.  [Learn JavaScript](https://learn.javascript.ru/class)

## Contributors ✨

Thanks goes to these wonderful people ([emoji key](https://allcontributors.org/docs/en/emoji-key)):

<!-- ALL-CONTRIBUTORS-LIST:START - Do not remove or modify this section -->
<!-- prettier-ignore-start -->
<!-- markdownlint-disable -->
<table>
  <tr>
    <td align="center"><a href="https://github.com/FELiX-RN"><img src="https://avatars0.githubusercontent.com/u/72006627?v=4?s=200" width="200px;" alt=""/><br /><sub><b>Philipp Dvinyaninov</b></sub></a><br /><a href="https://github.com/gHashTag/react-native-village/commits?author=FELiX-RN" title="Documentation">📖</a></td>
    <td align="center"><a href="https://fullstackserverless.github.io/"><img src="https://avatars0.githubusercontent.com/u/6774813?v=4?s=200" width="200px;" alt=""/><br /><sub><b>Dmitriy Vasilev</b></sub></a><br /><a href="#financial-gHashTag" title="Financial">💵</a></td>
    <td align="center"><a href="https://github.com/Resoner2005"><img src="https://avatars1.githubusercontent.com/u/75675814?v=4?s=200" width="200px;" alt=""/><br /><sub><b>Resoner2005</b></sub></a><br /><a href="https://github.com/gHashTag/react-native-village/issues?q=author%3AResoner2005" title="Bug reports">🐛 🎨 🖋</a></td>
    <td align="center"><a href="https://github.com/Navernoss"><img src="https://avatars0.githubusercontent.com/u/75784137?v=4?s=200" width="200px;" alt=""/><br /><sub><b>Navernoss</b></sub></a><br /><a href="#content-Navernoss" title="Content">🖋 🐛 🎨 </a></td>
  </tr>
  
</table>

<!-- markdownlint-restore -->
<!-- prettier-ignore-end -->

<!-- ALL-CONTRIBUTORS-LIST:END -->

[![Become a Patron!](/img/logo/patreon.jpg)](https://www.patreon.com/bePatron?u=31769291)
