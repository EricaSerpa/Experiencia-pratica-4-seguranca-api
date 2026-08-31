# Armazenamento Seguro de Credenciais

## 1. Senhas em texto puro

Senhas jamais devem ser armazenadas diretamente no banco de dados. Caso um invasor consiga acessar a base, todas as credenciais poderão ser visualizadas imediatamente, permitindo invasão de contas e possíveis fraudes.

Em uma plataforma financeira, esse problema pode gerar exposição de dados pessoais, prejuízos financeiros e danos à reputação da empresa.

## 2. Hash e criptografia

Hash e criptografia possuem objetivos diferentes.

O **hash** é uma transformação de mão única. A senha é transformada em um valor que não deve ser utilizado para recuperar a senha original.

A **criptografia**, por outro lado, foi projetada para permitir que um dado seja cifrado e posteriormente recuperado mediante uma chave apropriada.

Por isso, para armazenamento de senhas, deve ser utilizado hashing apropriado em vez de criptografia reversível.

## 3. Utilização do bcrypt

O **bcrypt** é um algoritmo desenvolvido para armazenamento seguro de senhas. Ele foi projetado para ser computacionalmente mais custoso, dificultando tentativas massivas de descoberta de senhas.

No cadastro, a senha fornecida pelo usuário é processada pelo bcrypt e somente o resultado do hash é armazenado no banco.

Durante o login, o sistema utiliza o bcrypt para verificar se a senha informada corresponde ao hash armazenado, sem precisar armazenar a senha original.

## 4. Salt

O **salt** é um valor aleatório utilizado junto à senha antes do processo de hashing. Ele faz com que duas pessoas com a mesma senha possam possuir hashes diferentes.

Isso dificulta ataques baseados em tabelas precomputadas, como rainbow tables, pois o atacante não consegue simplesmente comparar um hash obtido com uma lista de hashes previamente calculados.

## 5. Brute force

O ataque de brute force consiste em tentar diversas combinações de senhas até encontrar a correta.

O bcrypt ajuda a reduzir a eficiência desse ataque porque seu processamento é intencionalmente mais lento e possui um fator de custo configurável. Isso não elimina o risco de brute force, mas aumenta o custo computacional de cada tentativa.