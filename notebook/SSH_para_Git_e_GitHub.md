# Configurar SSH para Git e GitHub :key:

##### :warning: Encontrei o conteúdo desse tutorial em: https://medium.com/@rgdev/como-adicionar-uma-chave-ssh-na-sua-conta-do-github-linux-e0f19bbc4265, estou apenas colocando aqui para eventuais consultas pessoais.

Usando o protocolo SSH, você pode conectar e autenticar com servidores e serviços remotos. Com chaves SSH, você pode conectar com o Github sem ter que ficar digitando seu usuário ou senha a cada conexão.

## Verificar chaves SSH existentes.

1. Abra o Terminal
2. Digite **ls -al ~/.ssh** para ver se tem alguma chave SSH presente

```
$ ls -al ~/.ssh
# Lista os arquivos do seu diretório .ssh, se eles existem
```

Por padrão, o nome dos arquivos das chaves públicas pode ser um dos seguintes:

- *id_dsa.pub*
- *id_ecdsa.pub*
- *id_ed25519.pub*
- *id_rsa.pub*

Bom se você não tem um par de chave pública e privada, ou não quer conectar as que estão disponíveis no Github, então **gere uma chave nova**.

Se você viu um par de chave pública e privada listado (por exemplo *id_rsa.pub* and *id_rsa*) e gostaria de usá-las para conectar com o Github, você pode **adicionar sua chave SSH ao SSH-agent** e pular o próximo passo da geração de chave do tutorial.

## Gerar uma nova chave SSH

1. Abra o terminal
2. Digite isso, substituindo pelo seu email do Github.

```
ssh-keygen -t rsa -b 4096 -C "your_email@example.com"
```

Isso cria uma nova chave ssh, usando o email como rótulo.

3. Quando aparecer escrito no terminal “Enter a file in which to save the key,” pressione Enter. Isso aceita a localização do arquivo padrão.

```
Enter a file in which to save the key (/home/you/.ssh/id_rsa): [Press enter]
```

4. No terminal, digite uma senha segura.

```
Enter passphrase (empty for no passphrase): [Type a passphrase]
Enter same passphrase again: [Type passphrase again]
```

## Adicionando sua chave SSH ao ssh-agent

Antes de adicionar um nova chave SSH no ssh-agent para gerenciar suas chaves, você deveria **Verificar chaves SSH existentes** e **Gerar uma nova chave SSH** se for preciso.

1. Inicie o ssh-agent em background.

```
$ eval "$(ssh-agent -s)"
Agent pid 59566
```

2. Adicione sua chave privada SSH no ssh-agent. Se você criou sua chave com um nome diferente, substitua *id_rsa* no comando com o nome de sua chave privada.

```
$ ssh-add ~/.ssh/id_rsa
```

## Adicionar a chave SSH na sua conta do Github

1. Copie a chave SSH

Se sua chave SSH tem um nome diferente que o exemplo no código, modifique o nome do arquivo. Quando copiar sua chave, não adicione novas linhas ou espaços em branco.

```
$ sudo apt-get install xclip
# Faz o download e instala o xclip. Se você não tem instalado o 'apt-get', você pode usar outro instalador (como o 'yum')$ xclip -sel clip < ~/.ssh/id_rsa.pub
# Copia o conteúdo da sua chave id_rsa.pub
```

**Dica:** Se `xclip` não está funcionando, você pode encontrar a pasta oculta `.ssh` , abrir o arquivo no terminal, e copiar ela.

```
$ cat ~/.ssh/id_rsa.pub
```

2. No canto superior direito do Github, clique na sua foto de perfil e clique em **Settings**.

3. Na barra lateral esqueda, clique em **SSH and GPG keys**.

4. Clique em **New SSH key** ou **Add SSH key**.

5. No campo “Título”, adicione um descrição para a nova chave.

6. Cole sua chave dentro do campo “Key”.

7. Clique em **Add SSH key**.

8. Se for solicitado, confirme sua senha do Github.

## Alterar o diretório remoto para SSH

Caso você já tenha projetos do github que estão utilizando HTTPS para conexão no seu computador, e quiser mudar para SSH.

Dentro da pasta do repositório digite, substituindo o ***your_user\*** pelo seu usuário do github e ***name_repository\*** pelo nome do seu repositório.

```
$ git remote set-url origin git@github.com:your_user/name_repository.git
```

Na primeira conexão ele vai perguntar se você quer continuar conectado, só digitar *yes* e também vai pedir a senha da sua chave SSH. Nas próximas conexões que você for fizer algo, não vai mais precisar digitar seu usuário do github nem a senha.