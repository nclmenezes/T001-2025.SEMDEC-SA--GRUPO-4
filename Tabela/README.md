## 1. Casos de Teste — Cadastro (Primeiro cadastro – parcial)

| ID   | Função           | Cenário                                      | Tipo    | Pré-condição                                        | Passos                                             | Resultado Esperado                           |
| ---- | ---------------- | -------------------------------------------- | ------- | --------------------------------------------------- | -------------------------------------------------- | -------------------------------------------- |
| T1.1 | Cadastro parcial | Cadastro novo com dados mínimos válidos      | Sucesso | Sem usuário com o mesmo e-mail                      | 1. Inserir usuário<br>2. Inserir credencial        | Usuário e credencial cadastrados com sucesso |
| T1.2 | Cadastro parcial | Cadastrar senha com segurança fraca          | Falha   | A senha deve ter 1 maiúscula e 1 caractere especial | 1. Tentar cadastrar senha fraca                    | Falha no CHECK `validar_senha`               |
| T1.3 | Cadastro parcial | Cadastrar e-mail já existente                | Falha   | Já existe usuário com esse e-mail                   | 1. Inserir usuário válido                          | Falha por `UNIQUE (email)`                   |
| T1.4 | Cadastro parcial | Cadastro sem nome                            | Falha   | —                                                   | 1. Inserir usuário com nome `NULL`                 | Falha por `NOT NULL (nome)`                  |
| T1.5 | Cadastro parcial | Cadastro sem data de nascimento              | Falha   | Campo obrigatório                                   | 1. Inserir usuário com data_nascimento `NULL`      | Falha por `NOT NULL (data_nascimento)`       |
| T1.6 | Cadastro parcial | Cadastro sem localização                     | Falha   | Inserir CEP ou bairro                               | 1. Inserir usuário com localização `NULL`          | Falha por `NOT NULL (localizacao)`           |
| T1.7 | Cadastro parcial | Cadastro sem gênero                          | Falha   | Campo obrigatório                                   | 1. Não informar gênero                             | Falha por `NOT NULL (genero)`                |
| T1.8 | Cadastro parcial | Cadastrar credencial com usuario_id inválido | Falha   | ID de usuário inexistente                           | 1. Inserir credencial com `usuario_id` inexistente | Falha por `FOREIGN KEY fk_usuario`           |


## 2. Casos de Teste — Atualização Cadastral

| ID   | Função      | Cenário                                                  | Tipo    | Pré-condição       | Passos                                 | Resultado Esperado                         |
| ---- | ----------- | -------------------------------------------------------- | ------- | ------------------ | -------------------------------------- | ------------------------------------------ |
| T2.1 | Atualização | Atualizar telefone, data_nascimento, gênero, localização | Sucesso | Usuário cadastrado | 1. Executar `UPDATE` com novos valores | Dados atualizados com sucesso              |
| T2.2 | Atualização | Atualizar nome e sobrenome                               | Sucesso | Usuário cadastrado | 1. `UPDATE` nome e sobrenome           | Nome e sobrenome atualizados               |
| T2.3 | Atualização | Tentar alterar e-mail                                    | Falha   | Usuário cadastrado | 1. `UPDATE` no campo e-mail            | Trigger impede a alteração e lança exceção |
| T2.4 | Atualização | Informar telefone inválido                               | Falha   | Usuário cadastrado | 1. `UPDATE` com valor inválido         | Falha por valor inválido no campo telefone |


## 3. casos de Teste — Exclusão de Cadastro

| ID   | Função   | Cenário                                           | Tipo    | Pré-condição               | Passos                                          | Resultado Esperado                                       |
| ---- | -------- | ------------------------------------------------- | ------- | -------------------------- | ----------------------------------------------- | -------------------------------------------------------- |
| T3.1 | Exclusão | Excluir usuário e credenciais (CASCADE)           | Sucesso | Usuário possui credencial  | 1. `DELETE` usuário<br>2. Verificar credenciais | Usuário excluído e credenciais removidas automaticamente |
| T3.2 | Exclusão | Tentar excluir usuário inexistente                | Neutro  | Usuário não existe         | 1. `DELETE` com ID inexistente                  | 0 linhas afetadas; nenhum efeito colateral               |
| T3.3 | Exclusão | Tentar excluir usuário com credenciais incorretas | Falha   | Usuário possui credenciais | 1. `DELETE` usuário<br>2. Verificar credenciais | Usuário não excluído por falha nas credenciais           |

## 4. Casos de Teste — Validação de Cadastro Existente (E-mail)

| ID   | Função           | Cenário                         | Tipo    | Pré-condição                  | Passos                           | Resultado Esperado |
| ---- | ---------------- | ------------------------------- | ------- | ----------------------------- | -------------------------------- | ------------------ |
| T4.1 | Validar cadastro | Verificar e-mail existente      | Sucesso | Usuário com aquele e-mail     | 1. `SELECT` filtrando por e-mail | Retorna 1 linha    |
| T4.2 | Validar cadastro | Verificar e-mail não cadastrado | Sucesso | E-mail inexistente no sistema | 1. `SELECT` filtrando por e-mail | Retorna 0 linhas   |

## 5. casos de Teste — Exibir Perfil do Usuário

| ID   | Função        | Cenário                          | Tipo    | Pré-condição                     | Passos                                        | Resultado Esperado                 |
| ---- | ------------- | -------------------------------- | ------- | -------------------------------- | --------------------------------------------- | ---------------------------------- |
| T5.1 | Exibir perfil | Buscar perfil por ID válido      | Sucesso | Usuário e credenciais existentes | 1. `SELECT` com `JOIN` usuários x credenciais | Retorna 1 linha com todos os dados |
| T5.2 | Exibir perfil | Buscar perfil por ID inexistente | Neutro  | Não existe usuário com esse ID   | 1. `SELECT` com `JOIN` filtrando por ID       | Nenhuma linha retornada            |


## 6. Casos de Teste — Alteração de Senha

| ID   | Função        | Cenário                              | Tipo    | Pré-condição                    | Passos                                   | Resultado Esperado                   |
| ---- | ------------- | ------------------------------------ | ------- | ------------------------------- | ---------------------------------------- | ------------------------------------ |
| T6.1 | Alterar senha | Alterar senha com sucesso            | Sucesso | Credencial existente            | 1. `UPDATE` senha usando `usuario_id`    | Senha atualizada com sucesso         |
| T6.2 | Alterar senha | Alterar senha de usuário inexistente | Neutro  | Não existe credencial associada | 1. `UPDATE` com `usuario_id` inexistente | 0 linhas afetadas; nenhuma alteração |
