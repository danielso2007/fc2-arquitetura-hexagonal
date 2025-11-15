[![Node.js CI](https://github.com/danielso2007/fc2-arquitetura-hexagonal/actions/workflows/node.js.yml/badge.svg)](https://github.com/danielso2007/fc2-arquitetura-hexagonal/actions/workflows/node.js.yml)
![GitHub package version](https://img.shields.io/github/package-json/v/danielso2007/fc2-arquitetura-hexagonal.svg)
[![GitHub pull requests](https://img.shields.io/github/issues-pr-raw/danielso2007/fc2-arquitetura-hexagonal.svg)](https://github.com/danielso2007/fc2-arquitetura-hexagonal/pulls)
[![GitHub issues](https://img.shields.io/github/issues/danielso2007/fc2-arquitetura-hexagonal.svg)](https://github.com/danielso2007/fc2-arquitetura-hexagonal/issues?q=is%3Aopen+is%3Aissue)
![GitHub last commit](https://img.shields.io/github/last-commit/danielso2007/fc2-arquitetura-hexagonal.svg)
![GitHub contributors](https://img.shields.io/github/contributors/danielso2007/fc2-arquitetura-hexagonal.svg)
![GitHub top language](https://img.shields.io/github/languages/top/danielso2007/fc2-arquitetura-hexagonal.svg)
[![Conventional Commits](https://img.shields.io/badge/Conventional%20Commits-1.0.0-yellow.svg)](https://conventionalcommits.org)

# Projeto de curso Arquitetura Hexagonal

Para estudo.

### Iniciando o projeto

# Estrutura do projeto

Obs.: Para gerar essa saída, foi usado o comando: `tree -I "node_modules|dist|.git"`

```shell
.
├── adapters
│   ├── cli
│   │   ├── product.go
│   │   └── product_test.go
│   ├── db
│   │   ├── product.go
│   │   └── product_test.go
│   ├── dto
│   │   └── product.go
│   └── web
│       ├── handler
│       │   ├── error_json.go
│       │   ├── error_json_test.go
│       │   └── product.go
│       └── server
│           └── server.go
├── application
│   ├── mocks
│   │   └── application.go
│   ├── product.go
│   ├── product_service.go
│   ├── product_service_test.go
│   └── product_test.go
├── cmd
│   ├── cli.go
│   ├── http.go
│   └── root.go
├── db.sqlite
├── docker-compose.yaml
├── Dockerfile
├── go.mod
├── go.sum
├── LICENSE
├── main.go
├── package.json
└── README.md
```

# Diagrama de arquitetura

### Nível 1

![alt text](doc/arquitetura-c4-model-nivel-1.svg)

### Nível 2

![alt text](doc/arquitetura-c4-model-nivel-2.svg)

### Nível 3

![alt text](doc/arquitetura-c4-model-nivel-3.svg)

### Nível 4

![alt text](doc/arquitetura-c4-model-nivel-4.svg)

## Pontos técnicos e mapeamento:

- `interface UserRepository` = port (coloque em `application/ports` ou `domain/ports`).
- `PostgresUserRepo` = adapter/infra (`adapters/postgres`) — contém `*sql.DB` e queries.
- `RegisterUserUseCase` = application service (`application/user/usecase.go`) — injeta `UserRepository` e `EmailNotifier`.
- `UserController` = adapter de entrada (`cmd/http/handler.go`) — converte request → DTO → chama usecase.
- Testes: mock `UserRepository` e `EmailNotifier` ao testar `RegisterUserUseCase`.

