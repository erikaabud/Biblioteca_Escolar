# Biblioteca Escolar — versão completa

Esta versão foi consolidada para evitar migrações parciais. O SQL e o backend estão alinhados.

## Instalação limpa (recomendado)
1. No MySQL/phpMyAdmin, execute **DataBase/biblioteca_escolar.sql**. Ele APAGA e recria somente o banco `biblioteca_escolar`.
2. Confira `backend/.env` e ajuste `DB_PASSWORD` se seu MySQL tiver senha.
3. No terminal: `cd backend`, `npm install`, `npm run dev`.
4. Abra `http://localhost:3000`.

Admin inicial: `bibliotecario@escola.com` / `123456` (ou os valores do `.env`).

## O que já está incluído
- usuários aluno/funcionário/bibliotecário; login identifica o perfil automaticamente;
- catálogo com 104 livros;
- área do aluno separada em Catálogo e Minha Biblioteca;
- empréstimos, devoluções, notificações e configurações;
- colunas de metadados (`sinopse`, `capa_url`, `open_library_id`) já no SQL;
- capas/sinopses: banco local -> Open Library -> Google Books -> fallback `Sem capa`;
- timeout de 5 s para APIs externas, evitando `Carregando capa...` infinito.

Não execute arquivos de atualização antigos: esta versão usa apenas `biblioteca_escolar.sql`.


## Metadados, capas e sinopses
A versão atual usa Google Books como fonte principal. Para uso estável, preencha `GOOGLE_BOOKS_API_KEY` em `backend/.env`. Se o Google Books não trouxer algum dado, o backend tenta Gutendex/Project Gutenberg e depois Open Library. Os dados encontrados são salvos na tabela `livros`, incluindo capa, sinopse, páginas e identificadores externos.
