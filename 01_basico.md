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

```shell 
docker pull <nome_imagem>
```

