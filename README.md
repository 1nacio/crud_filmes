# Agregador de Filmes

Aplicação de terminal em Python, orientada a objetos, integrada a um banco SQLite3. Permite cadastrar filmes, gêneros, diretores, usuários e reviews (com avaliação em estrelas).

## Requisitos

- Python 3.8 ou superior (o módulo `sqlite3` já vem com o Python; não é preciso instalar nada).

## Como executar

Na pasta do projeto, rode:

```
python main.py
```

O arquivo do banco (`filmes.db`) e as tabelas são criados automaticamente na primeira execução.

## Funcionalidades

O menu principal oferece:

1. **Cadastrar**, **Listar**, **Atualizar** e **Remover** (CRUD), sempre perguntando em qual tabela a operação será feita;
2. **Ranking de filmes por média de estrelas**;
0. **Sair da aplicação**.

As avaliações vão de 0 a 5 estrelas, aceitando meia estrela (ex.: 3.5).

## Banco de dados

| Tabela | Campos principais | Relacionamentos |
|---|---|---|
| `generos` | id, nome | — |
| `diretores` | id, nome, nacionalidade | — |
| `usuarios` | id, nome, email | — |
| `filmes` | id, titulo, ano | `genero_id` → generos, `diretor_id` → diretores |
| `reviews` | id, estrelas, comentario | `usuario_id` → usuarios, `filme_id` → filmes |

Não é possível remover um registro que ainda esteja sendo usado por outro (por exemplo, um gênero com filmes cadastrados).

## Estrutura do projeto

```
agregador_filmes/
├── main.py                # ponto de entrada
├── database/
│   └── conexao.py         # conexão com o SQLite e criação das tabelas
├── models/                # classes que representam os dados (Genero, Diretor, Usuario, Filme, Review)
├── dao/                   # acesso ao banco: todo o SQL fica aqui (inserir, listar, atualizar, deletar)
└── ui/
    ├── entrada.py         # funções de leitura e validação de entradas
    ├── menu_principal.py  # menu principal e escolha da tabela
    └── menu_*.py          # telas de cada tabela
```

Cada camada tem uma responsabilidade: `ui` conversa com o usuário, `models` guarda os dados, `dao` conversa com o banco e `database` cuida da conexão.

## Reiniciar o banco

Para começar do zero, feche o programa e apague o arquivo `filmes.db`. Ele será recriado na próxima execução.
