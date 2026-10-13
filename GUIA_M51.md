# M51 — Projeto independente no VS Code

Este projeto usa a M50 como base, mas tem pasta, ambiente virtual e repositório
próprios. Não copie o ZIP para a pasta da M50.

1. Extraia o ZIP em C:\Users\INSPIRON\Desktop\EBAC\EBACc\m51.
2. Abra a pasta m51-meu-blog que contém manage.py no VS Code.
3. No PowerShell, execute os comandos abaixo, um por vez:

```powershell
py -m venv .venv
.\.venv\Scripts\python.exe -m pip install -r requirements.txt
.\.venv\Scripts\python.exe manage.py migrate
.\.venv\Scripts\python.exe manage.py check
.\.venv\Scripts\python.exe -m pytest -v
.\.venv\Scripts\python.exe manage.py runserver
```

Esperado: 12 passed. Abra http://127.0.0.1:8000/post/ para ver Hello World.
A página principal continua sendo Meu Blog. A base de dados é nova: não há
usuários ou posts da M50. Caso queira usar o admin, execute createsuperuser.
Pare o servidor com Ctrl+C. Se a porta estiver ocupada, pare o servidor da M50
ou use runserver 8001 e abra http://127.0.0.1:8001/post/.

## Repositório local novo e branch views

```powershell
git init
git branch -M main
git add README.md .gitignore
git commit -m "Inicia repositório M51 Django Views"
git switch -c views
git add .
git status
git commit -m "Implementa PostView com Hello World e testes"
```

Confira o git status antes do último commit: .venv, db.sqlite3 e caches não
devem aparecer. A pasta migrations e seus arquivos devem estar incluídos.
Não execute startproject: o projeto completo está pronto no ZIP.

## GitHub

Crie um novo repositório público m51-meu-blog, sem README, gitignore ou licença.
Na pasta da M51, execute:

```powershell
git remote add origin https://github.com/mtgbcma-dotcom/m51-meu-blog.git
git push -u origin main
git push -u origin views
Start-Process "https://github.com/mtgbcma-dotcom/m51-meu-blog/compare/main...views?expand=1"
```

Confirme base main e compare views. Abra o PR com o título:
M51 — View de Post com retorno Hello World.

Descrição após testar no seu notebook:

Implementei a PostView usando a classe View do Django e o método get(), com
retorno HTTP contendo Hello World. Configurei a rota /post/ com as_view().
Utilizei a estrutura do Meu Blog como base em um projeto independente para a M51.
Incluí testes da rota, do conteúdo da resposta e do método HTTP não implementado.
Validação: manage.py check sem problemas e pytest com 12 testes aprovados.
Este Pull Request compara views com main e permanecerá aberto para avaliação.

Adicione os perfis oficiais dos tutores da EBAC como revisores, conforme os
usuários informados pelo curso. Não faça merge. Envie o link desse novo PR
na entrega da M51. Prints de Hello World e dos testes podem complementar o PR.

## Arquivos centrais da M51

- blog/views.py: PostView e a listagem do blog.
- blog/urls.py: rota /post/ e as_view().
- blog/test_views.py: 3 testes da view e rota.
- config/urls.py: inclusão das rotas do app.

Validação do pacote: Python 3.12.14, Django 5.2.18, pytest 9.1.1,
pytest-django 4.14.0; 12 testes aprovados. Repita no seu notebook.
