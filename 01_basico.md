# 01 Basico

## Docker

- Containers docker são ambientes virtuais separados que possibilitam
a execução e configuração de vários processos e recursos. Eles ajudam na hora de executar um determinado ambiente de desenvolvimento ou de produção por exemplo. A camada fica totalmente isolada do resto do sistema.
- É tipo uma máquina virtual, porém bem mais leve. 

## Imagens Docker

- São moldes para criação dos containers, eles especificam como que o container será criado. É como se fosse uma classe no assunto orientação a objetos.

## Container x Imagem

- Uma imagem é uma só, é o molde pra criar o container.
- Vários containers podem ser criados a partir de uma imagem, eles podem se diferenciar entre si depois de instanciados, uma vez que ele é a instancia, é possível mudar qualquer coisa dele depois, instalar coisas e mexer no sistema de arquivos.

## Docker Hub

Repositório de imagens na web.
Existem várias imagens para variados propositos como por exemplo a Postgis que cria um container com um banco de dados PostgreSQL, com esta imagem dispensamos a instalação do PostgreSQL na nossa máquina.

### Baixando do Docker Hub

É possivel baixarmos imagens do Dockerhub usando o comando **pull** 

```shell 
docker pull <nome_imagem>
```

No entando podemos baixar a imagem e já criar o container diretamente usando o comando **run**
```shell 
docker run <nome_imagem>
```

o Docker segue os seguintes passos:
Verifica se a imagem está disponível localmente (no cache local do Docker).
Se não estiver disponível, ele faz o pull automático da imagem do Docker Hub (ou de outro registry configurado).
Depois de baixada, ele cria e inicia um container baseado nessa imagem.

## Volumes x Containers

É possível armazenar arquivos diretamente em um container, mas podemos criar algo que se chama **volume**, ele é basicamente um local para armazenamento de dados dos nossos containers, podemos usar um único volume para armazenar dados comuns a vários containers.

## Exemplo de uso de **volume**

No seguinte exemplo criamos um container usando a imagem do **postgis**, que é uma imagem capaz de rodar o PostgreSQL.

```shell
docker run --name meu-postgis \
  -e POSTGRES_PASSWORD=senha_segura \
  -e POSTGRES_USER=usuario \
  -e POSTGRES_DB=meubanco \
  -p 5432:5432 \
  -d postgis/postgis
```

| Parâmetro                           | Função                                            |
| ----------------------------------- | ------------------------------------------------- |
| `--name meu-postgis`                | Nome do container                                 |
| `-e POSTGRES_PASSWORD=senha_segura` | Senha do superusuário                             |
| `-e POSTGRES_USER=usuario`          | (opcional) nome do usuário                        |
| `-e POSTGRES_DB=meubanco`           | (opcional) nome do banco criado                   |
| `-p 5432:5432`                      | Expõe a porta 5432 para acesso externo            |
| `-d`                                | Roda em background (detached mode)                |
| `postgis/postgis`                   | Nome da imagem usada (será baixada se necessário) |

No entando os dados desta forma serão salvos dentro do container, o que significa que ao perder o container perderemos os dados.
Para resolver isso podemos salvar os dados fora dele, em um **volume**, assim mesmo que o container morra, os dados estão seguros.
Para isso só adicionamos ```-v /caminho/no/host:/var/lib/postgresql/data``` ao comando

```shell
docker run --name meu-postgis \
  -e POSTGRES_PASSWORD=senha_segura \
  -e POSTGRES_USER=usuario \
  -e POSTGRES_DB=meubanco \
  -p 5432:5432 \
  -v $HOME/docker/postgis-data:/var/lib/postgresql/data \
  -d postgis/postgis
```

### Executar container em background

```docker run -dti <image_name>```

# 🐳 Diferença entre `docker run` e `docker exec`

## 🔹 `docker run`

- Cria **um novo container** a partir de uma imagem.
- Pode executar um comando assim que o container é iniciado.
- Se a imagem não estiver no host, o Docker faz o **download automaticamente**.
- Você pode especificar volumes, redes, variáveis de ambiente e mais no momento da criação.

## Executando container já criado
O **docker run** tambem serve para rodar um container já criado

```docker run <nome_container>```

**Exemplo:**
```shell
docker run -it ubuntu bash
```

## 🔹 `docker exec`

- O comando `docker exec` é utilizado para **executar um comando em um container que já está em execução**.
- Com `docker exec`, você não cria um novo container. Em vez disso, você interage com um container que já está ativo.
- Esse comando é muito útil para **executar comandos de forma interativa ou fazer depuração** em containers em execução.

### Exemplo de uso:
```bash
docker exec -it meu-container bash

```
#### Significado das flags -it
**-i (interactive)**: Mantém o STDIN aberto, permitindo interatividade.

**-t (tty)**: Aloca um pseudo-TTY, criando um terminal interativo.

