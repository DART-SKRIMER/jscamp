---
id: typescript08
title: Интерфейсы
sidebar_label: Интерфейсы
---

Одним из основных принципов _TypeScript_ является то, что типизация основана на структуре объектов. Такой способ типизации называют `неявной` или `«утиной»` — объект относят к тому или иному типу (классу, интерфейсу), если он имеет (реализует) все его свойства и методы. Интерфейсы в TS применяются как раз для того, чтобы описывать нужные вам типы.

## Простой пример

Лучший способ узнать, как работают интерфейсы - начасть с простого примера:

[Playground Link](https://www.typescriptlang.org/play?#code/GYVwdgxgLglg9mABAcxgNwKYDEBOIZSIAUweBAXIgN6JgCGAthpQM5Q4xjKIC+AlNQBQiEYggIWcADYYAdFLjIiAcgDi6DIihxETRMsQBqRKXxRZ9Jn0E9BgmYQYBPXGZaIAvNVqNm+gEJ09PTKADSILADuGBhQYBgsLJQA7OEARggJlMB0UiyatqiYrgREziVQLHxAA)

```jsx
function giveFruit(fruit: { name: string }) {
  console.log('Give to me ' + fruit.name)
}

let myFruits = { name: 'Banana', sweetness: 7, bones: false }
giveFruit(myFruits)
```

Функция `giveFruit()` имеет единственный параметр, который требует, чтобы переданный объект имел свойство с именем `name` типа `string`. Обратите внимание, что наш объект на самом деле имеет больше свойств, чем требуется, но компилятор только проверяет, присутствуют ли хотя бы те, которые необходимы, и соответствуют требуемым типам.

Напишем тот же пример, для проверки свойства _name_ с типом _string_, но при помощи интерфейсов.

[Playground Link](https://www.typescriptlang.org/play?#code/JYOwLgpgTgZghgYwgAgGJQK7DMg3gKGSORDgFsIAuZAZzClAHMAaQ4mgdwgjBAhprUQGMgCNorYslEB7PoOkyZAGwhwQ+AL758MDCARhgc5I2AA3COiw4AFDEzZq17AEo8bIgjk0VEAHTKMoy2AOQA4hYoYDLIFMihyADUyA42-qQUrlo6qjhkAJ4uYDTIALx4JORUCQBC6g2hzLRcPPIKAOzNsvLU8Mo0KNpmlsW2hcU0rkA)

```jsx
interface Fruit {
  name: string;
  sweetness: number;
  bones: boolean;
}

function giveFruit(fruit: Fruit) {
  console.log('Give to me ' + fruit.name)
}

let myFruits = { name: 'Banana', sweetness: 7, bones: false }
giveFruit(myFruits)
```

Интерфейс `Fruit` - это имя, которое мы теперь можем использовать для описания требования в предыдущем примере. Он по-прежнему представляет наличие единственного свойства с именем _name_ типа _string_. Обратите внимание, что нам не нужно было явно указывать, что объект, который мы передаем в функцию `giveFruit()`, наследует этот интерфейс, как это может быть в других языках. Здесь важен только образец. Если объект, который мы передаем функции, соответствует перечисленным требованиям, то всё позволено.

Стоит отметить, что проверка типов **не требует**, чтобы эти свойства имели какой-либо порядок, а только то, что свойства, необходимые для интерфейса, присутствуют и имеют требуемый тип.

## Необязательные свойства

Не все свойства интерфейса могут быть обязательными. Некоторые существуют при определенных условиях или могут вообще отсутствовать. Интерфейсы с необязательными свойствами записываются аналогично другим интерфейсам, где каждое необязательное свойство обозначается знаком `?` в конце имени свойства в декларации.

[Playground Link](https://www.typescriptlang.org/play?#code/JYOwLgpgTgZghgYwgAgGJQK7DMg3gKGSORDgFsIAuZAZzClAHMAaQ4mgdwgjBAhprUQGMgCNorYslEB7PoOkyZAGwhwQk4ghUyoAfiEjxUfAF98+VTlHrb1dFhwBePGylFSFagHIAQrdJvTXdaLh55BQB2YPdZeWp4ZRoIGKltZV1qAAYAD1RUAFEARgBmAFZkMwsrZDgABzrVe0xsZBcCEI9yKmRvAEEG1SC3d05uXn4FMtTiOP5qegwIMyA)

```jsx
interface Fruit {
  name: string;
  sweetness: number;
  bones: boolean;
  color?: number;
}

let banana: Fruit = {
  name: 'Banana',
  sweetness: 7,
  bones: false,
  color: 0xffe135
}

let apple: Fruit = {
  name: 'Apple',
  sweetness: 5,
  bones: true
}
```

Необязательные свойства популярны при создании шаблонов, таких как «option bags», в которых вы передаете объект в функцию, у которого заполнены только пара свойств.

## Только для чтения

Некоторые свойства могут быть заданы только для чтения, а значение они получат при создании объекта. Этого можно добиться, поместив ключевое слово _readonly_ перед именем свойства.

```jsx
interface Point {
  readonly x: number;
  readonly y: number;
}

let a1: Point = { x: 10, y: 40 }
console.log('Точка [' + a1.x + '; ' + a1.y + ']')
```

Можно создать переменную c типом `Point`, присвоив ей литерал объекта. После этого значения свойств `x` и `y` изменять будет нельзя.

## Лишние свойства

В нашем первом примере использования интерфейсов _TypeScript_ позволил передать `{ name: string; sweetness: number, bones: boolean }` там, где ожидалось всего лишь `{ name: string; }`. Также мы узнали о необязательных свойствах, и о том, как они могут быть полезны при передаче аргументов в функции. Рассмотрим пример.

```jsx
interface Fruit {
  name: string;
  sweetness?: number;
  bones?: boolean;
  color?: number;
}

function addFruit(x: Fruit): { name: string, color: number } {
  // ...
}

let banana = addFruit({ name: 'banana', colour: 0xffe135 })
// error: 'colour' not expected in type 'Fruit'
```

Обратите внимание, что аргумент, передаваемый в `addFruit()`, записан как `colour` вместо `color`. В чистом _JavaScript_ подобные вещи не выдают ошибок, но и не работают так, как хотел бы разработчик.

Можно сказать, что данная программа корректна с точки зрения типов, так как типы свойств `sweetness` совместимы, `color` отсутствует, а наличие дополнительного свойства `colour` не имеет никакого значения.

Однако _TypeScript_ делает предположение, что в этом куске кода есть ошибка. Литералы объектов обрабатываются им по-особенному, и проходят _проверку на наличие лишних свойств_. Эта проверка делается, когда литералы либо присваиваются другим переменным, либо передаются в качестве аргументов. Если в литерале есть какие-либо свойства, которых нет в целевом типе, то это будет считаться ошибкой.

Обойти такую ошибку можно несколькими способами. **Первый** из которых - это использование приведение типов:

[Playground Link](https://www.typescriptlang.org/play?#code/JYOwLgpgTgZghgYwgAgGJQK7DMg3gKGSORDgFsIAuZAZzClAHMAaQ4mgdwgjBAhpoB+aiAxkARtFbFk4gPZ8h1eXIA2EOCGnEEauVGEkxkqPgC++fDAwgEYYAuRwAJs-RYwACgAe1d9gBKalwScipaeiZmZF1VfRFjaDM8NiIAejTkADoc80t1HHFNYuQAXidXfy8Q0gpqAHIi0lJ66Ni5DChqAAZvVFQAUQBGAGYAVmRkuBo0TECgA)

```jsx
let banana = addFruit({ name: 'banana', colour: 0xFFE135 } as Fruit)
```

**Второй способ** - добавление строкового индекса, его лучше использовать тогда, когда вы уверены, что объект может иметь дополнительные свойства.

[Playground Link](https://www.typescriptlang.org/play?#code/JYOwLgpgTgZghgYwgAgGJQK7DMg3gKGSORDgFsIAuZAZzClAHMBuQ4hAewBsOoB+aiAxkARtFbFkAbQAOUDjIBy5KrXpMAutTggAnqwC++fDAwgEYYBxDI4AEzvosYABQAPak+wBKarhIq1HQMIIwANMicPFCCwmJQBnhsRAD0KcgAdFn4RvhcEDgiOsXIALy2Dl6u-qQU1ADkRaSk9RFRHBgxyAAMbqioAKIAjADMAKzIBt5AA)

```jsx
interface Fruit {
  name: string;
  color?: number;
  [propName: string]: any;
}
```

В данном примере интерфейс `Fruit` может иметь любое количество свойств. Если это не `name` или `color`, то тип свойства _не имеет значения_.

**Третий способ** - присвоить объект другой переменной. Из-за присваивания объекта другой переменной он не будет проходить проверку на избыточные свойства, компилятор не выдаст ошибки.

[Playground Link](https://www.typescriptlang.org/play?#code/JYOwLgpgTgZghgYwgAgGJQK7DMg3gKGSORDgFsIAuZAZzClAHMAaQ4mgdwgjBAhpoB+aiAxkARtFbFk4gPZ8h1eXIA2EOCGnEEauVGEkxkqPgC++fDAwgEYYAuRwAJs-RYwACgAe1d9gBKalwScipaeiZmZF1VfRFjaDM8NiIAejTkADoc80t1HDkAB3sFGmQAXjxQimoAcnFNJrro2LkMKGoABm9UVABRAEYAZgBWZDNtIkbSUkqnV38vYtKQGgCgA)

```jsx
let options = { name: 'banana', colour: 0xffe135 },
  banana = addFruit(options)
```

Стоит иметь ввиду, что для простого кода не стоит обходить данные проверки свойств. Для более сложных литералов объектов, которые содержат в себе методы, параметры состояния и др., стоит держать в памяти данные способы обхода проверок, но все же большинство ошибок, связанных с проверкой лишних свойств, как правило, на самом деле являются ошибками. Если у вас возникает такая ошибка, возможно стоит пересмотреть объявление типа.

## Типы функций

Помимо описания свойств, интерфейсы также позволяют описывать типы функций.

Для описания типа функции в интерфейсе, в нем нужно определить сигнатуру вызова. Это похоже на объявление функции только со списком параметров и типом возвращаемого значения. Каждый параметр в списке должен иметь имя и тип.

```jsx
interface SearchFunc {
  (source: string, subString: string): boolean;
}
```

Определив такой интерфейс один раз, мы можем его использовать также как и все другие интерфейсы. Пример ниже показывает, как определить переменную с типом функции и присвоить ей значение.

[Playground Link](https://www.typescriptlang.org/play?#code/JYOwLgpgTgZghgYwgAgMoTlBALAYgVxAWQG8AoZS5ACgGcB7fLCALmVrClAHMAad-ACNUnHmw5cQ3AJRtB9egBsMIANxkAvmTLKwyALYBPdJhxsTWPIQTqyRizmQBeZDGthg9EHUbNxoqX5aIRFJbn8w6VIKKl1kKAhgxT0XBiYkADpaDEs6EICZdSpkYBgaBKSUlwBaAEYo8mLihLAmEFc4RWyiqi1iiC6URqbKFrbkTnwIHsotLTIELwZlDMV6bmp7HJxqAHJBOBBDuGRFYH0UOAAHK+Vd-n3jo93paSA)

```jsx
let mySearch: SearchFunc
mySearch = function (source: string, subString: string) {
  let result = source.search(subString)
  if (result == -1) {
    return false
  } else {
    return true
  }
}
```

Имена параметров не обязательно должны совпадать, чтобы функция прошла проверку на соответствие типов. Мы, к примеру, могли бы записать предыдущий пример — вот так:

[Playground Link](https://www.typescriptlang.org/play?#code/JYOwLgpgTgZghgYwgAgMoTlBALAYgVxAWQG8AoZS5ACgGcB7fLCALmVrClAHMAad-ACNUnHmw5cQ3AJRtB9egBsMIANxkAvmTLKwyALYBPdJhxsTWPIQTqyRizmQBeZDGthg9EHSzjRU-lohP0kZOQVlOBBSCipdZCgIIMU9F1osADpaDEs6IWl1KmRgGBpE5NSXAFoARmkYoqLEsCZo+EVswqotIogOlHJGqmbW5E58CC7KLS0yBC8GZQzFem5qexycagByQSj95EVgfRQ4AAcz5W3+Xf2QOG3paSA)

```jsx
let mySearch: SearchFunc
mySearch = function (src: string, sub: string): boolean {
  let result = src.search(sub)
  if (result == -1) {
    return false
  } else {
    return true
  }
}
```

Параметры функций проверяются друг за другом, и типы параметров, находящихся на соответствующих позициях, сравниваются попарно. Если вы не хотите указывать типы для аргументов, то TypeScript сможет вывести типы из контекста, основываясь на том, что функция присваивается переменной, тип которой — SearchFunc. В следующем примере тип возвращаемого значения функции тоже выводится: это делается на основании значений, которые она возвращает (false и true). Если бы функция возвращала числа или строки, то компилятор во время проверки типов предупредил бы, что тип возвращаемого значения не совпадает с типом, указанным в интерфейсе SearchFunc.

[Playground Link](https://www.typescriptlang.org/play?#code/JYOwLgpgTgZghgYwgAgMoTlBALAYgVxAWQG8AoZS5ACgGcB7fLCALmVrClAHMAad-ACNUnHmw5cQ3AJRtB9egBsMIANxkAvmTLKwyALYBPdJhxsTWPIQTajFnMgC8yGNbDB6IOln60h00goqXWQoCD9FPWdaLAA6WgxLOn8gymAYGjCIqOcAWgBGAPIqEtCIMCYQFzhFBNTkLRKIWpRi0sowiqgqznwIeq0tMgRPBmVYxXpuajtEnGoAckE4EBW4ZEVgfRQ4AAdd5QX+JbXVhelpIA)

```jsx
let mySearch: SearchFunc
mySearch = function (src, sub) {
  let result = src.search(sub)
  if (result == -1) {
    return false
  } else {
    return true
  }
}
```

## Индексируемые типы

Аналогично тому, как мы можем использовать интерфейсы для описания типов функций, мы также можем описывать типы, в которые мы можем _«индексировать»_, например, `a[10]` или `ageMap["daniel"]`. Индексируемые типы имеют сигнатуру индекса, которая описывает типы, которые мы можем использовать для индексации объекта, вместе с соответствующими типами возврата при индексации. Давайте посмотрим на пример:

[Playground Link](https://www.typescriptlang.org/play?#code/JYOwLgpgTgZghgYwgAgMpiqA5gQSlOAT2QG8AoZZAbVABMIAPALmRAFcBbAI2gF0WAzhmwBuMgF8yZADYQwyDoTwFCLdJhC58RMYuVFkAXmoAiAEIB7LiYA0yEwDEoEWid5iZchYXWDhmo299QioABncpBAsQAQtZADppCywACj1tEPCASiA)

```jsx
interface StringArray {
  [index: number]: string;
}

let myArray: StringArray
myArray = ['Bob', 'Fred']

let myStr: string = myArray[0]
```

Здесь у нас есть интерфейс `StringArray`, у которого есть сигнатура индекса. Эта сигнатура говорит о том, что, когда `StringArray` индексируется _числом_, возвращается _строка_.

## Типы классов

В _TypeScript_ также возможно одно из наиболее распространенных применений интерфейсов в таких языках, как _C#_ и _Java_, - явное принудительное принудительное соблюдение классом определенного контракта.

```jsx
interface ClockInterface {
  currentTime: Date; // переменные
  setTime(d: Date): void; // методы
}

class Clock implements ClockInterface {
  currentTime: Date = new Date()
  setTime(d: Date) {
    this.currentTime = d
  }
  constructor(h: number, m: number) {}
}
```

### Статические и экземплярные классы

При работе с классами и интерфейсами полезно помнить, что класс имеет два типа: _статические_ и _экземпларные_. Вы можете заметить, что если вы создаете интерфейс с сигнатурой конструктора и пытаетесь создать класс, реализующий этот интерфейс, вы получаете ошибку:

[Playground Link](https://www.typescriptlang.org/play?#code/JYOwLgpgTgZghgYwgAgMIBsD2CDWrMgDOYUArgmJlMgN4BQyjyIEA7sgBQAWmpUAXM1IBbAEbQANMmGhSkQSBHioASgDcdAL506CdHEKE0WXMmDCADugjCI4Ixmx4CxMhSq0GTAPTfkAUSgoKi9GBD4oOzAAFXMIQQAROEgNJmQEFxJySihuBSVJaXyxaBVabU0gA)

```jsx
interface ClockConstructor {
    new (hour: number, minute: number);
}

class Clock implements ClockConstructor {
    // Error
    currentTime: Date;
    constructor(h: number, m: number) {}
}
```

Это потому, что, когда класс реализует интерфейс, проверяется только сторона экземпляра класса. Поскольку конструктор находится в статической стороне, он не включен в эту проверку.

Вместо этого вам нужно будет работать непосредственно со статической стороной класса. В следующем примере мы определяем два интерфейса: `ClockConstructor` для конструктора и `ClockInterface` для методов экземпляра. Затем для удобства мы определяем функцию конструктора `createClock`, которая создает экземпляры типа, который передается ей:

[Playground Link](https://www.typescriptlang.org/play?#code/JYOwLgpgTgZghgYwgAgMIBsD2CDWrMgDOYUArgmJlMgN4BQyjyIEA7sgBQAWmpUAXM1IBbAEbQANMmGhSkQSBHioASkEZsOAJLho8JAG46AXzp1QkWIhQbcOy-pT0myMMFwc1yAG6ZgAEyNTOhhSEApgAmQEKAg4SFscDgYmCip1LFx8IhJySigJFMYePgUlSSLpWXkhMWg6L0T7PWtaStiwPhBmNmj87l4CqsVIFSCzBHQ4QkJkABFgAHNgMDh0RORgYQAHdAhhCHBZpt0rJDaXBAJiMjSobjK6oeFH5RVaUxc3D3fnF1Trpg9gA6LCLDgAInEEG2yGh2whY0qpmCk2mswAgiA1phFhstrt9ocwMdMtpTo4LgCcrd+lxXpJpAzVB9Kt8kr9KpdASCwZD2a5NIijC4UWY9mBkP4lis1sgALzRWLxCCJDgLZardZkqQARgATHqAOxIiXIODYsEKpVxBJkjhYnF4nXII1SADM+qR0s1a2B7M8dAtTv97g5QA)

```jsx
interface ClockConstructor {
  new(hour: number, minute: number): ClockInterface;
}

interface ClockInterface {
  tick(): void;
}

function createClock(ctor: ClockConstructor, hour: number, minute: number): ClockInterface {
  return new ctor(hour, minute)
}

class DigitalClock implements ClockInterface {
  constructor(h: number, m: number) {}
  tick() {
    console.log('beep beep')
  }
}

class AnalogClock implements ClockInterface {
  constructor(h: number, m: number) {}
  tick() {
    console.log('tick tock')
  }
}

let digital = createClock(DigitalClock, 12, 17)
let analog = createClock(AnalogClock, 7, 32)
```

Поскольку первый параметр `createClock` имеет тип `ClockConstructor`, в createClock _(AnalogClock, 7, 32)_ он проверяет, имеет ли `AnalogClock` правильную сигнатуру конструктора.

## Расширение интерфейсов

Как и классы, интерфейсы могут расширять друг друга. Это позволяет вам копировать элементы одного интерфейса в другой, что дает вам больше гибкости в том, как вы разделяете свои интерфейсы на повторно используемые компоненты.

[Playground Link](https://www.typescriptlang.org/play?#code/JYOwLgpgTgZghgYwgAgMoAs4AcUG8BQyRyCA9gDalQBcyAzmFKAOYDc+AvvvqJLIigAKEEKkakA1nkLEcIAOrAAJmHS0QAVwC2AI2jsu+APRHkgHhBAvCCA+EEBsIIFYQQIIggIRBATCB2L1u8kACIIAYQB4ASIIAcIN7uQXY84NDwSGgAjhpwUCgQAB6QIEp0aJg4ADTIwqLiUsgExPTKEAAyIsyq6tp6UAbc5BBg9AlJKAC8ZRzIcNmo3cnsdGMQAHRklFDI-QBEOuQaEEsTU9N0VbUg9eiLyACMAAxbicnTcooqR-0ArNMXQA)

```jsx
interface Shape {
    color: string;
}

interface PenStroke {
    penWidth: number;
}

// множественное расширение
interface Square extends Shape, PenStroke {
    sideLength: number;
}

let square = {} as Square;
square.color = "blue";
square.sideLength = 10;
square.penWidth = 5.0;
```

## Гибридные типы

Как мы упоминали ранее, интерфейсы могут описывать более сложные типы, присутствующие в реальном мире _JavaScript_. Из-за динамического и гибкого характера _JavaScript_ вы можете случайно встретить объект, который работает как комбинация некоторых типов, описанных выше.

Одним из таких примеров является объект, который действует как функция и объект с дополнительными свойствами:

[Playground Link](https://www.typescriptlang.org/play?#code/JYOwLgpgTgZghgYwgAgMIHsCu5rIN4BQyxyAFAM5hxRgBcyImAtgEbQCU9lUoA5gNxESoSFABucADb1GraIJLIoEchDClOyMemAATQQF8CBGNgRhg6EMl5qM2URvr2cUfEOKS1yBFlfIAXmRTEHNLawoqGhlmNih2fANkOHI0P1EFEl8HaAA6EWgJSUDkAEYAJgBmTOJs11zlVTASkLCrMgS8AxqlNUwoazqMgiMCL2aEEtswF0d2QQRSUoAGeYIEBpU1DQX81yKSgFZc5f4gA)

```jsx
interface Counter {
    (start: number): string;
    interval: number;
    reset(): void;
}

function getCounter(): Counter {
    let counter = function (start: number) {} as Counter;
    counter.interval = 123;
    counter.reset = function () {};
    return counter;
}

let c = getCounter();
c(10);
c.reset();
c.interval = 5.0;
```

## Расширение классов интерфейсами

Когда тип интерфейса расширяет тип класса, он наследует переменные класса, но не их реализации. Это как если бы интерфейс объявил всех переменных класса без предоставления реализации. Интерфейсы наследуют даже _private_ и _protected_ переменные базового класса. Это означает, что, когда вы создаете интерфейс, который расширяет класс _private_ или _protected_ полями, этот тип интерфейса может быть реализован только этим классом или его подклассом.

Это полезно, когда у вас большая иерархия наследования, но вы хотите указать, что ваш код работает только с подклассами, которые имеют определенные свойства. Подклассы не должны быть связаны, кроме наследования от базового класса. Например:

[Playground Link](https://www.typescriptlang.org/play?#code/MYGwhgzhAEDCD2A7ALgJ3iaBvAUNf0ADqgJYBuYyAptBMpVQFzRiICeA3DgL444koqqAGZhgNAMpUQVYPQBGMhCnSYqAD2qIAJjGVoM2PAQjTZyABQBKZmXgltXXjlCQYAIQCuyZEmgatXTgkA0wSAFtCGXCqFBgpGTkwRSp9VSMCWjM5a2xeZ1coaAAVAPd4dX9NWKC0w1xM00TLKzyePkKYAElwsABzVJD0iKiqGLjoBPNkpSH6nAB6BbhwIoByHv7BlQw16AFgeFRUcxA2fcjo2OQYAWoRMRo1qaSUupA1gDoStkIqGAAFmAyDRTIQwKgGNBtLJwJDkCQkDB4MIWERSBRqOj4H9UMhzms6AwvnxMsRyFCidRmKxOMZ8E1zLksPkgA)

```jsx
class Control {
    private state: any;
}

interface SelectableControl extends Control {
    select(): void;
}

class Button extends Control implements SelectableControl {
    select() {}
}

class TextBox extends Control {
    select() {}
}

class ImageControl implements SelectableControl {
    private state: any;
    select() {}
}
```

В приведенном выше примере `SelectableControl` содержит все члены `Control`, включая свойство `private state`. Поскольку `state` является _private_ полем, только потомки `Control` могут реализовать `SelectableControl`. Это связано с тем, что только потомки элемента `Control` будут иметь закрытый элемент, созданный в той же декларации, что является обязательным требованием для совместимости закрытых членов.

## Вопросы

Теперь мы готовы с вами изучать _TypeScript_, но для того чтобы понять на сколько вы усвоили этот урок пройдите тест в [мобильном приложении](http://onelink.to/njhc95) в нашей школы по этой теме.

![Sumerian school](/img/app.png)

## Ссылки

1. [TypeScriptLang](https://www.typescriptlang.org/docs/handbook/interfaces.html)
2. [Интерфейсы](https://metanit.com/web/typescript/3.3.php)

## Contributors ✨

Thanks goes to these wonderful people ([emoji key](https://allcontributors.org/docs/en/emoji-key)):

<table>
  <tr> 
    <td align="center"><a href="https://github.com/IIo3iTiv"><img src="https://avatars1.githubusercontent.com/u/72025062?v=4?s=200" width="200px;" alt=""/><br /><sub><b>IIo3iTiv</b></sub></a><br /><a href="https://github.com/gHashTag/react-native-village/commits?author=IIo3iTiv" title="Documentation">📖</a></td>
    <td align="center"><a href="https://fullstackserverless.github.io/"><img src="https://avatars0.githubusercontent.com/u/6774813?v=4?s=200" width="200px;" alt=""/><br /><sub><b>Dmitriy Vasilev</b></sub></a><br /><a href="#financial-gHashTag" title="Financial">💵</a></td>
  </tr>
</table>

[![Become a Patron!](/img/logo/patreon.jpg)](https://www.patreon.com/bePatron?u=31769291)
