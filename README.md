# treinamento
Esse repositório é destinado para um projeto de treinamento, afim de adquirir conhecimento na criação de sistemas web

git config

CTRL + L : limpa o terminal

criar um nome: git config --global user.name "Maikol"

criar um email: git config --global user.email maikoldepaula@gmail.com

visualizar nome e email: git config user.email 

visualizar o nome da branch padrao: git config init.defaultBranch 

alterando o nome da branch padrao para main: git config --global init.defaultBranch main

clonar repositorio: git clone (link do repositorio)

liberar comandos sem token de autentificação: git config --global credential.helper store ou cache. store é mais usado quando só vc usa o computador

local onde está armazenado as configurações: git config --global --show-origin credential.helper

ir para o diretorio das chaves: cd ~/.ssh:

listar o diretorio atual : ls 

exibir o conteudo da chave public : cat id_ed25519.pub

criando o diretorio(pasta) em um local definido: mkdir "nome da pasta" 

iniciar um repositorio git: git init

para acessar um repositorio remoto a partir de um repositorio local, usar: git remote add origin {url}

clonando uma branch especifica: git clone URL --branch feature-1 --single-branch

criando um arquivo README.md: touch README.md

adicionar o arquivo na area de preparação: git add "nome do arquivo"

comittar: git commit -m"mensagem"

exibir os commits: git log

criando um gitignore : echo "arquivo" > .gitignore

apagando os arquivos do gitignore: echo > .gitignore

criando um gitkeep para definir diretorio vazio: touche "arquivo"/.gitkeep

mandar todos arquivos para area de preparção: git add .

verificar os commits e o status: git status

remover o git init errado: git 

restaurar um arquivo em seu ultimo estado na arvore de trabalho: git restore "nome do arquivo"

alterando mensagem do commit: git commit --amend -m"mensagem"

alterando mensagem do commit atraves do editor do git: git commit --amend, logo apos apertar "i" e para sair "esc + : + w + Q"

desfazer o ultimo commit: git reset --(soft/mixed/hard) + hash do commit

historico mais detalhado: git reflog

enviar as alterações do repositorio local para o remoto: git push -u origin main

atualizar o repositorio local com as alterações do remoto: git pull

***branch é uma ramificação de algum projeto

***criar uma branch dentro de uma ja existente faz ela apontar para o commit que ja estava sendo apontado

criando branch teste: git checkout -b "nome" 

retornando para branch main: git checkout main

listar os ultimos commits de cada branch: gir branch -v

mesclar branchs: git merge "nome da branch teste"

listar branchs: git branch

excluir branch teste: git branch -d teste

baixar as alterações do repositorio remoto sem dar merge: git fetch origin main

ver as alterações do repositorio remoto: git diff main origin/main

trazer as alterações do remoto para o loca: git merge origin/main

clonar apenas uma branch: copiar url do repositore. git clone "URL" --branch teste --single-branch

arquivar modificação: git stash

listar modificação arquivada: git stash list

deletar commit: git reset HEAD^


git stash pop:-= 

gist stash apply:-=


git checkout master-dev

git checkout -b numero da branch

git pull upstream numero da atividade


---
nginx

start nginx






