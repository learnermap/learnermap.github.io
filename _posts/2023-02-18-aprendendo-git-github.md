---
layout: post
title: "Aprendendo Git e Github"
categories: git, github, devops
author:
- Luciano
published: true
---

O Git é um sistema de controle de versão. Com ele é possível registrar alterações e visualizar quando e porque foram realizadas no código-fonte de um projeto.

O Github é uma plataforma na web que utiliza o Git como base. Com ele é possível descentralizar o desenvolvimento de software, pois hospeda na nuvem o código-fonte versinado pelo Git. Além disso, oferece inúmeras outras ferramentas como gestão de projetos e até networking.

## O que estou aprendendo?

1. [Instalando e configurando o Git](#01-configrando-o-git)
2. [Essencial do Git](#02-essencial-do-git)
3. [Repositórios Remotos](#03-repositorios-remotos)
4. [Ramificação](#04-ramificacao)
5. [Extras](#05-extras)
6. [Configurar múltiplas contas Git no mesmo computador](#06-configurar-multiplas-contas-no-pc)

## Links úteis

- [Markdown Cheat Sheet – How to Write in Markdown with Examples](https://www.freecodecamp.org/news/markdown-cheat-sheet/)
- [Como escrever um README incrível no seu Github](https://www.alura.com.br/artigos/escrever-bom-readme)
- [Git log format string cheatsheet](https://devhints.io/git-log-format)
- [git log cheatsheet](https://devhints.io/git-log)
- [Criar um repositório](https://www.atlassian.com/br/git/tutorials/setting-up-a-repository)
- [Manual Prático de Git/Github](https://guilhermeonrails.github.io/manual-do-git-e-github/)
- [Como excluir branches locais e remotos do Git](https://www.freecodecamp.org/portuguese/news/como-excluir-branches-locais-e-remotos-do-git/)

## 01. Configurando o Git

## Instalando o Git

Em sistemas linux baseados no Debian:

```
# apt install git
```

## Configuração inicial do Git

Existem diversas configurações possíveis para o git. Inicialmente, podemos utilizar:

- Nome do usuário:

```
$ git config --global user.name 'Seu nome de Usuário'
```

- Email:

```
$ git config --global user.email 'email@email.com'
```

- Editor:

```
$ git config --global core.editor 'sublime'
```

Ao final das configurações, podemos listar os valores:

```
$ git config --list
```

## 02 - Essencial do Git

## Inicializando um repositório

- Dentro da pasta do projeto, execute o comando:

```
$ git init
```

- Uma estrutura de diretório será criada para monitorar o versionamento:

```
git-e-github-para-iniciantes/
├── .git
│   ├── branches
│   ├── COMMIT_EDITMSG
│   ├── config
│   ├── description
│   ├── HEAD
│   ├── hooks
│   ├── index
│   ├── info
│   ├── logs
│   ├── objects
│   ├── ORIG_HEAD
│   └── refs
└── Readme.md
```

## O ciclo de vida dia status de seus arquivos

- **untracked:** não marcado, acabou de ser add no repo e ainda não foi reconhecido pelo git.

```
$ touch Readme.md
$ git st

On branch master

No commits yet

Untracked files:
  (use "git add <file>..." to include in what will be committed)

	Readme.md

nothing added to commit but untracked files present (use "git add" to track)
```

- **unmodified:** add no stage, mas não foi feito o commit.

```
$ git add .
$ git st
On branch master

No commits yet

Changes to be committed:
  (use "git rm --cached <file>..." to unstage)

	new file:   Readme.md

```

- **modified:** existe no stage, porém existem alterações que devem ser enviadas para o staged.

```
$ echo "Nova linha adicionada" >> Readme.md 
$ git st
On branch master

No commits yet

Changes to be committed:
  (use "git rm --cached <file>..." to unstage)

	new file:   Readme.md

Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git checkout -- <file>..." to discard changes in working directory)

	modified:   Readme.md


```

- **staged:** alterações incluídas no staged, arquivo disponível para commit.

```
$ git add .
$ git st
On branch master

No commits yet

Changes to be committed:
  (use "git rm --cached <file>..." to unstage)

	new file:   Readme.md

```

Nesse case, para fazer o commit, execute o comando:

```
$ git ci -m 'Add Readme.md'
[master (root-commit) fef5e6e] Add Readme.md
 1 file changed, 0 insertions(+), 0 deletions(-)
 create mode 100644 Readme.md
$ git st
On branch master
nothing to commit, working tree clean
```

## Visualizando logs

- Para verificar o histório de alterações podemos utilizar:

```
$ git log
commit 39a8f346ebcbcaa6960eb41f4b9f79a1299f9d3d (HEAD -> master)
Author: learnermap <email@gmail.com>
Date:   Thu Jan 23 09:31:31 2020 -0300

    Nova linha add

commit 4abd079354ec6e3546b25a8318776543c9b84642
Author: learnermap <email@gmail.com>
Date:   Thu Jan 23 09:26:48 2020 -0300

    Commit inicial
```

- Informações adicionais no log:

```
$ git log --decorate
```

- Filtro pelo autor

```
$ git log --author="Will"
```

- Log resumido

```
$ git shortlog
```

- Somente quantidade de commits e o nome

```
$ git shortlog -sn
```

- Exibindo em forma gráfica

```
$ git log --graph
```

- Identificando alterações pela hash

```
$ git show 3621c562ca13cd41cde6334c643e8412ab6ac053
```

## Visualizando o diff

- Visualizando mudanças antes do stage.

```
$ git diff
$ echo "Nova linha adicionada 5" >> Readme.md 
learnermap@linux:~/courses/git/test$ git diff
diff --git a/Readme.md b/Readme.md
index ca6549f..0b73485 100644
--- a/Readme.md
+++ b/Readme.md
@@ -4,3 +4,5 @@ Nova linha adicionada
 Nova linha adicionada 1
 Nova linha adicionada 2
 Nova linha adicionada 3
+Nova linha adicionada 4
+Nova linha adicionada 5
```

- Exibindo somente o nome do arquivo modificado.

```
git diff --name-only
```

## Desfazendo coisas


#### Excluindo alterações antes do stage

```
$ echo "Nova linha adicionada 7" >> Readme.md 
$ git st
On branch master
Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git checkout -- <file>..." to discard changes in working directory)

	modified:   Readme.md

no changes added to commit (use "git add" and/or "git commit -a")
$ git diff
diff --git a/Readme.md b/Readme.md
index 654e88c..fba9807 100644
--- a/Readme.md
+++ b/Readme.md
@@ -7,3 +7,4 @@ Nova linha adicionada 3
 Nova linha adicionada 4
 Nova linha adicionada 5
 Nova linha adicionada 6
+Nova linha adicionada 7
```

Alteração adicionada.

```
$ git co Readme.md
$ git st
On branch master
nothing to commit, working tree clean
$ git diff
$ 
```

#### Excluindo alterações no stage

```
$ echo "Nova linha adicionada 7" >> Readme.md 
$ git st
On branch master
Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git checkout -- <file>..." to discard changes in working directory)

	modified:   Readme.md

no changes added to commit (use "git add" and/or "git commit -a")
$ git add .
$ git st
On branch master
Changes to be committed:
  (use "git reset HEAD <file>..." to unstage)

	modified:   Readme.md
```

Neste ponto, as modificações já foram enviadas para o stage.

```
$ git reset HEAD
Unstaged changes after reset:
M	Readme.md
$ git st
On branch master
Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git checkout -- <file>..." to discard changes in working directory)

	modified:   Readme.md

no changes added to commit (use "git add" and/or "git commit -a")
```

Modificações removidas do stage.

```
$ git co Readme.md
$ git st
On branch master
nothing to commit, working tree clean
$ 
```

Modificações removidas do arquivo.

#### Excluindo alterações no commit

- **soft**: remove alterações do commit, deixando no stage. 

```
$ git reset --soft 9936c23
```

- **mixed**: remove alterações do commit e stage, deixando no arquivo.

```
$ git reset --mixed 9936c23
```

- **hard**: remove todas as alterações.

```
$ git reset --hard 9936c23
```

**Importante**: 

- Sempre informar o hash do commit anterior ao que será excluído!
- Utilize o reset hard antes do push.

## 03. Repositórios Remotos

## Criando um repositório no Github

- Com uma conta ativa no Github, 

<!-- ![Github](images/github-home.png) -->

- crie e configure um novo repositório.

<!-- ![Github](images/create-new-repo.png) -->

## Criando adicionando uma chave SSH

- Gerar uma nova chave ssh (*Linux/Debian*)

```
$ ssh-keygen -t rsa -b 4096 -C "your_email@example.com"
```

- Será solicitado um nome para o arquivo id_rsa e uma passphrase:

```
> Enter passphrase (empty for no passphrase): [Type a passphrase]
> Enter same passphrase again: [Type passphrase again]
```

- Adicione a chave ssh ao ssh-agent

```
$ eval "$(ssh-agent -s)"
> Agent pid 59566
```

- Adicione a chave ssh ao Github

Copie sua chave pública e crie um novo registro de chave nas configurações do Github

<!-- ![](images/add-new-ssh-key.png)  -->

## Ligando repositório local a um remoto

- Utilize as instruções exibidas no momento da criação do repositório:

```
…or create a new repository on the command line

echo "# git-e-github-para-iniciantes" >> README.md
git init
git add README.md
git commit -m "first commit"
git remote add origin git@github.com:learnermap/git-e-github-para-iniciantes.git
git push -u origin master

…or push an existing repository from the command line

git remote add origin git@github.com:learnermap/git-e-github-para-iniciantes.git
git push -u origin master
```

> Caso deseje atualizar o nome do repositório remote utilize:

```
$ git remote set-url origin <nova-url>
```

## Enviando mudanças para um repositório remoto

- Após enviar pro stage e realizar o commit das alterações:

```
$ git push origin master
```

- Realizando o push de todos os branches.

```
$ git push --all origin
```

## Clonando repositórios remotos

- Prefira ssh por ser mais rápido.

```
$ git clone gitgit@github.com:learnermap/git-e-github-para-iniciantes.git
```

## Fazendo fork de um projeto

- Copia um projeto de terceiros.

	- Realizar um fork do projeto para sua conta do Github
	- Realizar as alterações
	- Enviar um pull-request para as alterações serem adicionadas ao projeto original.

## 04. Ramificação (Branch)

## O que é um branch e por que usar?

>*"É um ponteiro que leva a um commit."*

- Preserva o `master`
- Trabalho simultâneo
- Evita conflitos

## Criando um branch

- Criando um novo branch de nome testing.

```
$ git co -b testing
Switched to a new branch 'testing'
```

É criando um novo branch, que dará origem a uma ramificação do master

- Listar os branches existentes, identificando o atual.

```
$ git br
 master
* testing
```

- Criando um novo branch vazio.

```
$ git co --orphan empty-branch
Switched to a new branch 'empty-branch'
```

É criado um novo branch, porém com os arquivos somente no stage, sem commits.

```
$ git show
fatal: your current branch 'empty-branch' does not have any commits yet
$ git st
On branch empty-branch

No commits yet

Changes to be committed:
  (use "git rm --cached <file>..." to unstage)

	new file:   new-file.md
	new file:   Readme.md
```

Remova os arquivos no stage e o branch estará completamente vazio.

```
$ git rm -rf .
rm 'new-file.md'
rm 'Readme.md'
$ git st
On branch empty-branch

No commits yet

nothing to commit (create/copy files and use "git add" to track)

```

## Movendo e deletando branches

- Para listar e alterar entre os branches, utilize:

```
$ git br
* master
  testing
$ git co nome-do-branch
```

- Deletando um branch

```
$ git br -D new-branch 
Deleted branch new-branch (was d0985c5).
```

**Importante:** Antes de sair de um branch, realize o commit de todas as alterações.

## Renomeando branch

- Para alterar o nome do branch atual para `main`:

```
$ git branch -M main
```

## Entendendo o merge

- Mantém o histórico dos commits anteriores em todos os branches.
- Cria um commit somente para fazer a união dos branches, pode afetar a legibilidade da árvore.

## Entendendo o rebase

- Insere o novo ramo na frente do último commit da master.
- Altera o histórico, prejudicando a ordem cronológica.
- Exemplo:

```
$ git pull --rebase
```

## Merge e rebase na prática

- merge: utilizado mais em pull request, para demonstrar a união de dois branches.

```
*   4f3bc99 (HEAD -> master) Merge branch 'iss1'
|\  
| * 0d10cb7 (iss1) Add file3
* | d0e0074 Add file4
|/  
* d1cf62b Add file2
* 2203974 add file1
```

- rebase: 

```
* cfb12d7 (HEAD -> master) Add file4
* 9589576 (iss1) Add file3
* a25161a Add file2
* d66e61d Add file1
```

## 05. Extras

## Criando o `.gitignore`

- Ignorar e não *trackear* certos arquivos.
- Criar um arquivo chamado `.gitignore`.
- Dentro do arquivo, especificar os tipos ou nomes de arquivos a serem ignorados pelo git.

```
Profile
*.json
*.xls

```

- Mais em:
	- [Doc](https://git-scm.com/docs/gitignore)
	- [Template](https://github.com/github/gitignore)

## Git stash é lindo

- Guarda modificações ainda não commitadas temporariamente.

```
$ git st
On branch master
Changes to be committed:
  (use "git reset HEAD <file>..." to unstage)

	new file:   file2

$ git stash
Saved working directory and index state WIP on master: 0d184db add file1
$ git log
commit 0d184db65a59d829eaa3421615bca8182a03ffab (HEAD -> master)
Date:   Thu Jan 23 18:58:44 2020 -0300

    add file1
$ git st
On branch master
nothing to commit, working tree clean
$ git co -b iss1
Switched to a new branch 'iss1'
$ git stash apply
On branch iss1
Changes to be committed:
  (use "git reset HEAD <file>..." to unstage)

	new file:   file2

$ git st
On branch iss1
Changes to be committed:
  (use "git reset HEAD <file>..." to unstage)

	new file:   file2

$ git ci -m 'add file2'
[iss1 737c612] add file2
 1 file changed, 0 insertions(+), 0 deletions(-)
 create mode 100644 file2
$ git log
commit 737c612f1b09b5a2026d754f33d4a3191a0ab533 (HEAD -> iss1)
Date:   Thu Jan 23 19:03:14 2020 -0300

    add file2

commit 0d184db65a59d829eaa3421615bca8182a03ffab (master)
Date:   Thu Jan 23 18:58:44 2020 -0300

    add file1
$ git co master 
Switched to branch 'master'
$ git stash clear
$ git stash list
$ git log
commit 0d184db65a59d829eaa3421615bca8182a03ffab (HEAD -> master)
Date:   Thu Jan 23 18:58:44 2020 -0300

    add file1
$ git merge iss1 
Updating 0d184db..737c612
Fast-forward
 file2 | 0
 1 file changed, 0 insertions(+), 0 deletions(-)
 create mode 100644 file2
$ git log
commit 737c612f1b09b5a2026d754f33d4a3191a0ab533 (HEAD -> master, iss1)
Date:   Thu Jan 23 19:03:14 2020 -0300

    add file2

commit 0d184db65a59d829eaa3421615bca8182a03ffab
Date:   Thu Jan 23 18:58:44 2020 -0300

    add file1
$ 
```

- Lista tudo o que estiver no stash. 

```
$ git stash list
```

- Limpa tudo o que estiver no stash. 

```
$ git stash clear
```

## Alias para que te quero

- Assim como no unix, é possível criar aliases para os comandos do git.
- Alguns aliases utilizados:

```
git config --global alias.st status
git config --global alias.ci commit
git config --global alias.co checkout
git config --global alias.br branch
git config --global alias.lg log --pretty=format:"%h %ad - %s" --date=short

```

## Versionamento com tags

- Utilizado para delimitar um grupo de commits.
- Criando uma tag:

```
$ git tag -a 1.0.0 -m 'Update file1'
```

- Enviando a tag para o Github

```
$ git push origin master --tags
```

- Listando as tags:

```
$ git tag
```

No Github, será criado um pacote com o source compactado e com a tag definida no formato de release.


## Salvando sua sexta com git revert

- Utilizado para voltar no fluxo de commits, mas não perder o histórico de alterações.
- Adicionando um novo arquivo e incluindo no versionamento com commit.

```
$ touch file3
$ git st
On branch master
Untracked files:
  (use "git add <file>..." to include in what will be committed)

	file3

nothing added to commit but untracked files present (use "git add" to track)
$ git add file3 
$ git st
On branch master
Changes to be committed:
  (use "git reset HEAD <file>..." to unstage)

	new file:   file3

$ git ci -m 'add file3'
[master 77dbe03] add file3
 1 file changed, 0 insertions(+), 0 deletions(-)
 create mode 100644 file3
$ git st
On branch master
nothing to commit, working tree clean
$ git lg
77dbe03 2020-01-23 - add file3
737c612 2020-01-23 - add file2
0d184db 2020-01-23 - add file1
```

- Executando o revert do último commit

```
$ git revert 77dbe03
[master f1a5762] Revert "add file3"
 1 file changed, 0 insertions(+), 0 deletions(-)
 delete mode 100644 file3
$ git lg
f1a5762 2020-01-23 - Revert "add file3"
77dbe03 2020-01-23 - add file3
737c612 2020-01-23 - add file2
0d184db 2020-01-23 - add file1
```

- Apesar do arquivo adicionado não existir mais no diretório, o commit continua no histório.

```
$ git st
On branch master
nothing to commit, working tree clean
$ git diff
$ ll
total 12
drwxr-xr-x 3 leanermap leanermap 4096 Jan 23 19:34 ./
drwxr-xr-x 5 leanermap leanermap 4096 Jan 23 18:57 ../
-rw-r--r-- 1 leanermap leanermap    0 Jan 23 18:58 file1
-rw-r--r-- 1 leanermap leanermap    0 Jan 23 19:03 file2
drwxr-xr-x 8 leanermap leanermap 4096 Jan 23 19:35 .git/
```

## Apagando tags e branches remotos

- Apagando tag localmente

```
$ git tag -d 1.0.0 
```

- Apagando tag remotamente

```
$ git push origin :1.0.0 
```

- Apagando branch localmente

```
$ git br -d nome-da-branch
```

- Apagando branch localmente

```
$ git push origin --delete :nome-da-branch
```

# 06. Configurar múltiplas contas Git no mesmo computador

Em caso de necessitar logar com duas ou mais contas diferentes do git no mesmo computador, realize as seguintes configurações:

- Configure um arquivo `config` no diretório `~/.ssh/`:

```
$ cd ~/.ssh
$ touch config
```

- Esse arquivo deverá conter um alias para cada usuário, exemplo:

``` 
Host github.com
	HostName github.com
	User git
	IdentityFile ~/.ssh/id_ed25519_usuario-principal

```

A linha `IdentityFile` refere-se ao arquivo de chave privada. Por isso, deverá existir uma chave configurada para cada usuário existente no arquivo.

Ao configurar a chave de cada usuário, uma sugestão, é adicionar o nome do usuário como um sufixo ao nome do arquivo da chave, conforme o exemplo acima.

Desta forma, poderá ir adicionando no `config` essa configuração, na medida que necessitar criar novos usuários do git no computador, exemplo:

``` 
Host github-usuario-secundario
	HostName github.com
	User git
	IdentityFile ~/.ssh/id_ed25519_usuario-secundario

```

Na linha `Host github-usuario-secundario`, definimos o alias utilizado para aquele usuário.

Por fim, quando for criar o repositório local, a url do ssh do origin, será composta com o alias existente na variável Host, do `config`. Exemplo: 

```
$ git remote -v
origin	git@github-usuario-secundario:usuario-secundario/test.git (fetch)
...
```

> Lembrando que para o usuário principal, não é necessário configurar um alias, já que será o usuário padrão.

```
Host github.com
```

É isso.