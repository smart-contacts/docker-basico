<p align="center">
  <a href="https://smartcontacts.com.br/">
    <img alt="Smart Contacts" src="https://smartcontacts.com.br/assets/img/logo.png" width="200" />
  </a>
</p>
<h2 align="center">
Informação sobre tecnologia, dicas, tutoriais, mini-cursos e muito mais.
</h2>

## Episódio 02 - Comandos Básicos com Docker

Basicamente, um container é criado a partir de uma imagem docker. O repositório oficial de imagens docker é o [Docker Hub](https://hub.docker.com/). Lá você poderá pesquisar as imagens que mais se adequam aquilo que você precisa. Quando executar o comando para rodar um container é necessário informar qual será a imagem que esse container usará.

> Crie uma conta no Docker Hub para que você possa enviar as imagens que você criar a partir de containers que você utilizará no seu dia a dia como desenvolvedor. Veremos isso aqui nessa série.

> Evite usar imagem que não seja Oficial.

### Containers

Executar um container:

```
$ docker run hello-world
```

Verificar containers em execução no seu PC:

```
$ docker ps
```

Verificar todos os containers que existem no seu PC, inclusive aqueles que não estão em execução no momento:

```
$ docker ps -a
```

Se você desejar baixar uma imagem para rodar um container na sua máquina, você pode usar a opção **pull** do Docker. Exemplo:

```
$ docker pull mongo
```

Rodar um container nginx mapeando a porta 8080 do seu PC com a porta 80 do container:

```
$ docker run -p 8080:80 nginx
```

Rodar o container do nginx denominado webserver em segundo plano, deixando o terminal disponível para uso:

```
$ docker run --name webserver -p 8080:80 -d nginx
```

Criar um novo container com a imagem baixada **mongo** que foi baixada no primeiro exemplo:

```
$ docker run --name mongodb -p 27017:27017 -d mongo
```

Excluir um container do seu PC:

```
$ docker rm <id ou nome do container>

Caso não seja possível excluir o container no momento você pode usar a opção -f para forçar
```

Exibir os logs de um container pode ajudar a investigar possíveis problemas ao tentar rodar um container:

```
$ docker logs <id ou nome do container>
```

> Você pode usar ```docker rm --help``` para consultar as opções disponíveis para usar. O ```--help``` se aplica para qualquer comando do Docker.

### Imagens

Verificar quais imagens de containers estão instaladas localmente no seu PC:

```
$ docker images
```

Remover uma imagem do seu PC:

```
$ docker rmi <id ou nome da imagem>
```

Remover todas as imagens do seu PC:

```
$ docker rmi $(docker images -q) -f
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
