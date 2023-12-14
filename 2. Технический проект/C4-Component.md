```plantuml
!include https://raw.githubusercontent.com/plantuml-stdlib/C4-PlantUML/master/C4_Component.puml

title Component

Container(WebApp, "Расширение для браузера", "React", "Позволяет пользователям сохранять ресурсы и управлять ими")

ContainerDb(DataBase1, "База данных 1", "DB", "PostqreSQL")
ContainerDb(DataBase2, "База данных 2", "DB", "Neo4j")

System_Ext(ExtApp, "Визуальное отображение новых типов узлов", "Дополнение к расширению для отображения нового типа узлов")
System_Ext(ExtApi, "Внешний API хранящий новый тип узлов", "Внешний API, в котором будет бизнес-логика по работе с новыми типами узлов")

Container(ApplicationApi, "Сервис API", "C#", "Принимает запросы из веб-приложения и вызывает нужные операции")

System_Boundary(IntegrationApi, "Сервис API для интеграции") {
	Component(IntegrationAccess, "Контроллер предоставления доступа к внешним узлам", "C#", "Вызывает методы основного сервиса предоставления доступа")
	Component(IntegrationFileSystem, "Контроллер иерархической структуры для работы с внешними узлами", "C#", "Вызывает методы основной файловой системы")
}

System_Boundary(AuthService, "Сервис аутентификации") {
	Component(AuthController, "Контроллер сервиса аутентификации", "C#", "Производит аутентификацию пользователей")
	Component(Auth, "Сервис с бизнес-логикой аутентификации", "C#", "Реализует бизнес-логику аутентификации")
	Component(AuthRepository, "Модуль работы с базой данных", "C#", "Реализует логику работы с базой данных")
	Component(Tokens, "Сервис токенов", "C#", "Генерирует токены для аутентификации пользователей")
}

System_Boundary(FileSystemService, "Сервис иерархической структуры узлов") {
	Component(FileSystemController, "Контроллер иерархической структуры узлов", "C#", "Управляет иерархической структурой узлов")
	Component(FileSystem, "Сервис с бизнес-логикой иерархической структуры узлов", "C#", "Реализует бизнес-логику иерархической структуры узлов")
	Component(FileSystemRepository, "Модуль работы с базой данных", "С#", "Реализует логику работы с базой данных")
}

System_Boundary(AccessService, "Сервис предоставления доступа") {
	Component(AccessController, "Контроллер предоставления доступа", "C#", "Управляет доступами аккаунта к ресурсам")
	Component(Access, "Сервис с бизнес-логикой предоставления доступа", "C#", "Реализует бизнес-логику предоставления доступа")
	Component(AccessRepository, "Модуль работы с базой данных", "C#", "Реализует логику работы с базой данных")
}

System_Boundary(LinksService, "Сервис управления ссылками") {
	Component(LinksController, "Контроллер управления ссылками", "C#", "Управляет ссылками")
    'Component(Links, "Сервис с бизнес-логикой управления ссылками", "C#", "")
    'Component(LinksRepository, "", "C#")
}

System_Boundary(FolderService, "Сервис управления папками") {
	Component(FolderController, "Контроллер управления папками", "C#", "Управляет папками")
    Component(Folder, "Сервис с бизнес-логикой управления папками", "C#", "Реализует бизнес-логику управления папками")
    'Component(FolderRepository, "", "C#")
}

System_Boundary(ProxyService, "Сервис интеграции") {
    Component(ProxyController, "Контроллер интеграции", "C#", "Перенаправляет запросы на другие сервисы, для расширения функциональности")
}

Rel_Right(WebApp, ExtApp, "Отображает новый тип узлов")
Rel(WebApp, ApplicationApi, "Выполняет запросы к")

'Аутентификация
Rel(ApplicationApi, AuthController, "Направляет запросы на нужный сервис")
Rel(AuthController, Auth, "Вызывает методы")
Rel(AuthController, Tokens, "Запросы на генерацию")
Rel(Auth, AuthRepository, "Обращается к базе данных")
Rel(AuthRepository, DataBase1, "Читает и записывает данные")

'Иерархическая структура узлов
Rel(ApplicationApi, FileSystemController, "Направляет запросы на нужный сервис")
Rel(FileSystemController, FileSystem, "Вызывает методы")
Rel(FileSystem, FileSystemRepository, "Обращается к базе данных")
Rel(FileSystemRepository, DataBase2, "Читает и записывает данные")

'Сервис предоставления доступа
Rel(ApplicationApi, AccessController, "Направляет запросы на нужный сервис")
Rel(AccessController, Access, "Вызывает методы")
Rel(Access, AccessRepository, "Обращается к базе данных")
Rel(AccessRepository, DataBase1, "Читает и записывает данные")

'Сервис управления ссылками
Rel(ApplicationApi, LinksController, "Направляет запросы на нужный сервис")
'Rel(LinksController, Links, "")
'Rel(Links, LinksRepository, "")
Rel(LinksController, FileSystem, "Вызывает методы")
'Rel(LinksRepository, DataBase2, "Читает и записывает данные")

'Сервис управления папками
Rel(ApplicationApi, FolderController, "Направляет запросы на нужный сервис")
Rel(FolderController, Folder, "Вызывает методы")
'Rel(Folder, FolderRepository, "")
Rel(Folder, FileSystemRepository, "Вызывает методы")
'Rel(FolderRepository, DataBase2, "")

'Сервис интеграции
Rel(ApplicationApi, ProxyController, "Направляет запросы на нужный сервис")
Rel(ProxyController, ExtApi, "Перенаправляет запросы на внешний API")

Rel(ExtApi, IntegrationAccess, "Отправляет запросы к")
Rel(ExtApi, IntegrationFileSystem, "Отправляет запросы к")

Rel(IntegrationAccess, Access, "Вызывает методы")
Rel(IntegrationFileSystem, FileSystem, "Вызывает методы")

```
```
```