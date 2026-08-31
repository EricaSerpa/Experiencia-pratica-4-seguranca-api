# Reflexão Final

A Experiência Prática IV permitiu compreender que a segurança deve fazer parte de todo o processo de desenvolvimento de uma aplicação back-end, e não ser tratada somente como uma etapa final. Durante a atividade, foram analisadas vulnerabilidades que poderiam comprometer diretamente uma plataforma financeira, como SQL Injection, armazenamento inseguro de senhas, falhas de autorização, vazamento de tokens e ausência de mecanismos adequados de expiração.

Um dos principais aprendizados foi perceber que uma API pode funcionar corretamente do ponto de vista funcional e, mesmo assim, apresentar riscos graves de segurança. Uma vulnerabilidade pode permitir acesso indevido a dados pessoais, extratos e operações financeiras, causando prejuízos aos usuários e também à própria empresa.

A análise do fluxo de autenticação com JWT mostrou a importância de separar autenticação e autorização. A autenticação permite identificar o usuário, enquanto a autorização determina quais recursos ele pode acessar. O uso de middlewares permite centralizar essas verificações e impedir que cada endpoint tenha que implementar novamente as mesmas regras de segurança.

Também foi possível compreender a importância da proteção das credenciais. O uso de bcrypt e salt evita que senhas sejam armazenadas diretamente no banco de dados e dificulta ataques de força bruta. Da mesma forma, a utilização de tokens com expiração reduz o período de exposição quando uma credencial é comprometida.

Como oportunidade de melhoria, reconheço que ainda preciso aprofundar meus conhecimentos práticos em segurança de APIs, especialmente na implementação de autenticação, autorização, proteção de bancos de dados e testes de vulnerabilidades.

Como desenvolvedora back-end em formação, considero que esta experiência contribuiu para ampliar minha visão sobre desenvolvimento seguro. Aprendi que escrever código não significa apenas fazer uma funcionalidade funcionar, mas também pensar em quem pode acessá-la, quais dados podem ser expostos e como o sistema deve reagir diante de uma tentativa de ataque.

Concluo esta experiência com uma compreensão mais ampla de que segurança, confiabilidade e qualidade devem caminhar juntas no desenvolvimento de sistemas modernos.