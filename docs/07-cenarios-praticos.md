# Análise de Cenários Práticos de Segurança

## 1. SQL Injection

### Vulnerabilidade

O trecho abaixo apresenta uma vulnerabilidade de **SQL Injection**:

```javascript
const email = req.body.email;
const query = "SELECT * FROM usuarios WHERE email = '" + email + "'";
```

O problema ocorre porque o valor recebido do usuário é concatenado diretamente na consulta SQL.

### Risco

Um atacante poderia manipular a entrada enviada no campo de e-mail para alterar a lógica da consulta, podendo tentar burlar a autenticação ou acessar informações indevidas.

### Correção

A aplicação deve utilizar consultas parametrizadas ou **Prepared Statements**, mantendo os dados fornecidos pelo usuário separados da instrução SQL.

Exemplo conceitual:

```javascript
const query = "SELECT * FROM usuarios WHERE email = ?";
const usuario = await db.query(query, [email]);
```

Dessa forma, o valor recebido é tratado como dado e não como parte da instrução SQL.

## 2. Quebra de autorização

Um usuário comum conseguiu acessar:

`GET /admin/usuarios`

A falha é uma **quebra de controle de acesso**, pois a aplicação verificou a autenticação, mas não aplicou corretamente a autorização.

Autenticação responde "quem é o usuário?", enquanto autorização responde "o que esse usuário pode fazer?".

A proteção deve utilizar middleware que valide o JWT e, posteriormente, verifique o perfil do usuário. Uma rota administrativa deve exigir uma função autorizada, como `ADMIN`.

Caso um usuário autenticado, mas sem permissão administrativa, tente acessar a rota, o sistema deve retornar `403 Forbidden`.

## 3. Vazamento de JWT

O vazamento de um JWT válido pode permitir que outra pessoa utilize a sessão do usuário enquanto o token estiver válido.

A mitigação inclui HTTPS, armazenamento seguro no cliente, expiração dos tokens e mecanismos de revogação ou renovação quando necessários.

## 4. Senhas armazenadas em texto puro

O armazenamento de uma senha como:

```text
senha: "123456"
```

é uma vulnerabilidade grave. Um invasor que obtenha acesso ao banco consegue visualizar imediatamente a senha.

A solução é utilizar hashing apropriado, como bcrypt com salt, armazenando somente o resultado do processamento e nunca a senha original.

## 5. Conclusão dos cenários

Os incidentes analisados demonstram que a segurança depende de várias camadas. Prepared Statements protegem a comunicação com o banco, middlewares controlam o acesso às rotas, JWTs com expiração reduzem o risco de sessões comprometidas e bcrypt protege as credenciais armazenadas.

Nenhuma dessas medidas deve ser considerada isoladamente. A combinação das diferentes camadas aumenta a proteção da API e reduz os impactos de possíveis falhas.