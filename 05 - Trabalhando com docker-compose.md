<p align="center">
  <a href="https://smartcontacts.com.br/">
    <img alt="Smart Contacts" src="https://smartcontacts.com.br/assets/img/logo.png" width="200" />
  </a>
</p>
<h2 align="center">
Informação sobre tecnologia, dicas, tutoriais, mini-cursos e muito mais.
</h2>

## Episódio 05 - Trabalhando com docker-compose

### O que é o docker-compose?

O **docker-compose** é uma ferramenta cujo o objetivo é facilitar o processo de executação de containers docker de forma declarativa. Cada container é executado como um serviço.

O arquivo para criar as instruções para o docker-compose deve ser nomeado como ```docker-compose.yml``` ou ```docker-compose.yaml```.

É importante entender que a **identação deve ser respeitada**, pois ela define a hierarquia das instruções para o docker. A instrução **services** é usada para definir o nome de cada container/serviço. Abaixo de cada serviço, seguem as instruções para definição da imagem docker, volumes, variáveis de ambiente, portas de comunicação, etc.

Exemplo 1:

```
version: '3'
services:
  db:
    image: mysql:5.7
    volumes:
      - db_data:/var/lib/mysql
    restart: always
    environment:
      MYSQL_ROOT_PASSWORD: wordpress
      MYSQL_DATABASE: wordpress
      MYSQL_USER: wordpress
      MYSQL_PASSWORD: wordpress

  wordpress:
    depends_on:
      - db
    image: wordpress:latest
    ports:
      - 8080:80
    restart: always
    environment:
      WORDPRESS_DB_HOST: db:3306
      WORDPRESS_DB_USER: wordpress
      WORDPRESS_DB_PASSWORD: wordpress
volumes:
  db_data:
```

#### volumes

A instrução **volumes** é útil para você manter na sua máquina local arquivos usados no container, mesmo após o encerramento da execução desse container. No exemplo acima, o diretório local da sua máquina denominado "db_data" está sendo mapeado com o diretório do banco de dados do container.

O diretório "db_data" deve ser criado na sua máquina no mesmo local do arquivo **docker-compose.yaml**.

#### networks

Por padrão, o Compose configura uma única rede para os serviços configurados no **docker-compose.yaml**. Cada container de um serviço ingressa na rede padrão e é acessível pelos outros containers nessa rede. O hostname de cada container será o próprio nome do serviço, configurado no **docker-compose.yaml**. O nome da rede será definido com o mesmo nome do diretório onde está o seu projeto. Também é definido um endereço IP para cada container configurado como serviço.

> Você pode estar acessando o arquivo **/etc/hosts** de um container/serviço para verificar as configurações de rede.

É possível configurar suas próprias redes com a instrução **networks**, como no exemplo abaixo. Isso permite criar topologias mais complexas e especificar opções e drivers de rede personalizados. Você também pode usá-lo para conectar serviços a redes criadas externamente que não são gerenciadas pelo Compose. Para mais detalhes sobre configuração de redes personalizadas, acesse a [documentação específica](https://docs.docker.com/compose/networking/).

Exemplo 2:

```
version: '3'
services:
  # Banco de dados
  database:
    image: mysql:5.7
    volumes:
      - db_data:/var/lib/mysql
    environment:
      - "MYSQL_DATABASE=homestead"
      - "MYSQL_USER=homestead"
      - "MYSQL_PASSWORD=secret"
      - "MYSQL_ROOT_PASSWORD=smartcontacts"
    networks:
      - smartcontacts

  # App Laravel
  app:
    image: smartcontacts/laravel-app:v1
    container_name: app
    ports:
        - 8000:8000
    networks:
      - smartcontacts       
    depends_on:
      - database

  # Servidor Web
  web:
    image: smartcontacts/web:v1
    container_name: web  
    ports:
      - 8080:80
    networks:
      - smartcontacts
    depends_on:
      - app    
networks:
  smartcontacts:
volumes:
  db_data:
```

> Os exemplos acima são hipotéticos, você deve substituir os nomes das imagens usadas como exemplo, por imagens que você criar aí no seu ambiente de desenvolvimento ou por imagens oficiais que podem ser encontradas no [Docker Hub](https://hub.docker.com/).

Após criar o arquivo ```docker-compose.yaml```, execute o comando abaixo para subir os serviços (o comando deve ser executado no diretório onde se encontra o arquivo):

```
$ docker-compose up -d
```

Para encerrar os serviços, basta executar:

```
$ docker-compose down
```

Verificar somente os containers dos serviços sendo executados:

```
$ docker-compose ps
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
