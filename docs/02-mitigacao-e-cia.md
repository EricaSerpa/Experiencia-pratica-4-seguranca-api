# Estratégias de Mitigação e Tripé CIA

## 1. Estratégias de mitigação

Após identificar as vulnerabilidades da API financeira, foram definidas medidas para reduzir os riscos e proteger os dados e as operações da aplicação.

### SQL Injection

Utilizar **Prepared Statements** ou consultas parametrizadas, evitando a concatenação direta de dados fornecidos pelo usuário nas consultas SQL. Também é importante validar as entradas recebidas pela API.

### Senhas armazenadas sem proteção

As senhas não devem ser armazenadas em texto puro. Deve ser utilizado um algoritmo de hashing apropriado, como **bcrypt**, com salt. Dessa forma, mesmo em caso de acesso indevido ao banco de dados, as senhas originais não ficam expostas diretamente.

### Falhas de autorização

Implementar **middlewares de autenticação e autorização**, verificando o usuário autenticado e seu perfil de acesso antes de permitir operações protegidas. O uso de RBAC permite separar permissões de clientes e administradores.

### Exposição de dados

Aplicar validação de entrada, controle de acesso e princípio do menor privilégio. A API deve retornar somente os dados necessários ao usuário autorizado e evitar informações sensíveis nas respostas.

### Tokens sem expiração

Os JWTs devem possuir tempo de validade definido por meio da claim `exp`. Também devem ser utilizados HTTPS, armazenamento seguro no cliente e mecanismos de revogação ou renovação quando necessários.

## 2. Aplicação do Tripé CIA

### Confidencialidade

A confidencialidade garante que informações financeiras e pessoais sejam acessadas somente por usuários autorizados. Na plataforma, isso é aplicado por meio de autenticação, autorização, HTTPS e controle de acesso aos dados.

### Integridade

A integridade garante que informações e transações não sejam alteradas de forma indevida. Prepared Statements, validação de dados, autorização das operações e controles nas transferências ajudam a impedir modificações não autorizadas.

### Disponibilidade

A disponibilidade garante que a plataforma permaneça acessível e funcionando quando necessária. Medidas como rate limiting, monitoramento, tratamento adequado de erros, backups e proteção contra ataques contribuem para manter os serviços disponíveis.

## Conclusão

A combinação das estratégias de mitigação com os princípios de Confidencialidade, Integridade e Disponibilidade permite construir uma API financeira mais segura e confiável. A segurança deve estar presente desde o desenvolvimento e ser considerada continuamente durante todo o ciclo de vida da aplicação.