---
id: start00_2
title: Настройка рабочего окружения на MacOS
sidebar_label: Настройка MacOS
---

Данная статья поможет настроить рабочее окружение React Native на операционной системе MacOS под мобильную операционную систему iOS.

## Компоненты

Для работы понадобятся следующие компоненты: Node, Watchman, XCode и интерфейс командной строки React Native.

Для создания программного кода понадобиться редактор. Мы рекомендуем использовать `VS Code` Но можно использовать и любой другой редактор, понравившийся вам.

## Node & Watchman

[Node.js](https://nodejs.org/en/) - это среда для серверной разработки на языке `JavaScript`. Если вы уже устанавливали `Node`, то убедитесь, что это 10 версия или больше.

[Watchman](https://facebook.github.io/watchman/) - утилита для просмотра файлов с открытым исходным кодом, которая отслеживает файлы и выполняет действия при их изменении. Устанавливаем его для повышения производительности.

Устанавливать `Node` и `Watchman` рекомендуем через `Homebrew`.

[Homebrew](https://brew.sh/) - утилита командой строки в MacOS и Linux, которая позволяет устанавливать пакеты и приложения. Кратко `Homebrew` это менеджер пакетов в MacOS. После установки `Homebrew` выполните следующие команды в терминале:
```bash
brew install node
brew install watchman
```

## XCode & CocoaPods

`XCode` - это интегрированная среда разработки (IDE) программного обеспечения для платформы MacOS разработанная корпорацией Apple. Самый простой способ установки `XCode` - через [Mac App Store](https://apps.apple.com/us/app/xcode/id497799835?mt=12). Внутри `XCode` потребуется установить нужный симулятор `iOS` и инструменты командной строки.

#### Установка симулятора iOS в XCode
Установка симулятора происходит в настройках XCode, для того, чтобы в них перейти понадобится создать новый проект или открыть уже существующий, создать проект можно кнопкой `Create a new XCode project` в главном меню приложения `XCode`.
![XCode](/img/rn/00_2/03_00.png)

После создания проекта открывается основное окно для разработки.
![XCode](/img/rn/00_2/03_01.png) 

Для того, чтобы зайти в настройки приложения в верхней панели выбираем `XCode`, далее `Preferences...`

![XCode](/img/rn/00_2/03_02.png)

Откроется окно с настройками. Для установки симулятора переходим во вкладку `Components` Раскрывается список доступных симуляторов, выбрав понравившийся устанавливаем его нажав на стрелочку рядом с названием симулятора.
![XCode](/img/rn/00_2/03_03.png)

#### Установка инструментов командной строки
Для установки инструментов необходимо в настройках `XCode` перейти на вкладку `Locations`. Строка `Command Line Tools:` в раскрывающемся списке выбираем самую последнюю версию инструментов командной строки.
![XCode](/img/rn/00_2/03_04.png)

#### Установка CocoaPods
[CocoaPods](https://cocoapods.org/) - это мощное и одновременно изящное средство управления зависимостями Cocoa-библиотек, которые разработчики используют в своих iOS и MacOS проектах.

Для установки `CocoaPods` можно воспользоваться менеджером пакетов `Homebrew` показанным ранее.
```bash
brew install cocoapods
```

## Создание проекта ReactNative
Создание проекта и дальнейшая работа с проектом на React Native схожа с созданием проекта в ОС Windows 10. Для создания проекта используется встроенный интерфейс командной строки React Native `npx`. Создадим проект под названием `MyReact`. После запуска команды в терминале пойдёт процесс создания проекта, он не быстрый. 
```bash
npx react-native init MyReact
```
![XCode](/img/rn/00_2/04_00.png)

## Запуск Metro Budnler
`Metro Bundler` - это сборщик `JavaScript`, который поставляется вместе с `React Native`. `Metro` принимает файлы и параметры ввода, компилируя все файлы `JavaScript` в один файл. После его запуска мы можем увидеть в какой файл `Metro` скомпилировал `JavaScript` код, он подсвечивается зелёным.

Запуск осуществляется в терминале, перед запуском команды перейдём в директорию с нашим проектом `MyReact` и пропишем следующую команду:
```bash
npx react-native start
```
Если при запуске не обнаружились ошибки мы увидим такую картину:
![XCode](/img/rn/00_2/04_01.png)

## Запуск приложения
Терминал, в котором работает `Metro Bundler` не выключаем. Для запуска приложения открываем новый терминал. На этом шаге так же потребуется перейти в корень проекта `MyReact`. После перехода выполняем команду:
```bash
npx react-native run-ios
```
Данная команда запустит приложение проекта `MyReact` в симуляторе `iOS`. Если вы не изменяли никакие файлы в проекте, то должны увидеть приветствие от `React Native`.
![XCode](/img/rn/00_2/04_02.png)

## VS Code
Как говорилось в начале статьи подойдёт любой редактор, но мы рекомендуем использовать `VS Code`. Для установки рекомендуемого редактора можно воспользоваться указанным ранее менеджером пакетов `Homebrew`, для этого в терминале нужно прописать следующую команду:
```bash
brew cask install visual-studio-code 
```

После установки `VS Code` запускаем его. Для открытия проекта `MyReact` в главном меню находим строку `Open folder...`, по нажатию на которую откроется диалоговое окно, в котором нужно выбрать папку с нашим проектом `MyReact`.
![XCode](/img/rn/00_2/04_04.png)

После выбора проекта появится навигационная панель `Навигатор` для работы с проектом.

## Hello World
После того, как мы установили и запустили `VS Code` можно начать работу. Для этого открываем файл `App.js` в корне проекта. В этом файле описано, что будет видеть пользователь при запуске приложения. При первом запуске мы видели приветствие от `React Native`. Мы можем изменить несколько строк и при сохранении картинка на симуляторе изменится. Замените весь код в файле `App.js` на представленный ниже и сохраните файл:
```jsx
import React from 'react'
import { SafeAreaView, StyleSheet, ScrollView, View, Text, StatusBar } from 'react-native'

import {
  Header,
  LearnMoreLinks,
  Colors,
  DebugInstructions,
  ReloadInstructions
} from 'react-native/Libraries/NewAppScreen'

const App: () => React$Node = () => {
  return (
    <>
      <Text style={styles.h1}>Hello World</Text>
    </>
  )
}

const styles = StyleSheet.create({
  h1: {
    backgroundColor: '#BEFCE5',
    color: '#000',
    fontSize: 25,
    fontWeight: '700',
    padding: 20,
    textAlign: 'center'
  }
})

export default App
```
![XCode](/img/rn/00_2/04_05.png)

#### Вот так просто!

## Ссылки
1. [Node.js](https://nodejs.org/en/)
2. [Watchman](https://facebook.github.io/watchman/)
3. [Homebrew](https://brew.sh/)
4. [Map App Store -> XCode](https://apps.apple.com/us/app/xcode/id497799835?mt=12)
5. [CocoaPods](https://cocoapods.org/)
6. [Visual Studio Code](https://code.visualstudio.com)

## Contributors ✨

Thanks goes to these wonderful people ([emoji key](https://allcontributors.org/docs/en/emoji-key)):

<!-- ALL-CONTRIBUTORS-LIST:START - Do not remove or modify this section -->
<!-- prettier-ignore-start -->
<!-- markdownlint-disable -->
<table>
  <tr> 
    <td align="center"><a href="https://github.com/KoDim-React"><img src="https://avatars1.githubusercontent.com/u/72087863?v=4?s=200" width="200px;" alt=""/><br /><sub><b>Dmitiy K.</b></sub></a><br /><a href="#mentoring-KoDim-React" title="Mentoring">🧑‍🏫</a></td>
    <td align="center"><a href="https://github.com/IIo3iTiv"><img src="https://avatars1.githubusercontent.com/u/72025062?v=4?s=200" width="200px;" alt=""/><br /><sub><b>IIo3iTiv</b></sub></a><br /><a href="https://github.com/gHashTag/react-native-village/commits?author=IIo3iTiv" title="Documentation">📖</a></td>
  </tr>
</table>

<!-- markdownlint-restore -->
<!-- prettier-ignore-end -->

<!-- ALL-CONTRIBUTORS-LIST:END -->

[![Become a Patron!](/img/logo/patreon.png)](https://www.patreon.com/bePatron?u=31769291)