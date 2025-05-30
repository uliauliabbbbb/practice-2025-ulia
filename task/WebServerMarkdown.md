\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\
# Простой веб-сервер на .NET

##  Цель проекта

Создание и исследование простой технологии веб-сервера с минимальной зависимостью от внешних библиотек, предназначенной для демонстрации базовых принципов работы HTTP-сервера на платформе .NET.

---

## Исследование предметной области

### 1. Что такое веб-сервер?
Веб-сервер — это программное обеспечение, обрабатывающее HTTP-запросы от клиентов (обычно браузеров) и возвращающее HTTP-ответы (HTML, JSON и др.).

### 2. Как устроены HTTP-запросы и ответы?
HTTP-запросы и ответы состоят из:
- стартовой строки (метод, путь, версия),
- заголовков,
- тела (опционально).

### 3. Особенности ручной реализации сервера
- Использование TCP-соединения.
- Разбор HTTP-протокола вручную.
- Маршрутизация путей.
- Асинхронная обработка клиентов.

---

## Руководство по созданию сервера

###  Необходимые инструменты

- Visual Studio 2022 / Rider
- .NET 6 SDK или выше

---

### Пошаговая инструкция

#### Шаг 1: Клонируйте репозиторий

```bash
git clone https://github.com/uliauliabbbbb/practice-2025-ulia.git
cd practice-2025-ulia/BasicWebServer-main
```

#### Шаг 2: Откройте решение `BasicWebServer.sln` в Visual Studio

#### Шаг 3: Запустите проект `BasicWebServer.Demo`

Он использует модуль `BasicWebServer.Server`, чтобы поднять веб-сервер.

#### Шаг 4: Изучите файл `StartUp.cs`

Тут создается сервер, маршруты и запускается асинхронная обработка запросов.

```csharp
var server = new HttpServer(port, routeTable);
await server.StartAsync();
```

#### Шаг 5: Добавьте свои маршруты

```csharp
routeTable.Add(HttpMethod.Get, "/", request => new TextResponse("<h1>Привет, мир!</h1>", ContentType.Html));
```

---

## Примеры кода

### Простой GET-обработчик

```csharp
routeTable.Add(HttpMethod.Get, "/time", request =>
{
    var currentTime = DateTime.Now.ToString();
    return new TextResponse($"Текущее время: {currentTime}");
});
```

### Обработка POST-запроса

```csharp
routeTable.Add(HttpMethod.Post, "/echo", request =>
{
    var body = request.Body;
    return new TextResponse($"Вы отправили: {body}");
});
```

---

## 🖼 Иллюстрации

![Диаграмма архитектуры](docs/img/architecture.png)


1. **Диаграмма архитектуры** (клиент → сервер → маршруты → ответы).
2. **Скриншот запуска проекта в Visual Studio**.
3. **Скриншот вывода в браузере (`http://localhost:5000/`)**.
4. **Схема обработки запроса** (TCP → разбор → маршрутизация → ответ).
5. **Диаграмма классов проекта** (`HttpServer`, `Route`, `Request`, `Response`).
6. **Пример POST-запроса через curl/Postman**.

*Изображения сохраняются в папку `/docs/img/` и вставляются так:*

```markdown
![Архитектура](docs/img/architecture.png)
```

---

## Структура проекта

```text
BasicWebServer-main/
│
├── BasicWebServer.Server/       # Основной сервер
├── BasicWebServer.Demo/         # Демонстрация
├── docs/img/                    # Иллюстрации
└── README.md                    # Описание проекта
```

---

## 🔚 Заключение

Этот проект позволяет понять, как устроен простой веб-сервер "изнутри", включая работу с TCP, маршрутизацией и асинхронностью. Он станет хорошей основой для дальнейшего изучения сетевого программирования и HTTP
