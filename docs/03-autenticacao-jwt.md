# Autenticação com JSON Web Token (JWT)

## 1. Fluxo de autenticação

O JWT será utilizado para identificar usuários autenticados e permitir o acesso seguro aos endpoints protegidos da API.

### 1. Login do usuário

O usuário envia uma requisição `POST` para o endpoint de login contendo seu e-mail e senha. Os dados são enviados por meio de uma conexão HTTPS.

### 2. Verificação das credenciais

O back-end recebe os dados e procura o usuário no banco de dados. A senha informada não é comparada diretamente com uma senha armazenada em texto puro. O sistema utiliza **bcrypt** para verificar se a senha fornecida corresponde ao hash armazenado.

Se as credenciais forem inválidas, a API retorna `401 Unauthorized`.

### 3. Geração do JWT

Após a autenticação bem-sucedida, o servidor gera um JSON Web Token contendo informações necessárias para identificar o usuário, como seu ID e perfil de acesso.

O token deve possuir uma data de expiração (`exp`) e ser assinado por uma chave protegida no servidor.

### 4. Envio do token ao cliente

O servidor retorna o token ao cliente após o login. Em uma aplicação web, uma alternativa mais segura é utilizar um cookie configurado com atributos como `HttpOnly`, `Secure` e `SameSite`, reduzindo a exposição do token a scripts executados no navegador.

### 5. Requisições subsequentes

Nas próximas requisições para endpoints protegidos, o cliente envia o token de autenticação. Quando utilizado no header HTTP, o formato convencional é:

`Authorization: Bearer <token>`

A comunicação deve ocorrer utilizando HTTPS para proteger os dados durante o transporte.

### 6. Validação pelo middleware

Antes de chegar ao controller responsável pela regra de negócio, a requisição passa pelo middleware de autenticação. O middleware verifica a existência do token, valida sua assinatura e verifica sua expiração.

Se o token for válido, as informações necessárias do usuário são disponibilizadas para as próximas etapas e a requisição continua seu processamento.

Se o token estiver ausente, inválido ou expirado, o acesso é interrompido e a API retorna `401 Unauthorized`.

## 2. Estrutura do JWT

Um JSON Web Token é formado por três partes principais:

### Header

O Header identifica informações sobre o token, principalmente o tipo (`JWT`) e o algoritmo utilizado para sua assinatura.

Exemplo simplificado:

```json
{
  "alg": "HS256",
  "typ": "JWT"
}
```

### Payload

O Payload contém as informações, chamadas de claims, que serão transportadas pelo token. Essas informações não devem conter senhas ou outros dados sensíveis.

Exemplo simplificado:

```json
{
  "id": 1050,
  "email": "usuario@exemplo.com",
  "role": "CLIENTE",
  "exp": 1788000000
}
```

O Payload é codificado, mas não deve ser considerado secreto. Por isso, informações confidenciais não devem ser colocadas nele.

### Signature

A Signature é utilizada para verificar a autenticidade e integridade do token. Ela é criada a partir do Header e do Payload utilizando uma chave mantida pelo servidor.

Caso alguém altere o conteúdo do Payload, a assinatura deixará de corresponder ao token original e a validação deverá falhar.

## 3. Segurança no uso do JWT

Para aumentar a segurança, a aplicação deve utilizar HTTPS, tokens com tempo de expiração adequado, chaves de assinatura protegidas por variáveis de ambiente e mecanismos de renovação ou revogação quando necessários.

Além disso, a autenticação deve ser complementada pela autorização. Um JWT válido identifica o usuário, mas não significa que ele tenha permissão para acessar todas as funcionalidades da aplicação.