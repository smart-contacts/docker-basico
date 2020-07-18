<p align="center">
  <a href="https://smartcontacts.com.br/">
    <img alt="Smart Contacts" src="https://smartcontacts.com.br/assets/img/logo.png" width="200" />
  </a>
</p>
<h2 align="center">
Informação sobre tecnologia, dicas, tutoriais, mini-cursos e muito mais.
</h2>

## Episódio 03 - Comandos de interação Docker

### Melhorando a interação com os Containers Docker

Acessar o shell de um container:

```
$ docker exec webserver uname -a

$ docker exec -it webserver /bin/bash

A opção -it permite interagir com o shell do container (/bin/bash)
```

A partir desse tipo de acesso, pode-se fazer modificações no container, instalar pacotes e bibliotecas, etc. Depois de realizar as modificações necessárias é possível criar uma imagem a partir desse container que foi customizado.

Criação de uma nova imagem customizada:

```
$ docker commit webserver smartcontacts/nginxcustom:v1
```

Criando um novo container com base na imagem criada no exemplo acima:

$ docker run -d -p 8080:80 --name web02 smartcontacts/nginxcustom:v1

### Entendendo o conceito de Volumes de Dados do Docker

Os volumes são usados para que possamos mapear os dados usados nos containers com o host, de forma que, ao parar e/ou remover um container, os dados sejam mantidos no host. A opção "-v" permite informar o volume a ser usado para os dados.

Mapeando uma pasta existente do host com um container:

```
$ docker run -d -p 8080:80 -v /home/smartcontacts/www/:/usr/share/nginx/html --name webserver nginx

$ docker exec -it webserver /bin/bash
```

Inspecionar as ações executadas pelo docker com o container criado acima:

```
$ docker inspect webserver
```

Compartilhando volumes entre containers:

```
$ docker run -d -p 8085:80 --volumes-from webserver --name web02 nginx
```

Ou seja, a pasta do host está compartilhada com dois containers.

### Configurando um ambiente WordPress

Criar o container do Mysql:

```
$ docker run --name dbserver -e MYSQL_ROOT_PASSWORD=root -e MYSQL_DATABASE=wordpress -d mysql:5.7
```

Criar o container do WordPress:

```
$ docker run --name wordpress --link dbserver:mysql -d -p 8088:80 wordpress

$ docker exec -it wordpress bash
```

Verificar o arquivo /etc/hosts:

```
$ cat /etc/hosts

O IP do container do banco de dados deve estar configurado
```

Instalar o cliente Mysql no container wordpress para acessar o servidor do outro container:

```
$ apt-get update

$ apt-get install mysql-cliente vim

$ mysql -uroot -h mysql -p
A senha do mysql é root

$ show databases;
Executar no console do mysql
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
