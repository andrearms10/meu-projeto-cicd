# Comando Básicos do GIT

### Criando repositório local

- **`mkdir meu-projeto-cicd`**: Cria uma nova pasta chamada "meu-projeto-cicd" no seu computador.

- **`&&`**: Une dois comandos. O segundo só roda se o primeiro der certo.

- **`cd meu-projeto-cicd`**: Entra na pasta que você acabou de criar.

- **`git init`**: Transforma essa pasta em um repositório Git para iniciar o controle de versão.

- **`echo "# Meu Projeto CI/CD" > README.md`**: Cria um arquivo de texto chamado "README.md" com o conteúdo # Meu Projeto CI/CD.

- **`git add .`**: Adiciona todos os arquivos novos ou modificados (neste caso, o README.md) para a área de preparação do Git.

- **`git commit -m "chore: initial commit"`**: Salva permanentemente essas alterações no histórico do Git com a mensagem descritiva informada

<br>

### Só que estamos criando um repositório local na nossa máquina e precisamos vincular ao repositório do GitHub (remoto que é conhecido como origin). 

### Seguem os comandos abaixo para vincular o nosso repositório local ao remoto do GitHub.


<br>

- **`git branch -M main`**: Renomeia a sua branch principal **local Master** para `main` (padrão atual do GitHub).

- **`git remote add origin <URL>`**: Vincula o seu repositório local ao repositório remoto que você acabou de criar no GitHub sob o nome "origin". 
Este é o **nome padrão** (um apelido) que o Git dá para o seu servidor remoto principal.

- **`git push -u origin main`**: Envia os seus arquivos locais para o GitHub e define a branch `main` como o destino padrão para os próximos envios. [1, 2]


<br>

### Após a vinculação (1 vez) segue o Fluxo padrão

git add .

git commit -m "Adiciona novos arquivos"

git push



### **mas antes de enviar,  solicita uma autenticação → Conclua a autenticação**

1. O terminal vai gerar um **link** de autenticação e  abrir o navegador sozinho.

2. O navegador vai abrir uma aba pedindo um **código de dispositivo** (Device Code)

3. Acesse o seu e-mail, pegue o código de verificação enviado pelo GitHub e insira na página do navegador.

4. Mantenha a aba do navegador aberta até aparecer a mensagem **"Authentication Successful"** (Autenticação Bem-sucedida).Assim que o navegador confirmar o sucesso, volte para o terminal e você verá que o envio dos arquivos terá sido concluído.

### Configurar chaves **SSH** ou **Tokens de Acesso Pessoal (PAT)** elimina a necessidade de fazer login pelo navegador toda vez que você usar o terminal. A diferença principal é:

• **Token de Acesso (PAT)**: Funciona como uma senha longa gerada pelo GitHub. É mais fácil de configurar, mas expira depois de um tempo (ex: 30 a 90 dias).

• **Chave SSH**: Cria uma conexão criptografada direta entre a sua máquina e o GitHub. É o método mais seguro, profissional e **nunca expira**. [1, 2, 3, 4, 5]


<br>

### **Opção 1: Configurar Chave SSH (Recomendado)**



**1. Gerar a chave no seu terminal [1]**

Abra o terminal e cole o comando abaixo, substituindo pelo seu e-mail do GitHub: [1, 2]

**bash**

`ssh-keygen -t ed25519 -C "seu-email@exemplo.com"`

- Pressione **Enter** em todas as perguntas que surgirem para salvar no local padrão e não definir uma senha (passphrase). [1]

**2. Copiar a chave gerada**

Execute o comando correspondente ao seu sistema operacional para copiar a chave pública para a área de transferência: [1]

- **Windows (Prompt/Git Bash)**: `clip < ~/.ssh/id_ed25519.pub`
- **Mac**: `pbcopy < ~/.ssh/id_ed25519.pub`
- **Linux**: `cat ~/.ssh/id_ed25519.pub` (selecione o texto exibido e copie manualmente) [1, 2, 3, 4]

**3. Adicionar a chave no GitHub [1]**

1. Acesse o **GitHub SSH Settings**.
2. Clique em **"New SSH key"**.
3. No campo **Title**, dê um nome para o seu computador (ex: "Meu Notebook").
4. No campo **Key**, cole o código que você copiou no passo anterior.
5. Clique em **"Add SSH key"**. [1, 2, 3, 4, 5]

**4. Alterar o link do seu projeto para SSH**

Como você começou o projeto usando o link `https://`, mude para o formato SSH com o comando:

**bash**

`git remote set-url origin git@github.com:SEU-USUARIO/meu-projeto-cicd.git`

*(Troque `SEU-USUARIO` pelo seu nome de usuário real do GitHub)*

---

<br>

### **Opção 2: Configurar Token de Acesso (PAT)**

Se preferir o Token em vez do SSH, siga estes passos:

**1. Gerar o Token no GitHub [1]**

1. Acesse o **GitHub Token Settings**.
2. Clique em **"Generate new token"** e escolha **"Generate new token (classic)"**.
3. No campo **Note**, escreva algo como "Terminal Git".
4. Defina a expiração (Ex: 30 ou 90 dias).
5. Nas caixas de seleção abaixo, marque pelo menos a opção **`repo`** (ela dá permissão para gerenciar seus repositórios).
6. Role até o final da página e clique em **"Generate token"**.
7. **Copie o token gerado imediatamente.** Ele só aparece uma vez. [1, 2, 3, 4, 5]

**2. Usar o Token no Terminal**

Quando você executar o comando `git push`, o terminal vai pedir o seu **Username** (digite seu usuário do GitHub) e depois a **Password**. [1]

- No campo **Password**, **cole o Token** que você copiou (não use a sua senha normal do GitHub).

*(Nota: Ao colar no terminal, os caracteres não aparecem por segurança, basta colar e apertar Enter).* [1, 2]

<br>


### O que significa o que significa o ~ em Paula@HP_Sam MINGW64 ~

O caractere til (**~**) significa que você está atualmente na sua **pasta home (diretório pessoal)** do usuário no Windows. 

No ambiente do **MINGW64** (comum ao usar o Git Bash no Windows), o terminal traduz os caminhos do Windows para o formato Linux.

Aqui está o desmembramento completo do que aparece na sua tela:
• **Paula**: O seu nome de usuário no Windows.
• **HP_Sam**: O nome da sua máquina (computador).
• **MINGW64**: O ambiente de simulação Unix (64-bit) que permite rodar comandos Linux no Windows.
• **~**: A sua localização atual, que equivale ao caminho físico `C:\Users\Paula`.

---

### **Como criar arquivos com o `echo`**

• **Criar um arquivo novo (ou sobrescrever)**: Usa-se o operador `>`
    ◦ `echo "Olá Mundo" > texto.txt`
    ◦ Isso cria o arquivo `texto.txt` com o conteúdo "Olá Mundo". Se o arquivo já existia, o conteúdo antigo é apagado. [1, 2]

• **Criar ou adicionar texto ao final**: Usa-se o operador `>>`
    ◦ `echo "Nova linha" >> texto.txt`
    ◦ Isso cria o arquivo se ele não existir, ou apenas adiciona "Nova linha" no final dele sem apagar o que já estava escrito. [1, 2, 3]

• **Criar um arquivo totalmente vazio**:
    ◦ `echo -n "" > vazio.txt` [1]