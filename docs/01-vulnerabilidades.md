# Identificação e Impactos de Vulnerabilidades

## Experiência Prática IV — Segurança de APIs

Esta etapa apresenta a análise das principais vulnerabilidades identificadas em uma API financeira fictícia, considerando seus mecanismos de ataque, impactos e possíveis dados comprometidos.

## 1. SQL Injection

### Mecanismo de ataque

Ocorre quando a API concatena entradas do usuário diretamente em consultas SQL sem sanitização ou uso de *Prepared Statements*. O atacante envia comandos maliciosos em campos de entrada, como login, busca de extrato ou identificador de transferência. A entrada pode alterar a lógica da consulta e permitir acesso ou manipulação indevida dos dados.

### Impactos e dados comprometidos

Podem ser comprometidos dados financeiros, históricos de transações, saldos, credenciais e informações pessoais. Para os usuários, pode ocorrer exposição de informações, alteração de registros ou prejuízos financeiros. Para a empresa, há riscos à confidencialidade e integridade dos dados, além de possível indisponibilidade do sistema.

## 2. Armazenamento inseguro de senhas

### Mecanismo de ataque

A vulnerabilidade ocorre quando as credenciais são armazenadas no banco de dados sem o uso de uma função de hashing criptográfico com *salt*. Caso um atacante consiga acesso ao banco por meio de uma invasão, backup exposto ou outra falha, poderá obter as senhas diretamente.

### Impactos e dados comprometidos

Podem ser expostos senhas, e-mails, CPFs e outros dados cadastrais. Os usuários podem sofrer roubo de contas e reutilização das credenciais em outros serviços. Para a empresa, o incidente pode gerar perda de confiança, danos à reputação e consequências legais.

## 3. Acesso indevido a dados de outros usuários

### Mecanismo de ataque

Acontece quando a API utiliza identificadores de recursos sem verificar se o usuário autenticado possui permissão para acessar aquele recurso. Um usuário pode alterar um identificador presente na requisição e tentar acessar dados pertencentes a outro cliente.

### Impactos e dados comprometidos

Podem ser expostos extratos, saldos, informações de transferências e dados de perfil. Isso representa uma violação de privacidade para os usuários e uma falha grave de controle de acesso para a empresa.

## 4. Ausência de autorização em rotas administrativas

### Mecanismo de ataque

Ocorre quando rotas administrativas não possuem mecanismos que verifiquem autenticação e perfil de acesso. Um atacante pode descobrir uma rota administrativa e tentar realizar requisições diretamente contra ela sem possuir privilégios suficientes.

### Impactos e dados comprometidos

Podem ser comprometidos dados administrativos, informações de clientes, relatórios financeiros e controles de saldo. Para a empresa, o problema pode facilitar fraudes, alterações indevidas e perda do controle operacional.

## 5. Tokens JWT sem expiração adequada

### Mecanismo de ataque

A vulnerabilidade ocorre quando tokens JWT são gerados sem uma data de expiração ou possuem validade excessivamente longa. Caso um token seja roubado, o atacante poderá reutilizá-lo para acessar a conta da vítima durante um período prolongado.

### Impactos e dados comprometidos

O atacante pode acessar extratos, perfil e funcionalidades financeiras da vítima. A empresa pode enfrentar fraudes, sequestro de sessões, custos de ressarcimento e danos à confiança dos clientes.

## Conclusão da análise

As vulnerabilidades analisadas demonstram que a segurança de uma API financeira depende da combinação de autenticação, autorização, proteção de dados e validação adequada das entradas. A identificação antecipada desses riscos permite aplicar medidas preventivas e reduzir os impactos de possíveis incidentes.
