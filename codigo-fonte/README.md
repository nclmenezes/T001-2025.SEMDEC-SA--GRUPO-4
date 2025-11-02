# Instruções de utilização

Para simplificar o uso do Git e manter o projeto bem modularizado, recomenda-se organizar o código por camadas/módulos de domínio. Cada integrante assume um módulo de domínio (ex.: Clientes, Funcionarios, Produtos) com responsabilidade ponta-a-ponta (rotas, controller, serviço, repositório e testes do módulo).

### Sugestões

**Estrutura de pastas**

```
src/
└─ Api/
   ├─ Controllers/        # Endpoints da API (REST)
   ├─ Application/        # Serviços/regras de negócio
   ├─ Domain/             # Entidades, DTOs e contratos
   ├─ Infrastructure/     # EF Core, repositórios, integrações
   ├─ Middlewares/        # Autenticação, logs, validações, etc.
   ├─ Mappings/           # AutoMapper/Mapster (opcional)
   ├─ Validators/         # FluentValidation (opcional)
   ├─ Program.cs          # Bootstrap (minimal hosting)
   └─ appsettings*.json   # Configurações por ambiente
tests/
└─ Api.Tests/             # Testes unitários/integração (xUnit)
```

### Divisão da força de trabalho

| Responsável | Módulo | Diretórios |
| --- | --- | --- |
| Aluno X | Cliente | Controller, Service, Repository, Tests, etc | 
| Aluno Y | Funcionário | Controller, Service, Repository, Tests, etc | 
| Aluno Z | Produtos | Controller, Service, Repository, Tests, etc | 

## Padrões e Convenções

| Padrões | Descrição | Exemplo / Sugestões |
| --- | --- | --- |
| Versionamento | `/api/v1` | use `AspNetCore.Mvc.Versioning` |
| Formato de resposta | `JSON` com envelope consistente | `{ data, error, meta }` |
| Erros | status `HTTP` corretos e corpo | `{ code, message, details }` |
| Validação | Defina as regras de validação dos `DTOs` de entrada | use `FluentValidation` |
| Autenticação / Autorização | Estabeleça responsabilidades/perfis | `JWT` e `RBAC` |
| Documentação | Documente as rotas | use `Swagger` e `OpenAPI` | 
| Migrations | Versione a evolução do banco de dados | use `EF Core Migrations` |

## Instalação da aplicação

**Execução local**

- `NET SDK 8.0` ou superior
- (Opcional) `Docker` para banco de dados

**Execução remota**

- Provedores sugeridos: `Azure App Service`, `Render`, `Railway`, `Fly.io`, ou `IIS on-premises`.
- Ambientes: dev, prod (variáveis/segredos separados).
- URL pública: [insira aqui após a publicação].

## Entregáveis do Módulo (por equipe)

- 	Rotas da API separadas por versão, para facilitar futuras atualizações sem quebrar versões antigas.. Exemplo: `/api/v1`;
- Documentação atualizada da API, mostrando como usar cada função e exemplos dos dados que devem ser enviados e recebidos. Exemplo `Swagger/OpenAPI`;
- Arquivos de atualização do banco de dados e, se quiser, um script para inserir dados iniciais;
- Testes que garantem que as funções mais importantes do módulo estão funcionando corretamente;
- Instruções explicando como preparar o ambiente, rodar o projeto e colocá-lo no ar.

## Histórico de versões

### [0.1.0] - DD/MM/AAAA
#### Adicionado/Atualizado/Removido
- Relação de artefatos ...
