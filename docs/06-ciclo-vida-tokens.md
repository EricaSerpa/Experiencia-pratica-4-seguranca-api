# Ciclo de Vida e Proteção dos Tokens

## 1. Importância da expiração

Um JWT deve possuir uma validade definida por meio da claim `exp`. A expiração limita o período durante o qual um token pode ser utilizado.

Essa medida reduz o tempo de exposição caso o token seja roubado ou vazado.

## 2. Riscos de tokens sem validade

Um token sem expiração pode permanecer válido por tempo indeterminado. Se um atacante obtiver esse token, poderá utilizá-lo para acessar recursos da conta da vítima enquanto o token continuar sendo aceito pela API.

Em uma plataforma financeira, isso pode resultar em consulta indevida de extratos, alteração de dados e realização de transferências não autorizadas.

## 3. Boas práticas

A aplicação deve utilizar HTTPS em todas as comunicações e manter os tokens protegidos no lado do cliente.

Em aplicações web, uma alternativa é utilizar cookies configurados com atributos de segurança, como `HttpOnly`, `Secure` e `SameSite`, reduzindo a exposição do token a scripts e alguns tipos de ataques.

Também devem ser utilizados tempos de expiração adequados e mecanismos de renovação e revogação quando necessários.

## 4. Variáveis de ambiente

As chaves utilizadas para assinar os JWTs não devem ser colocadas diretamente no código-fonte ou publicadas no GitHub. Elas devem ser armazenadas de maneira segura, por exemplo, por meio de variáveis de ambiente ou serviços próprios de gerenciamento de segredos.

Dessa forma, informações utilizadas para proteger a autenticação permanecem separadas do código da aplicação.