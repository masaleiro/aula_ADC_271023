# Branches e GitHub

## Exemplo Website (04_05_Git_Basico.pdf - página 66)

- Criar um ramo/“branch” para um assunto/problema/“issue” em que estamos a trabalhar.
- Fazemos algum trabalho nesse ramo
- Nesta altura recebemos uma chamada para resolver um problema crítico
- Volto ao ramo de produção
- Crio um ramo para adicionar o hotfix
- Após testes faço o merge e envio para produção
- Volto ao ramo em que estava a trabalhar e continuo

## Clonar o repositorio git_branching_website da conta ajpinto-ualg

Abrir o VSCode e abrir num terminal GitBash executar os seguintes comandos

```bash
$ cd ~
# criar a diretoria src se não existir 
$ mkdir src
# mudar para a diretoria src  
$ cd src
# clonar o projeto 
$ git clone https://github.com/ajpinto-ualg/git_branching_website.git
# mudar para a diretoria do repositorio
$ cd git_branching_website
```

## Criar um ramo/“branch” para um assunto/problema/“issue” em que estamos a trabalhar

Cada aluno deve criar um branch com a seguinte designação issueNumAluno (exemplo: issue12645)

```bash
$ git switch -c issue12645

Switched to a new branch 'issue12645'`
```

### Editar o ficheiro index_aNumAluno.html (exemplo: index_a12645.html)

```bash
$ code index_a12645.html
```

O ficheiro deve ficar da seguinte forma:

```html
<html>
<title>Página da empresa</title>

<body>
    <h1>XPTO, SA</h1>
    <p>Informação sobre a empresa...</p>
    <p>...</p>
    <div id="footer">
        Para suporte contacte-nos através do email suport@empresa.pt.
    </div>
</body>

</html>
```

### Criar um commit para as alterações

```bash
$ git commit -a -m "Adiciona um footer na página inicial"

[issue53 f3e672d] Adiciona um footer na página inicial
 1 file changed, 3 insertions(+), 1 deletion(-)
```

```bash
$ git status

On branch issue12645
nothing to commit, working tree clean
```

## Criar um branch para corrigir um erro critico para o qual fomos alertados

Mudar para o ramo `main`. Como podem constatar o index.html tem o conteúdo.

```bash
$ git switch main

Switched to branch 'main'

$ cat index_a12645.html
```

```html
<html>
<title>Página da empresa</title>

<body>
    <h1>XPTO, SA</h1>```bash
    <p>Informação sobre a empresa...</p>
    <p>...</p>
    <p>contacto: support@empresa.pt</p>
</body>

</html>
```

Para criar um ramo novo para corrigir o erro critico, cada aluno deve criar um branch com a seguinte designação hotfixNumAluno (exemplo: hotfix12645).

```bash
$ git switch -c hotfix12645

Switched to a new branch 'hotfix12645'
```

Editar e corrigir o erro critico (no exemplo, era o email que esta errado)

```bash
$ code index_a.html
```

Corrigir o e-mail tal como indicado no código abaixo

```html
<html>
<title>Página da empresa</title>

<body>
    <h1>XPTO, SA</h1>
    <p>Informação sobre a empresa...</p>
    <p>...</p>
    <p>contacto: suporte@empresa.pt</p>
</body>

</html>
```

Criar um commit com a correção

```bash
$ git commit -a -m "Corrige o endereço de e-mail na página inicial"

[hotfix 45ed9eb] CCorrige o endereço de e-mail na página inicial
 1 file changed, 1 insertion(+), 1 deletion(-)`
```

Depois de verificar que está tudo correto, é necessário enviar as alterações para o ramo de "produção". Primeiro vamos mudar para o ramo `main`.

```bash
$ git switch main

Switched to branch 'main'
```

E depois vamos "juntar" (*merge*) o conteúdo do ramo `hotfix` para o ramo `main`

```bash
$ git merge hotfix

Updating c78b551..45ed9eb
Fast-forward
 index.html | 2 +-
 1 file changed, 1 insertion(+), 1 deletion(-)
```

Seguidamente vamos validar o nosso commit e o estado do log com o **Git Graph** ou o **git log** e vamos "empurrar" essas alterações para o nosso repositório no GitHub

```bash
$ git push
```

> NOTA: Se não conseguirem fazer o *push* para o Github é porque provavelmente a vossa cópia local esta desatualizada em relação ao github, pelo que devem correr primeiro o comando `git pull`

Agora que o erro critico já foi corrigido e já está no `main`, podemos apagar o ramo `hotfix`

```bash
$ git branch

  hotfix
  issue53
* main

$ git branch -d hotfix`

Deleted branch hotfix (was 45ed9eb).
```

## Voltar ao ramo onde estavamos a trabalhar previamente (issue12645)

Vamos então voltar ao que estavamos a fazer (o footer no ramo `issue53`)

```bash
$ git switch issue12645

Switched to branch 'issue12645'

$ code index_a12645.html
```

Continuar a editar footer...

```html
<html>
<title>Página da empresa</title>

<body>
    <h1>XPTO, SA</h1>
    <p>Informação sobre a empresa...</p>
    <p>...</p>
    <div id="footer" style="background-color: bisque;">
        Para suporte contacte-nos através do email suport@empresa.pt
    </div>
</body>

</html>
```

E fazer commit às alterações

```bash
$ git commit -a -m "Adiciona uma cor de fundo ao footer"

[issue53 b5876be] Adiciona uma cor de fundo ao footer
 1 file changed, 1 insertion(+), 1 deletion(-)
```

Agora vamos adicionar uma cor ao fundo do header

```bash
$ code index_a12645.html

```

```html
<html>
<title>Página da empresa</title>

<body>
    <h1 style="background-color:bisque;">XPTO, SA</h1>
    <p>Informação sobre a empresa...</p>
    <p>...</p>
    <div id="footer" style="background-color: bisque;">
        Para suporte contacte-nos através do email suport@empresa.pt.
    </div>
</body>

</html>
```

E fazemos commit às alterações e validamos o nosso working enviroment

```bash
$ git commit -a -m "Adiciona um fundo na linha de titulo"

[issue53 96a5d98] Adiciona um fundo da linha de titulo
 1 file changed, 1 insertion(+), 1 deletion(-)

$ git status

On branch issue12645

nothing to commit, working tree clean
```

## Fazer o *merge* das novas alterações para produção

Terminamos o trabalho do issue, vamos passar tudo para o ramo `main`. Primeiro mudar para o ramo `main`...

```bash
$ git switch main

Switched to branch 'main'
```

... e depois fazemos o *merge* do ramo `issueNumAluno` no ramo atual (`main`)

```bash
$ git merge issue12645

Auto-merging index_aindex_a12645.html
CONFLICT (content): Merge conflict in index_a12645.html
Automatic merge failed; fix conflicts and then commit the result.
```

Neste caso o git não consegue fazer o merge automaticamente, há conflitos que alguém precisa resolver antes de poder continuar com o *merge*...

```bash
$ git status

On branch main
You have unmerged paths.
  (fix conflicts and run "git commit")
  (use "git merge --abort" to abort the merge)

Unmerged paths:
  (use "git add <file>..." to mark resolution)
        both modified:   index.html

no changes added to commit (use "git add" and/or "git commit -a")
```

```bash
code index_a12645.html
```

```diff
<html>
<title>Página da empresa</title>

<body>
    <h1 style="background-color:bisque;">XPTO, SA</h1>
    <p>Informação sobre a empresa...</p>
    <p>...</p>
<<<<<<< HEAD
    <p>contacto: suporte@empresa.pt</p>
=======
    <div id="footer" style="background-color: bisque;">
        Para suporte contacte-nos através do email suport@empresa.pt.
    </div>
>>>>>>> issue53
</body>

</html>
```

Vamos corrigir o ficheiro, apagando/alterando o que está entre as linhas `<<<<<<` e `>>>>>>`

```html
<html>
<title>Página da empresa</title>

<body>
    <h1 style="background-color:bisque;">XPTO, SA</h1>
    <p>Informação sobre a empresa...</p>
    <p>...</p>
    <div id="footer" style="background-color: bisque;">
        Para suporte contacte-nos através do email suporte@empresa.pt.
    </div>
</body>

</html>
```

### ``

```bash
$ git status

On branch main
You have unmerged paths.
  (fix conflicts and run "git commit")
  (use "git merge --abort" to abort the merge)

Unmerged paths:
  (use "git add <file>..." to mark resolution)
        both modified:   index.html

no changes added to commit (use "git add" and/or "git commit -a")

$ git add index.html

$ git commit
```

Neste caso, como não utilizamos a opção `-m`, vai abrir o editor para se preencher a mensagem de commit...

```bash
hint: Waiting for your editor to close the file... unix2dos: converting file C:/Users/pmguerre/src/proj2/.git/COMMIT_EDITMSG to DOS format...
dos2unix: converting file C:/Users/ajpinto/src/git_branching_website/.git/COMMIT_EDITMSG to Unix format...
[main b0255fc] Merge branch 'issue12645'
```

A seguir fazemos validamos o nosso *working* environment e empurramos as alterações para o GitHub


```bash
$  git status

On branch main
nothing to commit, working tree clean

$ git push

Counting objects: 100% (3/3), done.
Delta compression using up to 12 threads
Compressing objects: 100% (2/2), done.
Writing objects: 100% (2/2), 242 bytes | 242.00 KiB/s, done.
Total 2 (delta 1), reused 0 (delta 0), pack-reused 0
remote: Resolving deltas: 100% (1/1), completed with 1 local object.
To https://github.com/ajpinto-ualg/git_branching_website.git
   47ac74b..933c9ee  main -> main
```

E validamos o nosso log com o Git *Graph*
