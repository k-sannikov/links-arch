```plantuml
!include https://raw.githubusercontent.com/plantuml-stdlib/C4-PlantUML/master/C4_Container.puml

title Container

Person(Customer, "Хранитель", "Работает со своим хранилищем")
Person(Guest, "Участник ресерча", "Работает с предоставленным узлом")

System_Ext(WebApplication2, "Визуальное отображение новых типов узлов", "Дополнение к расширению для отображения нового типа узлов")
System_Ext(ExtApi, "Внешний API хранящий новый тип узлов", "Внешний API, в котором будет бизнес-логика по работе с новыми типами узлов")    

System_Boundary(app, "App") {
    Container(WebApplication1, "Расширение для браузера", "React", "Позволяет пользователям сохранять ресурсы и управлять ими")
    Container(ApiService, "Сервис API", "Принимает запросы из веб-приложений и вызывает нужные операции")    
    Container(IntegrationApi, "Сервис API для интеграции", "C#", "Получает запросы с внешнего сервиса и вызывает нужные операции")
    Container(Auth, "Сервис аутентификации", "C#", "Производит аутентификацию пользователей")
    Container(FileSystem, "Сервис иерархической структуры узлов", "C#", "Управляет иерархической структурой узлов")
    Container(Access, "Сервис предоставления доступа", "C#", "Управляет доступами аккаунта к ресурсам")
    Container(Links, "Сервис управления ссылками", "C#", "Управляет ссылками")
    Container(Folder, "Сервис управления папками", "C#", "Управляет папками")
    Container(Proxy, "Сервис интеграции", "C#", "Перенаправляет запросы по новым типам узлов")

    ContainerDb(DataBase1, "База данных 1", "PosqreSQL", "Хранит данные об аккаунтах и доступах")
    ContainerDb(DataBase2, "База данных 2", "Neo4j", "Хранит данные о файловой структуре, папках и ссылках")
}

Rel(Customer, WebApplication1, "Сохраняет ресурсы")
Rel(Guest, WebApplication1, "Сохраняет ресурсы")

Rel_Right(WebApplication1, WebApplication2, "Отображает новый тип узлов")
Rel(WebApplication1, ApiService, "Отправляет REST запросы с использованием https")

Rel(ApiService, Auth, "Запрашивает авторизацию")
Rel(ApiService, FileSystem, "Запрашивает и изменяет файловую структуру")
Rel(ApiService, Access, "Првоеряет и добавляет доступ аккаунта к ресурсу")
Rel(ApiService, Folder, "Запрашивает информацию о папках")
Rel(ApiService, Links, "Запрашивает информацию о ссылках")
Rel(ApiService, Proxy, "Отправляет запросы с внешних приложений")

Rel(Auth, DataBase1, "Читает и записывает данные")
Rel(Access, DataBase1, "Читает и записывает данные")

Rel(Links, DataBase2, "Читает и записывает данные")
Rel(Folder, DataBase2, "Читает и записывает данные")
Rel(FileSystem, DataBase2, "Читает и записывает данные")

Rel(Proxy, ExtApi, "Перенаправляет запросы, связанные с новыми типами узлов")

Rel_Left(IntegrationApi, ApiService, "Использует часть основных сервисов")
Rel(ExtApi, IntegrationApi, "Отправляет запросы на регистрацию нового узла")


```
```