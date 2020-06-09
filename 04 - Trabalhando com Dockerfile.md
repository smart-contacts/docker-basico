<p align="center">
  <a href="https://smartcontacts.com.br/">
    <img alt="Smart Contacts" src="https://smartcontacts.com.br/assets/img/logo.png" width="200" />
  </a>
</p>
<h2 align="center">
Informação sobre tecnologia, dicas, tutoriais, mini-cursos e muito mais.
</h2>

## Episódio 04 - Trabalhando com Dockerfile

### O que é um Dockerfile?

Falando de forma bem prática, o ```Dockerfile``` é um arquivo declarativo que tem como objetivo **construir imagens** docker.

O Dockerfile possui toda a estrutura e comandos necessários para o processo de construção de uma imagem Docker.

Exemplo de um arquivo ```Dockerfile```. Neste exemplo estarei comentando cada instrução para facilitar o entendimento. Logo abaixo você verá este mesmo exemplo sem os comentários:

```
instrução para definir a imagem docker que será usada como base para criação da nova imagem

FROM node:14.1-alpine

instrução para executar comandos na imagem base, no caso criar um subdiretório e
atribuir o usuario node e grupo node como "proprietários" do diretório /home/node/app

RUN mkdir -p /home/node/app/node_modules && chown -R node:node /home/node/app

criar o arquivo .bashrc na pasta /root com o conteúdo indicado pelo comando echo

RUN touch /root/.bashrc | echo "PS1='\w\$ '" >> /root/.bashrc

instrução que define o diretório base dentro da imagem

WORKDIR /home/node/app

instrução para copiar package*.json do diretório atual da sua máquina para o 
diretório base da imagem, definido no comando anterior

COPY package*.json ./

executar o comando indicado, no diretório base da imagem
no caso, o comando irá instalar tudo estiver configurado no package.json

RUN npm install

copiar todos os arquivos e subdiretórios da sua máquina para o diretório base da imagem

COPY . .

atribuir o usuario node e grupo node como "proprietários" de tudo que foi copiado

COPY --chown=node:node . .

definir o usuario

USER node

definir a porta onde o node da imagem funcionará

EXPOSE 3333

comando para executar o node da imagem

CMD [ "node", "index.js" ]
```

Exemplo do ```Dockerfile``` sem os comentário explicativos:

```
FROM node:14.1-alpine

RUN mkdir -p /home/node/app/node_modules && chown -R node:node /home/node/app

RUN touch /root/.bashrc | echo "PS1='\w\$ '" >> /root/.bashrc

WORKDIR /home/node/app

COPY package*.json ./

RUN npm install

COPY . .

COPY --chown=node:node . .

USER node

EXPOSE 3333

CMD [ "node", "index.js" ]
```

Após a criação do arquivo Dockerfile, você poderá criar sua própria imagem utilizando a seguinte sintaxe:

```
$ docker build -t <seu-user>/<nome-da-imagem>:<versao-da-imagem> .
```

> O ponto final define que a imagem será criada com base no arquivo Dockerfile que encontra-se no diretório atual. Caso a versão da imagem não seja informada, ela será nomeada automaticamente como "latest".

Construir uma imagem a partir de um Dockerfile:

```
$ docker build -t smartcontacts/nodecustom:v1 .
```

Rodar o container:

```
$ docker run -d -p 3000:3333 smartcontacts/nodecustom:v1
```

### Publicando imagem no Docker Hub

O Docker Hub é um repositório onde você pode disponibilizar suas imagens. Para isso você precisa realizar o login no shell usando as credenciais criadas no site do Docker Hub, conforme comando a seguir:

```
$ docker login

Aqui você deverá informar suas credenciais de acesso ao Docker Hub
```

Após realizar o login, a opção **push** do comando docker realiza o envio da imagem:

```
$ docker push <nome-da-imagem>
```

Exemplo:

```
$ docker push smartcontacts/nodecustom:v1
```

### Chegamos ao fim deste post

Se você tiver algo mais que possa agregar ao exposto, deixe seu comentário, será muito bem vindo!

Obrigado pela leitura.


### Links úteis:

[Canal no YouTube](https://www.youtube.com/channel/UCC6ue986efLUHRuqGiIfuwQ/featured?view_as=public)

[Instagram](https://www.instagram.com/smartcontacts/)

[Twitter](https://twitter.com/@ContactsSmart)

[GNU](http://www.gnu.org)

[Linux Ubuntu](https://ubuntu.com/)

[Docker](https://docs.docker.com/)
