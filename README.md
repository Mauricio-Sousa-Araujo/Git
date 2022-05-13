# Git

## Comandos Básicos de configuração

#### Para listas configurações correntes
1. git config --list 

#### Alterar Nome Global
2. git config --global user.name "Mauricio de Sousa"

#### Alterar nome Global
3. git config --global user.name "Mauricio de Sousa"

#### Alterar nome repositório local
4. git config  user.name "Mauricio de Sousa"

#### Alterar e-mail  global
5.  git config --global user.email "mauricio_ploc@hotmail.com"

#### Alterar e-mail repositório local
6.  git config  user.email "mauricio_ploc@hotmail.com"


## Comandos Básicos de trabalho

#### Cria o arquivo .git para que o arquivo possa ser versionado
1. git init  

#### Adiciona o arquivo para área de staging
2. git add file_name

#### Salva os arquivos da área de staging para o repositório local
3. git commit -m "Mensagem de comite"

#### 
4. git diff

#### 
5.  git diff -staged


## Comandos de log


#### Mostra histórico de  comites do mais recente pro mais antigo
1.  git log

#### Mostra histórico de  comites do mais recente pro mais antigo
2. git checkout id_versão

#### Limpa arquivos que foram criados que ainda não estão na área de staged
3. git clean -f

#### Remove as alterações que estão em stage
4. git reset --hard == git restore archive

#### Puxa alterações do repositório remoto
5. git pull

#### Empurra alterações no repositório remoto
4. git push