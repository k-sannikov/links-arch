```plantuml

package "Сервис с бизнес-логикой иерархической структуры узлов" <<Node>> {
	class IFileSystemService {
		+GetNode()
		+GetChildNodes()
		+GetParentsNodes()
		+CreateNode()
		+DeleteNode()
		+EditNode()
	}
	class FileSystemService {
		-_fileSystemRepository
		-_accessService
	}
}

class IFileSystemRepository
class IAccessService
class Exception

IFileSystemService <|.. FileSystemService
FileSystemService o-- IFileSystemRepository 
FileSystemService o-- IAccessService
FileSystemService ..> Exception : throws

```
```