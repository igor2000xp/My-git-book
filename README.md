---
description: 1️⃣Создание проекта React webinar 10-07-2025
---

# 1️⃣Создание проекта React webinar 10-07-2025

1️⃣Создание проекта

#### **✅ Подготовка** <a href="#ssylki" id="ssylki"></a>

1. Установить [nodejs](https://nodejs.org/en)

Команда для проверки что node установлена успешно

TerminalCopy

```bash
node -v
```

1. Установить [Webstorm ](https://www.jetbrains.com/ru-ru/webstorm/)или [VsCode](https://code.visualstudio.com/)

#### **✅ Установка и настройки** <a href="#ssylki-1" id="ssylki-1"></a>

1\) ⚡ **pnpm**

[pnpm](https://pnpm.io/) - это менеджер пакетов для JavaScript, который используется для установки и управления зависимостями в проектах. Он похож на другие популярные менеджеры пакетов, такие как `npm` и `yarn`, но отличается своей архитектурой и способом хранения зависимостей.

**Установка pnpm**

Windows

```bash
npm install -g pnpm
```

MacOS/LinuxTerminalCopy

```bash
sudo npm install -g pnpm
```

2\)⚡ Vite

[Vite ](https://vite.dev/)- это инструмент для сборки фронтенд-проектов, разработанный для быстрого запуска и разработки приложений с минимальным временем ожидания. Название "Vite" (произносится как "вит") происходит от французского слова, означающего "быстрый", что отражает основной фокус на скорости. Этот инструмент особенно популярен среди разработчиков, работающих с такими фреймворками, как Vue, React и Svelte.

2.1) Старт проекта

TerminalCopy

```bash
pnpm create vite
```

* Выберите название для проекта на ваш вкус (например, `shop`)
* Фреймворк - `React`
* Тип приложения - `TypeScript + SWC`

После создания проекта не забудьте установить зависимости, используя `pnpm i`

2.1) Запуск проекта

TerminalCopy

```
pnpm dev
```

**Итоговый результат 🚀**

![](https://safronman.gitbook.io/start-react-project/~gitbook/image?url=https%3A%2F%2Fcontent.gitbook.com%2Fcontent%2FxJIoZtsE9G7hgQDlQfPc%2Fblobs%2F8Bq3o2nIwJPCoBD4xjs4%2Fimage.png\&width=768\&dpr=4\&quality=100\&sign=ea5312fe\&sv=2)

3\) ⚡ Ставим библиотеки (понадобятся в дальнейшем).

* [**axios** ](https://www.npmjs.com/package/axios)
* [**react router**](https://www.npmjs.com/package/react-router-dom)

TerminalCopy

```bash
pnpm add axios react-router
```

4\) ⚡Замена шаблонного кода **🔗** [**Ссылка на архив с картинками и общим CSS файлом (App.css)**](https://drive.google.com/file/d/1dfxeu_8CjpXQMp4WT4muaC1wey4zccuB/view?usp=sharing)

В папке `src` замените:

* `App.css` - файл с глобальными стилями
* `assets` - директория с изображениями
* Удалите файл `index.css`
* Удалите из main.tsx не иcпользуемый импорт

Copy

```
import './index.css'
```

* App.tsx замените на следующий код

Copy

```
import './App.css'

function App() {
  return (
   <div>App</div>
  )
}

export default App
```

**Итоговый результат 🚀** ![](https://safronman.gitbook.io/start-react-project/~gitbook/image?url=https%3A%2F%2Fcontent.gitbook.com%2Fcontent%2FxJIoZtsE9G7hgQDlQfPc%2Fblobs%2F8It82RQYFQkjuks9GQ9P%2Fimage.png\&width=300\&dpr=4\&quality=100\&sign=2a09b508\&sv=2)
