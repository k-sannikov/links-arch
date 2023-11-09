```plantuml
!include https://raw.githubusercontent.com/plantuml-stdlib/C4-PlantUML/master/C4_Component.puml

title Component

System(WebApp, "Расширение для браузера")

ContainerDb(DataBase1, "База данных 1", "DB", "PostqreSQL")
ContainerDb(DataBase2, "База данных 2", "DB", "Neo4j")

System_Ext(ExtApp, "Дополнение (плагин)")
System_Ext(ExtApi, "API для хранения добавленного типа узла")

System(ApplicationApi, "Сервис API")

System_Boundary(IntegrationApi, "Сервис API для интеграции") {
	Component(IntegrationAccess, "Контроллер предоставления доступа к внешним узлам", "Вызывает методы основного сервиса предоставления доступа")
	Component(IntegrationFileSystem, "Контроллер иерархической структуры для работы с внешними узлами", "Вызывает методы основной файловой системы")
}

System_Boundary(ApiApp, "API приложения") {
	Component(AuthController, "Контроллер сервиса аутентификации", "Производит аутентификацию пользователей")
	Component(Auth, "Сервис с бизнес-логикой аутентификации", "")

	Component(FileSystemController, "Контроллер иерархической структуры узлов", "Управляет файловой структурой")
	Component(FileSystem, "Сервис с бизнес-логикой иерархической структуры узлов", "")

	Component(AccessController, "Контроллер предоставления доступа", "Управляет доступами аккаунта к ресурсам")
	Component(Access, "Сервис с бизнес-логикой предоставления доступа", "")

	Component(LinksController, "Контроллер управления ссылками", "Управляет ссылками")
    Component(Links, "Сервис с бизнес-логикой управления ссылками", "")
    
    Component(FolderController, "Контроллер управления папками", "Управляет папками")
    Component(Folder, "Сервис с бизнес-логикой управления папками", "")
    
    Component(ProxyController, "Контроллер интеграции", "Перенаправляет запросы на другие сервисы, для расширения функциональности")
}

Rel(WebApp, ApplicationApi, "Выполняет запросы к")
Rel(ExtApp, ApplicationApi, "Выполняет запросы к")

Rel(ApplicationApi, AccessController, "Направляет запросы на нужный сервис")
Rel(ApplicationApi, FileSystemController, "Направляет запросы на нужный сервис")
Rel(ApplicationApi, LinksController, "Направляет запросы на нужный сервис")
Rel(ApplicationApi, FolderController, "Направляет запросы на нужный сервис")
Rel(ApplicationApi, ProxyController, "Направляет запросы на нужный сервис")
Rel(ApplicationApi, AuthController, "Направляет запросы на нужный сервис")

Rel(AuthController, Auth, "Вызывает методы")
Rel(AccessController, Access, "Вызывает методы")
Rel(FileSystemController, FileSystem, "Вызывает методы")
Rel(LinksController, Links, "Вызывает методы")
Rel(FolderController, Folder, "Вызывает методы")

Rel(ProxyController, ExtApi, "Перенаправляет запросы на внешний API")

Rel(ExtApi, IntegrationAccess, "Отправляет запросы к")
Rel(ExtApi, IntegrationFileSystem, "Отправляет запросы к")

Rel_Up(IntegrationAccess, Access, "Вызывает методы")
Rel_Up(IntegrationFileSystem, FileSystem, "Вызывает методы")

Rel(Auth, DataBase1, "Читает и записывает данные")
Rel(Access, DataBase1, "Читает и записывает данные")
Rel(Links, DataBase2, "Читает и записывает данные")
Rel(FileSystem, DataBase2, "Читает и записывает данные")
Rel(Folder, DataBase2, "Читает и записывает данные")

```
```
```