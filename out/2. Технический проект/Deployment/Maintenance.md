```plantuml

folder "Development" {
	[Developer]
	[Code VCS]
	[DevOps]
}

folder "GitHub" {
	[Master directory]
	
	folder "GitHub Actions" {
		[Release Pipeline]
		[Deploy Pipeline]
	}
}

folder "DockerHub" {
	[Docker Registry]
}

folder "App Server" {
	[Container]
}

[Developer] -> [Code VCS] : Commit
[DevOps] --> [Deploy Pipeline] : Run
[Code VCS] --> [Master directory]
[Master directory] -> [Release Pipeline] : Run
[Release Pipeline] --> [Docker Registry] : Update image
[Deploy Pipeline] -> [Docker Registry] : fetch
[Deploy Pipeline] -> [Container] : deploy

```