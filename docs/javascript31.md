---
id: javascript31
title: ES6 Modules (import, export, require)
sidebar_label: ES6 Modules (import, export, require)
---

![@serverSerrverlesskiy](/img/javascript/headers/31.jpg)

С появлением `ES2015 (ES6)` со встроенной поддержкой модулей в JavaScript каждый файл стал предсталять собой отдельный модуль. Чтобы сделать объекты, функции, классы или переменные 🔔 доступными для внешнего мира, достаточно просто экспортировать их, а затем импортировать, где это необходимо, в другие файлы проекта.

## `Export` (экспорт)

![Export](https://media.giphy.com/media/JlxFcvNuzlPYA/giphy.gif)

Вы можете экспортировать объекты по одному. То, что не экспортируется, не будет доступно непосредственно за пределами модуля с целью безопасности:

```javascript
export const myNumbers = [1, 2, 3, 4]
const animals = ['Panda', 'Bear', 'Eagle'] // Недоступно вне модуля

export function myLogger() {
  return myNumbers, animals
}

export class Alligator {
  constructor() {
    // ...
  }
}
```

Или вы можете экспортировать желаемые элементы одним оператором в конце модуля:

```javascript
export { myNumbers, myLogger, Alligator }
```

### Экспорт с псевдонимом

Вы также можете дать псевдонимы экспортированным элементам с помощью ключевого🗝️ слова `as:`

```javascript
export { myNumbers, myLogger as Logger, Alligator }
```

### Экспорт по умолчанию

![default](https://media.giphy.com/media/3oEduLzte7jSNmq4z6/giphy.gif)

Вы можете определить экспорт по умолчанию с помощью `default:`

```javascript
export const myNumbers = [1, 2, 3, 4]
const animals = ['Panda', 'Bear', 'Eagle']

export default function myLogger() {
  console.log(myNumbers, pets)
}

export class Alligator {
  constructor() {
    // ...
  }
}
```

## `Import` (импорт)

![Import](https://media.giphy.com/media/3obeh2rCsGMkZdcTVy/giphy.gif)

Импорт также очень прост, через ключевое🗝️ слово `import,` где импортируемые объекты в фигурных скобках, а затем указываем расположение модуля 'app.js' относительно текущего файла:

```javascript
import { myLogger, Alligator } from 'app.js'
```

### Импорт с псевдонимом

![Rename](https://media.giphy.com/media/wAc290lRAgPAs/giphy.gif)

Можно использовать псевдонимы объектов во время импорта:

```javascript
import myLogger as Logger from 'app.js'
```

### Импорт всех экспортированных участников

![Import](https://media.giphy.com/media/8TkagzJHXLWmI/giphy.gif)

Вы можете импортировать все `*`, что возможно с помощью подключаемого модуля:

```javascript
import * as Utils from 'app.js'
```

Это позволяет вам получить доступ к объектам с точечной нотацией:

```javascript
Utils.myLogger()
```

### Импорт модуля с объектом по умолчанию

![import](https://media.giphy.com/media/fUdaShpuYH4GU647lJ/giphy.gif)

Вы импортируете объект по умолчанию, давая ему имя по вашему выбору. В следующем примере `Logger` это имя, присвоенное импортированному объекту по умолчанию:

```javascript
import Logger from 'app.js'
```

А вот как можно импортировать нестандартные элементы поверх объекта по умолчанию:

```javascript
import Logger, { Alligator, myNumbers } from 'app.js'
```

Инструкция `import` используется для импорта ссылок на значения, экспортированные из внешнего модуля. Импортированные модули находятся в строгом режиме независимо от того, объявляете🗣️ ли вы их как таковые или нет.

## `Require` (затребовать)

![download](https://media.giphy.com/media/nWGRHBnAl5Kmc/giphy.gif)

Использование стандарта `ES6` рекомендуется, так как это должно быть выгодно, когда нативная поддержка браузеров выпущена. Причина в том, что вы можете импортировать частичные файлы из одного файла, в то время как с `CommonJS` вы должны требовать весь файл.

- **ЕС6** → import, export default, export
- **CommonJS** → `require,` module.exports, exports.foo

Самое важное, что нужно знать, - это то, что модули ES6 действительно являются официальным стандартом, а модули CommonJS (Node.js) - нет.

Ниже приведено их общее употребление.

### ES6 экспорт по умолчанию

![import](https://media.giphy.com/media/gibvnAbdWQEiGtPlk3/giphy.gif)

```javascript
// say.js
let hello = () => {
  return 'Hello'
}
export default hello
```

```javascript
// app.js
import hello from './say'
hello() // returns Hello
```

### ЕС6 экспортировать несколько и импортировать несколько:

![Many_people](https://media.giphy.com/media/tsSUOFubsatTG/giphy.gif)

```javascript
// say.js
let hello1 = () => {
  return 'Hello1'
}
let hello2 = () => {
  return 'Hello2'
}
export { hello1, hello2 }
```

```javascript
// app.js
import { hello1, hello2 } from './say'
hello1() // returns Hello1
hello2() // returns Hello2
```

### CommonJS module.exports

![download](https://media.giphy.com/media/3o7TKWzRShjaQxMGCk/giphy.gif)

```javascript
// say.js
let hello = () => {
  return 'Hello'
}
module.exports = hello
```

```javascript
// app.js
const hello = require('./say')
hello() // returns Hello
```

### CommonJS module.exports множественное число

![binary_code](https://media.giphy.com/media/l1J9RFoDzCDrkqtEc/giphy.gif)

```javascript
// say.js
let hello1 = () => {
  return 'Hello1'
}
let hello2 = () => {
  return 'Hello2'
}
module.exports = {
  hello1,
  hello2
}
```

```javascript
// app.js
const hello = require('./say')
hello.hello1() // returns Hello1
hello.hello2() // returns Hello2
```

Фактическая загрузка любого модуля при использовании `require()` происходит в 5 шагов:

- Разрешение
- Загрузка
- Оберточная бумага
- Оценка
- Кеширование.

Первый 1️⃣ шаг `resolution` - это внутренний шаг, на котором `node.js` вычисляет пути к файлам и т. Д. На втором, то есть `loadingnode` извлекает код📟 в текущем процессе. `In wrappingin` завершает код📟 функции⚙️, как показано выше, а затем отправляет его в виртуальную машину, `evaluatingа` затем в конечном итоге `caches.`

Итак, в основном node никогда не знает, какие символы будет экспортировать модуль `CommonJS,` до тех пор, пока модуль не будет фактически оценен. И это самая большая разница с модулями `ECMAScript,` потому что ESM является лексическим и, следовательно, экспортируемые символы известны до того, как код📟 фактически оценивается.

## Подробный синтаксис

![book](https://media.giphy.com/media/s6OiiampNcye4/giphy.gif)

```javascript
import defaultExport from "module-name"
import * as name from "module-name"
import { export } from "module-name"
import { export as alias } from "module-name"
import { export1 , export2 } from "module-name"
import { export1 , export2 as alias2 , […] } from "module-name"
import defaultExport, { export [ , […] ] } from "module-name"
import defaultExport, * as name from "module-name"
import "module-name"
import("/module-name.js").then(module => {…}) // Динамический импорт
```

**defaultExport**

Имя объекта, который будет ссылаться на значение экспорта по умолчанию (дефолтный экспорт) из модуля.

**module-name**

Имя модуля для импорта. Это зачастую относительный или абсолютный путь к `.js` файлу модуля без указания расширения .js. Некоторые сборщики могут разрешать или даже требовать использования расширения; проверяйте своё рабочее окружение. Допускаются только строки с одиночными или двойными кавычками.

**name**

Имя локального обьекта, который будет использован как своего рода пространство имен, ссылающееся на импортируемые значения.

**export, exportN**

Имена значений, которые будут импортированы.

**alias, aliasN**

![Export](https://media.giphy.com/media/YrZmRyiCfmJCnH13QV/giphy.gif)

Имена, которые будут ссылаться на импортируемые значения.

### Описание

![Book](https://media.giphy.com/media/V8oj5SlnHsZMY/giphy.gif)

Параметр name это имя локального обьекта, который будет использован как своего рода пространство имен, ссылающееся на импортируемые значения. Параметры export определяют отдельные именованные значения, в то время как `import * as name` импортирует все значения.

### Импорт всего содержимого модуля

![insert](https://media.giphy.com/media/3o6ZtafpgSpvIaKhMI/giphy.gif)

Этот код📟 вставляет объект myModule в текущую область видимости, содержащую все экспортированные значения из модуля, находящегося в файле `/modules/my-module.js.`

```javascript
import * as myModule from '/modules/my-module.js'
```

В данном случае, доступ к импортируемым значениям можно осуществить с использованием имени модуля (в данном случае "myModule") в качестве пространства имен. Например, если импортируемый выше модуль включает в себя экспорт метода `doAllTheAmazingThings(),` вы можете вызвать его так:

```javascript
myModule.doAllTheAmazingThings()
```

### Импорт единичного значения из модуля

![Download](https://media.giphy.com/media/LHZyixOnHwDDy/giphy.gif)

Определенное ранее значение, названное myExport, которое было экспортировано из модуля `my-module` либо неявно (если модуль был экспортирован целиком), либо явно (с использованием инструкции export), позволяет вставить myExport в текущую область видимости.

```javascript
import { myExport } from '/modules/my-module.js'
```

### Импорт нескольких единичных значений

![insert](https://media.giphy.com/media/8OPgOmnuVIvoFyXR4w/giphy.gif)

Этот код📟 вставляет оба значения foo и bar в текущую область видимости.

```javascript
import { foo, bar } from '/modules/my-module.js'
```

### Импорт значений с использованием более удобных имен

![Import](https://media.giphy.com/media/jO1YINDl4HRdXDh3zX/giphy.gif)

Вы можете переименовать значения, когда импортируете их. Например, этот код📟 вставляет shortName в текующую область видимости.

```javascript
import { reallyReallyLongModuleExportName as shortName } from '/modules/my-module.js'
```

### Переименование нескольких значений в одном импорте

![Renaming](https://media.giphy.com/media/emc9V9NchQZKU/giphy.gif)

Код📟 , который импортирует несколько значений из модуля, используя более удобные имена.

```javascript
import { reallyReallyLongModuleExportName as shortName, anotherLongModuleName as short } from '/modules/my-module.js'
```

### Импорт модуля для использования его побочного эффекта

![Dowlands](https://media.giphy.com/media/FgiHOQyKUJmwg/giphy.gif)

Импорт всего модуля только для использования побочного эффекта от его вызова, не импортируя что-либо. Это запускает глобальный код📟 модуля, но в действительности не импортирует никаких значений.

```javascript
import '/modules/my-module.js'
```

### Импорт значения по умолчанию

![Download](https://media.giphy.com/media/hyZffrEauy8QU/giphy.gif)

Есть возможность задать дефолтный export (будь то объект, функция⚙️, класс или др.). Инструкция import затем может быть использована для импорта таких значений.

Простейшая версия прямого импорта значения по умолчанию:

```javascript
import myDefault from '/modules/my-module.js'
```

Возможно также использование такого синтаксиса📖 с другими вариантами из перечисленных выше (импорт пространства имен или именованный импорт). В таком случае, импорт значения по умолчанию должен быть определён первым. Для примера:

```javascript
import myDefault, * as myModule from '/modules/my-module.js'
// myModule использовано как пространство имен
или

import myDefault, { foo, bar } from '/modules/my-module.js'
// именованный импорт конкретных значений
```

### Импорт переменных

![Download](https://media.giphy.com/media/Y3Bb5MNAtOC4H73qbU/giphy.gif)

Если вы импортируете переменные 🔔 , то в данной области видимости они ведут себя как константы.

Такой код📟 выведет ошибку🙅‍♂️:

**my-module.js**

```javascript
export let a = 2
export let b = 3

main.js
import { a, b } from '/modules/my-module.js'
a = 5
b = 6
// Uncaught TypeError: Assignment to constant variable.
```

Для импорта можно воспользоваться объектом в котором хранятся эти переменные 🔔 .

Такой код📟 будет рабочим:

**my-module.js**

```javascript
export let obj = { a: 2, b: 4 }
```

**main.js**

```javascript
import { obj } from '/modules/my-module.js'

obj.a = 1
obj.b = 4
```

Учитывая, что import хранит именно ссылки на значения, экспортированные из внешнего модуля, то это можно использовать как замыкания.

## Вопросы:

![Question](https://media.giphy.com/media/l0HlRnAWXxn0MhKLK/giphy.gif)

Для того чтобы понять насколько вы усвоили этот урок пройдите тест в [мобильном приложении](http://onelink.to/njhc95) в нашей школы по этой теме.

![Sumerian school](/img/app.png)

1. Экспортировать желаемые элементы одним оператором в конце модуля можно командой:

- export { myNumbers, myLogger, Alligator }
- export const myNumbers = [1, 2, 3, 4]
- import myLogger as Logger from 'app.js'

2. Импорт всех экспортированных участников производится командой:

- import \* as Utils from 'app.js'
- import { myLogger, Alligator } from 'app.js'
- import myLogger as Logger from 'app.js'

3. Для указания конкретных функций экспорта используется:

- export { hello1, hello2 }
- import { hello1, hello2 } from './say'
- const hello = require('./say')

4. Команда `import myDefault, {foo, bar} from '/modules/my-module.js'` выполняет:

- именованный импорт конкретных значений
- экспорта по умолчанию (дефолтный экспорт) из модуля
- импортирует все значения.

## Ссылки:

1. [MDN web doc. Статья "Модули в ECMAScript 6: будущее уже сейчас"](https://frontender.info/es6-modules/)
2. [Статья "ES6 Modules and How to Use Import and Export in JavaScript"](https://www.digitalocean.com/community/tutorials/js-modules-es6)
3. [Статья "require против ES6 import / export"](https://coderoad.ru/31354559/%D0%98%D1%81%D0%BF%D0%BE%D0%BB%D1%8C%D0%B7%D0%BE%D0%B2%D0%B0%D0%BD%D0%B8%D0%B5-Node-js-require-%D0%BF%D1%80%D0%BE%D1%82%D0%B8%D0%B2-ES6-import-export)

## Contributors ✨

Thanks goes to these wonderful people ([emoji key](https://allcontributors.org/docs/en/emoji-key)):

<!-- ALL-CONTRIBUTORS-LIST:START - Do not remove or modify this section -->
<!-- prettier-ignore-start -->
<!-- markdownlint-disable -->
<table>
  <tr>
    <td align="center"><a href="https://github.com/KoDim-React"><img src="https://avatars1.githubusercontent.com/u/72087863?v=4?s=200" width="200px;" alt=""/><br /><sub><b>Dmitriy K.</b></sub></a><br /><a href="#mentoring-KoDim-React" title="Mentoring">📖</a></td>
    <td align="center"><a href="https://fullstackserverless.github.io/"><img src="https://avatars0.githubusercontent.com/u/6774813?v=4?s=200" width="200px;" alt=""/><br /><sub><b>Dmitriy Vasilev</b></sub></a><br /><a href="#financial-gHashTag" title="Financial">💵</a></td>
     <td align="center"><a href="https://github.com/Resoner2005"><img src="https://avatars1.githubusercontent.com/u/75675814?v=4?s=200" width="200px;" alt=""/><br /><sub><b>Resoner2005</b></sub></a><br /><a href="https://github.com/gHashTag/react-native-village/issues?q=author%3AResoner2005" title="Bug reports">🐛 🎨 🖋</a></td>
     <td align="center"><a href="https://github.com/Navernoss"><img src="https://avatars0.githubusercontent.com/u/75784137?v=4?s=200" width="200px;" alt=""/><br /><sub><b>Navernoss</b></sub></a><br /><a href="#content-Navernoss" title="Content">🖋 🐛 🎨 </a></td>
  </tr>
 
</table>

<!-- markdownlint-restore -->
<!-- prettier-ignore-end -->

<!-- ALL-CONTRIBUTORS-LIST:END -->

[![Become a Patron!](/img/logo/patreon.png)](https://www.patreon.com/bePatron?u=31769291)
