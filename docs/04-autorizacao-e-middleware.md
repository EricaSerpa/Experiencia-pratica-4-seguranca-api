# Autorização de Rotas e Middleware

## 1. Níveis de acesso

A API financeira deve utilizar diferentes níveis de acesso para impedir que usuários executem operações que não fazem parte de suas permissões.

| Endpoint                       | Nível de acesso | Justificativa                                                                                  |
| ------------------------------ | --------------- | ---------------------------------------------------------------------------------------------- |
| `POST /api/auth/login`         | Público         | Necessário para que o usuário envie suas credenciais e obtenha um JWT.                         |
| `POST /api/usuarios/cadastrar` | Público         | Permite o cadastro de novos usuários, utilizando validação e proteção contra abusos.           |
| `GET /api/extrato`             | Autenticado     | Contém informações financeiras privadas e deve estar disponível somente ao usuário autorizado. |
| `POST /api/transferencias`     | Autenticado     | Permite movimentação financeira e exige identificação e autorização do usuário.                |
| `GET /api/admin/painel`        | Admin           | Contém informações e funções administrativas e deve ser restrito a administradores.            |

## 2. Diferença entre autenticação e autorização

A **autenticação** verifica quem é o usuário. No projeto, essa identificação ocorre por meio das credenciais de login e posteriormente pelo JWT.

A **autorização** verifica o que o usuário pode fazer dentro da aplicação. Mesmo que o usuário esteja autenticado, ele não deve acessar recursos administrativos sem possuir a permissão necessária.

## 3. Funcionamento do middleware

O middleware funciona como uma camada de proteção entre a requisição HTTP e o controller da aplicação.

Primeiramente, verifica o header `Authorization` e identifica se existe um token no formato `Bearer <token>`. Em seguida, valida a assinatura do JWT e verifica sua validade e expiração.

Caso o token esteja ausente, inválido, adulterado ou expirado, a requisição é interrompida e a API retorna `401 Unauthorized`.

Quando o token é válido, as informações de identificação do usuário podem ser adicionadas ao objeto da requisição, por exemplo `req.user`. Em seguida, o middleware chama `next()` e permite que o processamento continue.

Em rotas administrativas, outro nível de autorização pode verificar a função do usuário, utilizando RBAC. Caso um usuário comum tente acessar uma rota administrativa, a API deve negar o acesso com `403 Forbidden`.

## 4. Benefício arquitetural

A utilização de middlewares centraliza as regras de segurança, evita repetição de código e facilita a manutenção da aplicação. Dessa forma, a autenticação e a autorização são aplicadas de maneira consistente em diferentes endpoints.