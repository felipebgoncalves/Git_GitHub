## VERSIONAMENTO DE CÓDIGO COM Git - RESUMO


### COMANDOS GIT

### Clonar Repositório no GitHub:
- Ir até à pasta em que será clonado o repositório
- Abrir o terminal do Git Bash
- Digitar o seguinte comando:

        git clone <endereço do repositório GitHub>

Obs.: Atalho do teclado para colar: Shift + Ctrl + Insert

# ----------------------------------------------------------------
### Trabalhar com arquivos dentro da pasta + repositório do GitHub

- Abrir a pasta criada
- Abrir o terminal do Git Bash dentro da pasta clonada (main)
- Digitar os seguintes comandos:


  - Verificar o status da branch 'main'

        git status

  - Add arquivos para a área de preparação do Git
              
        git add .

  - Versionamento de todos os arquivos que estão na área de preparação

        git commit -m '<mensagem>'

  - Verificação de todos os commits realizados no repositório clonado 
  
        git log

  - Enviar atualização dos arquivos para o repositório no GitHub

        git push origin main

  - Trazer os arquivos do repositório GitHub para a máquina local

        git pull origin main 

# ----------------------------------------------------------------
### Criar uma pasta (na máquina local) para subir arquivos para o GitHub

- Abrir diretório onde será criada a pasta no novo repositório
- Abrir terminal do Git Bash
- Digitar os seguintes comandos:

    - Criar a pasta

           mkdir <nome da pasta>
    
    - Iniciar o repositório
            
           git init

    - Alterar o nome da Branch - padrão é 'main'

          git branch -M main

# ----------------------------------------------------------------
### O que é uma BRANCH?

- É uma ramificação do projeto principal (branch main)

  - Comando para criação de uma nova Branch:

          git checkout -b <nome da nova branch>

  - Verificar (listar) todas as branchs do projeto

            git branch

  - Comando para entrar numa Branch (diferente da principal)

            git branch <nome da branch que desejo entrar>

  - Após validação dos arquivos na branch secundária e preciso levar essa alteração para a branch principal (main)
  
    - Obs.: Preciso estar na branch main para trazer (fazer o merge) a branch q desejo fundir

                git merge <nome da branch que quero fundir com a branch main>

  - Listar o último commit de cada Branch

                git branch -v
  
  - Excluir uma branch 

                git branch -d <nome da branch que se deseja excluir>
  
  - Clonar uma branch específica do repositório remoto 

                git clone <URL do repositório> --branch <nome da branch> --single-branch

# ----------------------------------------------------------------
- Outros comandos importantes

        git config --global user.name <nome>
        
        git config --global user.email <email>

        git config --global init.defaultBranch main

- Para excluir um versionamento de uma pasta (excluir recursivamente e a força) 
    
        rm -rf .git

- Retornar o último status de um arquivo modificado de forma errada (recuperar)
    
        git restore <nome do arquivo>

- Alteração da mensagem do último commit
        
        git log [verificar os commits]

        git commit --amend -m '<nova mensagem>'
        
  - Para escrever no editor:
       
        git commit --amend

  - i (para escrever)
  - esc + :
  - wq (para salvar e sair do editor)

- Para desfazer o último commit realizado 

- O comando 'git reset' oferece 03 opções: --soft // --mixed // --hard

  - --soft 
        
        git reset --soft <hash do commit>
  
  - --mixed

        git reset --mixed <had do commit>
  
  - --hard

        git reset --hard <hash do commit>

- Para retirar arquivos da área de preparação

        git reset <nome do arquivo>

        git restore --staged <nome do arquivo>


# ----------------------------------------------------------------
- Comando para associar um repositório local ao repositório remoto no GitHub
        
        git remote add origin https://github.com/USUÁRIO/REPOSITÓRIO.git

### Alterar a URL remota para a conta desejada

- Para a conta principal, a URL deve ser:

        git remote set-url origin git@github.com-principal:USUÁRIO/REPOSITÓRIO.git

- Para a conta secundária, a URL deve ser:

        git remote set-url origin git@github.com-secundaria:USUÁRIO/REPOSITÓRIO.git

- Verificar a URL remota atual

        git remote -v
        
# ----------------------------------------------------------------

#### Geração de chaves SSH

### 1. Gerar duas chaves

## Pessoal:

        ssh-keygen -t ed25519 -C "seu-email-pessoal@example.com" -f ~/.ssh/id_ed25519_github_pessoal


## Trabalho:

        ssh-keygen -t ed25519 -C "seu-email-trabalho@empresa.com" -f ~/.ssh/id_ed25519_github_trabalho


- O parâmetro -f define nomes diferentes para os arquivos da chave.

### 2. Adicionar ao ssh-agent

        eval "$(ssh-agent -s)"
        ssh-add ~/.ssh/id_ed25519_github_pessoal
        ssh-add ~/.ssh/id_ed25519_github_trabalho

### 3. Configurar o arquivo ~/.ssh/config

- Edite (ou crie) esse arquivo:

        nano ~/.ssh/config


- E adicione:

        # Conta Pessoal
        Host github.com-pessoal
            HostName github.com
            User git
            IdentityFile ~/.ssh/id_ed25519_github_pessoal
        
        # Conta Trabalho
        Host github.com-trabalho
            HostName github.com
            User git
            IdentityFile ~/.ssh/id_ed25519_github_trabalho

### 4. Adicionar as chaves no GitHub

- Vá em Settings → SSH and GPG keys em cada conta

- Copie a respectiva chave pública:

        cat ~/.ssh/id_ed25519_github_pessoal.pub
        cat ~/.ssh/id_ed25519_github_trabalho.pub


- Cole no GitHub certo.

### 5. Usar os repositórios corretamente

- Quando for clonar repositórios, use o Host configurado:

- Repositório pessoal:

        git clone git@github.com-pessoal:usuario/repositorio.git


- Repositório do trabalho:

        git clone git@github.com-trabalho:empresa/repositorio.git


👉 Assim, cada repositório vai usar a chave certa automaticamente.
