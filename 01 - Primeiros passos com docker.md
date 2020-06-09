<p align="center">
  <a href="https://smartcontacts.com.br/">
    <img alt="Smart Contacts" src="https://smartcontacts.com.br/assets/img/logo.png" width="200" />
  </a>
</p>
<h2 align="center">
Informação sobre tecnologia, dicas, tutoriais, mini-cursos e muito mais.
</h2>

## Episódio 01 - Primeiros Passos Com Docker

> Este primeiro episódio trará um background teórico para embasar aquilo que será desenvolvido a partir do próximo episódio. Sabemos que não é a preferência da maioria mas... se faz necessário.

### O que é Docker?

O Docker é uma plataforma para o desenvolvedor e/ou administrador de sistemas: criar, executar e compartilhar aplicativos em **containers**. O uso de containers para implantar aplicativos é chamado de conteinerização.

O docker foi feito para rodar no Linux. Logo, o melhor comportamento você encontrará rodando no Linux, apesar de poder instalar e usar tanto em Windows quanto em macOS.

> Para rodar o Docker no Windows você precisará da versão Professional, que contém o Hyper-V. Para rodar no Windows Home, você terá que usar um recurso adicional, que é a ToolBox.

O container é:

- Flexível: Até as aplicações mais complexas podem ser containers.

- Leve: os containers aproveitam e compartilham o kernel do host, tornando-os muito mais eficientes em termos de recursos do sistema do que as máquinas virtuais.

- Portátil: você pode criar localmente, implantar na nuvem e executar em qualquer lugar.

- Acoplamento fraco: os containers são altamente auto-suficientes e encapsulados, permitindo substituir ou atualizar um sem atrapalhar outros.

- Escalável: você pode aumentar e distribuir automaticamente réplicas de containers.

- Seguro: os containers aplicam restrições e isolamentos agressivos aos processos sem nenhuma configuração necessária da parte do usuário.

### Imagens e Containers

Fundamentalmente, um container não passa de um processo em execução, com alguns recursos adicionais de encapsulamento aplicados a ele para mantê-lo isolado do host e de outros containers.

Um dos aspectos mais importantes desse isolamento  é que cada container interage com seu próprio sistema de arquivos privado; esse sistema de arquivos é fornecido por uma imagem do Docker.

Uma imagem inclui tudo que é necessário para executar um aplicativo - o código ou binário, dependências e quaisquer outros objetos necessários.

> Acesse o [Docker Hub](https://hub.docker.com) para mais detalhes sobre imagens docker.

### Containers e Máquinas Virtuais

Um container é executado nativamente no Linux e compartilha o kernel da máquina host com outros containers.

Por outro lado, uma máquina virtual (VM) executa um sistema operacional "convidado" completo com acesso virtual a recursos de host por meio de um hipervisor.

![Containers vs VMs](https://smartcontacts.com.br/assets/img/docker.png)

> Imagem retirada de: http://imesh.github.io/images/contvsvm.png

### Baixar e Instalar o Docker

A documentação do Docker tem com detalhes os passos necessários para a instalação seja em Linux, macOS ou Windows.

Para ver mais detalhes sobre instalação acesse a documentação:

- Instalar no [macOS](https://docs.docker.com/docker-for-mac/install/)

- Instalar no [Windows](https://docs.docker.com/docker-for-windows/install/)

- Instalar no [Ubuntu](https://docs.docker.com/engine/install/ubuntu/)

> Aqui nesta série, estaremos utilizando o Linux Ubuntu versão 20.04.

### Instalando Docker no Ubuntu

1. Remover versões antigas:

```
$ sudo apt-get remove docker docker-engine docker.io containerd runc
```

2. Atualizar a lista de pacotes apt e instalar os pacotes para permitir o uso de um repositório em HTTPS:

```
$ sudo apt-get update

$ sudo apt-get install \
    apt-transport-https \
    ca-certificates \
    curl \
    gnupg-agent \
    software-properties-common

$ curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -

$ sudo add-apt-repository \
   "deb [arch=amd64] https://download.docker.com/linux/ubuntu \
   $(lsb_release -cs) \
   stable"

$ sudo apt-get update
```

3. Instalar o Docker Engine:

```
$ sudo apt-get install docker-ce docker-ce-cli containerd.io
```

### Verificar a Instalação do Docker

Execute o comando abaixo no seu terminal para verificar se o docker já está disponível para uso.

```
$ sudo docker run hello-world
```

A saída desse comando será:

```
Hello from Docker!

This message shows that your installation appears to be working correctly.

To generate this message, Docker took the following steps:

 1. The Docker client contacted the Docker daemon.
 2. The Docker daemon pulled the "hello-world" image from the Docker Hub.
    (amd64)
 3. The Docker daemon created a new container from that image which runs the
    executable that produces the output you are currently reading.
 4. The Docker daemon streamed that output to the Docker client, which sent it
    to your terminal.
```

### Configurações de Pós-Instalação

A instalação do Docker (considerando o Ubuntu) cria o grupo denominado **docker** no sistema, grupo este que possui as devidas permissões para execução dos comandos e processos do Docker.

Com base nisso, precisamos incluir o nosso usuário do sistema nesse grupo. Execute o comando abaixo:

```
$ sudo usermod -aG docker $USER
```

Após rodar o comando, efetue logout e login novamente para que essa alteração seja reconhecida pelo sistema.

### Serviço Docker

Caso queira que o serviço Docker esteja disponível para uso após o processo de boot do sistema, efetue a configuração abaixo:

```
$ sudo systemctl enable docker
```

Se em algum momento quiser desabilitar o carregamento do serviço do Docker no processo de boot, execute o seguinte comando:

```
$ sudo systemctl disable docker
```

#### Comandos para trabalhar com o serviço Docker

Verificar o status do serviço:

```
$ sudo systemctl status docker.service
```

Parar o serviço:

```
$ sudo systemctl stop docker.service
```

Iniciar o serviço:

```
$ sudo systemctl start docker.service
```

Reiniciar o serviço:

```
$ sudo systemctl restart docker.service
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
