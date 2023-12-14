```plantuml
!include https://raw.githubusercontent.com/plantuml-stdlib/C4-PlantUML/master/C4_Context.puml

title Context

Person(Customer, "Хранитель", "Работает со своим хранилищем")
Person(Guest, "Участник ресерча", "Работает в предоставленном узле")

System(App, "Система управления ресурсами", "Позволяет пользователям сохранять ресурсы и управлять ими")

System_Ext(ExtApp, "Визуальное отображение новых типов узлов", "Дополнение к расширению, для отображения нового типа узлов")
System_Ext(ExtApi, "Внешний API хранящий новый тип узлов", "Внешний API, в котором будет бизнес-логика по работе с новыми типами узлов")

Rel(Customer, App, "Сохраняет ресурсы")

Rel(Guest, App, "Сохраняет ресурсы")

Rel_Right(App, ExtApp, "Отображает новый тип узлов")

Rel(App, ExtApi, "Перенаправляет запросы по новым типам узлов")
```
