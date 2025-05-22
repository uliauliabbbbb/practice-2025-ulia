# Веб-сервер на C#

## Описание

Этот проект реализует учебный веб-сервер на C# с поддержкой маршрутизации, контроллеров, обработки сессий, cookies и авторизации пользователей.

## Архитектура

- **HttpServer** — запускает сервер, обрабатывает подключения, маршрутизирует запросы.
- **RoutingTable** — хранит сопоставления маршрутов и методов контроллеров.
- **Controller** — базовый класс контроллеров, реализует стандартные ответы.
- **HomeController, UsersController** — реализуют обработку страниц, форм, авторизации.
- **Session, Cookies** — обеспечивают хранение пользовательских данных между запросами.

## Основные маршруты

| URL          | Метод | Контроллер      | Метод        | Назначение           |
| ------------ | ----- | --------------- | ------------ | -------------------- |
| /            | GET   | HomeController  | Index        | Главная страница     |
| /HTML        | GET   | HomeController  | Html         | HTML-форма           |
| /HTML        | POST  | HomeController  | HtmlFormPost | Обработка формы      |
| /Content     | GET   | HomeController  | Content      | Работа с файлами     |
| /Cookies     | GET   | HomeController  | Cookies      | Работа с cookies     |
| /Session     | GET   | HomeController  | Session      | Работа с сессией     |
| /Login       | GET   | UsersController | Login        | Страница входа       |
| /Login       | POST  | UsersController | LogInUser    | Обработка входа      |
| /Logout      | GET   | UsersController | Logout       | Выход                |
| /UserProfile | GET   | UsersController | GetUserData  | Профиль пользователя |

flowchart LR
Client -->|HTTP запрос| HttpServer
HttpServer --> Router
Router -->|Маршрут| Controller
Controller -->|Ответ| HttpServer
HttpServer -->|HTTP ответ| Client

## Пример запуска

await new HttpServer(routes => routes
.MapGet("/", c => c.Index())
.MapGet("/Login", c => c.Login())
.MapPost("/Login", c => c.LogInUser())
// ... другие маршруты
).Start();

## Основные маршруты

| URL          | Метод | Контроллер      | Метод        | Назначение           |
| ------------ | ----- | --------------- | ------------ | -------------------- |
| /            | GET   | HomeController  | Index        | Главная страница     |
| /HTML        | GET   | HomeController  | Html         | HTML-форма           |
| /HTML        | POST  | HomeController  | HtmlFormPost | Обработка формы      |
| /Content     | GET   | HomeController  | Content      | Работа с файлами     |
| /Cookies     | GET   | HomeController  | Cookies      | Работа с cookies     |
| /Session     | GET   | HomeController  | Session      | Работа с сессией     |
| /Login       | GET   | UsersController | Login        | Страница входа       |
| /Login       | POST  | UsersController | LogInUser    | Обработка входа      |
| /Logout      | GET   | UsersController | Logout       | Выход                |
| /UserProfile | GET   | UsersController | GetUserData  | Профиль пользователя |

## Пример запуска

await new HttpServer(routes => routes
.MapGet("/", c => c.Index())
.MapGet("/Login", c => c.Login())
.MapPost("/Login", c => c.LogInUser())
// ... другие маршруты
).Start();

## Пример контроллера

public class HomeController : Controller
{
public Response Index() => Text("Hello from the server!");
public Response Html() => View();
public Response HtmlFormPost()
{
var name = Request.Form["Name"];
var age = Request.Form["Age"];
var model = new FormViewModel() { Name = name, Age = int.Parse(age) };
return View(model);
}
}

## Пример контроллера

public class HomeController : Controller
{
public Response Index() => Text("Hello from the server!");
public Response Html() => View();
public Response HtmlFormPost()
{
var name = Request.Form["Name"];
var age = Request.Form["Age"];
var model = new FormViewModel() { Name = name, Age = int.Parse(age) };
return View(model);
}
}

## Работа с сессией и cookies

- Сессии реализованы через уникальный идентификатор, который хранится в cookies.
- При авторизации в сессию записывается идентификатор пользователя.

## Диаграмма классов

classDiagram
class Controller {
+Request Request
+Text()
+Html()
+View()
+Redirect()
}
class HomeController
class UsersController
Controller <|-- HomeController
Controller <|-- UsersController

text

## Запуск

1. Склонируйте репозиторий.
2. Откройте проект в Visual Studio.
3. Соберите и запустите проект.
4. Перейдите по адресу http://localhost:8080/
