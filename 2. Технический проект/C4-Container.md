```plantuml
!include https://raw.githubusercontent.com/plantuml-stdlib/C4-PlantUML/master/C4_Container.puml

title Container

Person(Customer, "Хранитель", "Работает со своим хранилищем")
Person(Guest, "Участник ресерча", "Работает с предоставленным узлом")

System(Browser, "Браузер", "Браузер в котором пользователь ведет работу")

System_Ext(WebApplication2, "Дополнение (плагин)", "Позволяет расширить функциональность приложения")
System_Ext(ExtApi, "API для хранения добавленного типа узла", "Хранит новые типы узлов, которые добавляются другими программистами, предоставляет API для работы с ними")    

System_Boundary(app, "App") {
    System(WebApplication1, "Расширение для браузера", "Позволяет пользователям сохранять ресурсы и управлять ими")
    System(ApiService, "Сервис API", "Принимает запросы из веб-приложений и вызывает нужные операции")    
    System(IntegrationApi, "Сервис API для интеграции", "Получает запросы с внешнего сервиса и вызывает нужные операции")
    System(Auth, "Сервис аутентификации", "Производит аутентификацию пользователей")
    System(FileSystem, "Сервис иерархической структуры узлов", "Управляет иерархической структурой узлов")
    System(Access, "Сервис предоставления доступа", "Управляет доступами аккаунта к ресурсам")
    System(Links, "Сервис управления ссылками", "Управляет ссылками")
    System(Folder, "Сервис управления папками", "Управляет папками")
    System(Proxy, "Сервис интеграции", "Перенаправляет запросы с внешнего сервиса и вызывает нужные операции")

    ContainerDb(DataBase1, "База данных 1", "PosqreSQL", "Хранит данные об аккаунтах и доступах")
    ContainerDb(DataBase2, "База данных 2", "Neo4j", "Хранит данные о файловой структуре, папках и ссылках")
}

Rel(Customer, WebApplication1, "Сохраняет ресурсы")
Rel(Customer, WebApplication2, "Сохраняет ресурсы")
Rel(Customer, Browser, "Открывает и закрывает вкладки")

Rel(Guest, WebApplication1, "Сохраняет ресурсы")
Rel(Guest, WebApplication2, "Сохраняет ресурсы")
Rel(Guest, Browser, "Открывает и закрывает вкладки")

Rel(WebApplication1, Browser, "Читает открытые вкладки")
Rel(WebApplication1, ApiService, "Отправляет REST запросы с использованием https")
Rel(WebApplication2, ApiService, "Отправляет REST запросы с использованием https")

Rel(ExtApi, IntegrationApi, "Отправляет запросы на регистрацию нового узла")

Rel(ApiService, Auth, "Запрашивает авторизацию")
Rel(ApiService, FileSystem, "Запрашивает и изменяет файловую структуру")
Rel(ApiService, Access, "Првоеряет и добавляет доступ аккаунта к ресурсу")
Rel(ApiService, Folder, "Запрашивает информацию о папках")
Rel(ApiService, Links, "Запрашивает информацию о ссылках")
Rel(ApiService, Proxy, "Отправляет запросы с внешних приложений")

Rel(Proxy, ExtApi, "Перенаправляет запросы")

Rel(Auth, DataBase1, "Читает и записывает данные")
Rel(Access, DataBase1, "Читает и записывает данные")

Rel(Links, DataBase2, "Читает и записывает данные")
Rel(Folder, DataBase2, "Читает и записывает данные")
Rel(FileSystem, DataBase2, "Читает и записывает данные")

Rel(IntegrationApi, ApiService, "Использует часть основных сервисов")

```
```