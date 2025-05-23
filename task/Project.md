# BasicWebServer — Учебный проект на ASP.NET Core MVC

## Исследование предметной области

### Что такое Web Server?

Веб-сервер — это приложение, принимающее HTTP-запросы и отправляющее HTTP-ответы. Он может обслуживать статический контент (HTML, CSS, JS) или динамический (через backend-логику, базы данных и т.д.).

### Почему ASP.NET Core?

- ✔ Кроссплатформенность
- ✔ Высокая производительность
- ✔ Поддержка архитектуры MVC (Model-View-Controller)
- ✔ Интеграция с Razor Pages, Blazor, REST API

---

## Создание технологии

Проект представляет собой простой сервер на ASP.NET Core MVC с возможностью:

- возврата простого текста и HTML,
- отображения Razor-страниц,
- обработки HTML-форм с передачей данных в модель.

---

## 🛠 Пошаговое руководство по созданию

### Шаг 1. Установка SDK

Скачайте и установите [.NET SDK](https://dotnet.microsoft.com/download).

### Шаг 2. Создание проекта

```bash
dotnet new mvc -n BasicWebServer
cd BasicWebServer
```

### Структура:

```plaintext
BasicWebServer/
├── Controllers/
├── Models/
├── Views/
├── Program.cs
├── Startup.cs
```

---

## 💡 Примеры кода

### Контроллер: HomeController.cs

```csharp
public class HomeController : Controller
{
    public IActionResult Content()
    {
        return Content("Простой текст", "text/plain");
    }

    public IActionResult Html()
    {
        return Content("<h1>HTML контент</h1>", "text/html");
    }

    public IActionResult HtmlFormPost() => View();

    [HttpPost]
    public IActionResult HtmlFormPost(FormViewModel model)
    {
        return Content($"Привет, {model.Name}. Тебе {model.Age} лет.");
    }
}
```

---

### Модель: FormViewModel.cs

```csharp
public class FormViewModel
{
    public string Name { get; set; }
    public int Age { get; set; }
}
```

---

### Представление Razor: HtmlFormPost.cshtml

```html
<form asp-controller="Home" asp-action="HtmlFormPost" method="post">
  <label>Имя: <input type="text" name="Name" /></label><br />
  <label>Возраст: <input type="number" name="Age" /></label><br />
  <button type="submit">Отправить</button>
</form>
```

---

## 🧭 Конфигурация маршрутов

В `Startup.cs`:

```csharp
public void Configure(IApplicationBuilder app, IWebHostEnvironment env)
{
    app.UseRouting();
    app.UseEndpoints(endpoints =>
    {
        endpoints.MapControllerRoute(
            name: "default",
            pattern: "{controller=Home}/{action=Content}/{id?}");
    });
}
```

---

## Форма и модель

1. **Форма и модель**
   ```
   [Браузер]
       ↓ (HTML Form)
   [Контроллер]
       ↓ (Model Binding)
   [Модель]
       ↓
   [HTML Ответ]
   ```

---

## 🔧 Запуск проекта

```bash
dotnet build
dotnet run
```

Откройте браузер: http://localhost:5000/Home/HtmlFormPost

---

## 📁 Рекомендуемая структура репозитория

```plaintext
BasicWebServer/
├── README.md
├── PROJECT_DESCRIPTION.md
├── Controllers/
├── Models/
├── Views/
└── Startup.cs
```
