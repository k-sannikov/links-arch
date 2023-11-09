```plantuml
!include https://raw.githubusercontent.com/plantuml-stdlib/C4-PlantUML/master/C4_Container.puml

title Context

Person(Customer, "Хранитель", "Работает со своим хранилищем")
Person(Guest, "Участник ресерча", "Работает в предоставленном узле")

System(App, "Система управления ресурсами", "Позволяет пользователям сохранять ресурсы и управлять ими")

System(Browser, "Браузер", "Браузер в котором пользователь ведет работу")

Rel(Customer, App, "Сохраняет ресурсы")
Rel(Customer, Browser, "Открывает и закрывает вкладки")

Rel(Guest, App, "Сохраняет ресурсы")
Rel(Guest, Browser, "Открывает и закрывает вкладки")

Rel(App, Browser, "Получает открытые вкладки")

```
```