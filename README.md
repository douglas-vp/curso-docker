# Docker
 
  * Por que os containers são mais leves em relação a uma máquina virtual?
  * Como eles garantem o isolamento?
  * Como funcionam sem a necessidade de instalar um sistema operacional?
  * Como ocorre a divisão de recursos do sistema?
  * Como os containers funcionam?
  
 Os containers operam de maneira semelhante a processos no sistema operacional. Diferentemente das máquinas virtuais, que passam por uma etapa de virtualização do sistema operacional, os containers são executados diretamente como processos no sistema, o que resulta em um consumo de recursos reduzido, uma vez que eles não requerem virtualização completa.

 ### Como os containers garantem o isolamento?
 Os containers utilizam o conceito de ***namespaces*** para garantir o isolamento entre si e do sistema operacional original. Esse mecanismo permite que cada container tenha um ambiente isolado em diferentes níveis. Os principais namespaces utilizados são:

  * **PID**: Isola os processos de cada container, garantindo que um processo em um container não interfira nos processos do sistema operacional ou de outros containers.
  * **NET**: Isola a interface de rede de cada container, permitindo que sua comunicação de rede não afete o sistema original.
  * **IPC**: Gerencia a intercomunicação entre processos.
  * **MNT**: Garante o isolamento do sistema de arquivos, montagem e volumes.
  * **UTS**: Isola e, ao mesmo tempo, compartilha o host (kernel) entre o container e o sistema operacional.
    
 Graças ao namespace UTS, os containers que rodam em sistemas com kernel Linux podem acessar o kernel original do sistema sem a necessidade de um sistema operacional completo, utilizando apenas a parte do kernel necessária para sua execução.

 ### Gerenciamento de recursos: Cgroups
 Para o gerenciamento de recursos, os containers utilizam o conceito de ***Cgroups (Control Groups)***, que permitem definir limites para o consumo de CPU, memória e outros recursos, tanto manual quanto automaticamente, para cada container.
 
 O **Docker** é uma plataforma que implementa a virtualização de software utilizando a tecnologia de contêineres para facilitar a implantação e execução de aplicações. Um contêiner pode ser compreendido como uma unidade leve e portátil que contém tudo o necessário para executar um pedaço de software, incluindo o código, runtime,   bibliotecas e dependências. Esse modelo de virtualização oferece diversos benefícios, com destaque para o isolamento de contextos e o versionamento de aplicações.

### Isolamento de Contextos
Cada contêiner possui seu próprio sistema de arquivos, processos, espaço de rede e recursos, garantindo que a aplicação dentro do contêiner não interfira em outras aplicações ou no sistema hospedeiro. Isso proporciona um alto grau de independência e isolamento, essencial para a segurança e estabilidade do ambiente.

### Versionamento de Aplicações
No Docker, as aplicações são encapsuladas em imagens, que são versões imutáveis e autossuficientes. Uma imagem Docker é composta por camadas, o que permite o versionamento eficiente e a reutilização de partes comuns entre diferentes aplicações. Utilizando um arquivo de configuração chamado Dockerfile, que descreve os passos para criar uma imagem, o versionamento torna-se simplificado. Alterações no Dockerfile geram novas versões da imagem, garantindo consistência na implantação e no gerenciamento de versões.

O Docker proporciona uma abordagem eficiente para o desenvolvimento, empacotamento e execução de aplicações, oferecendo benefícios como isolamento de contextos, consistência entre ambientes e versionamento controlado. Essas características fazem do Docker uma ferramenta poderosa para equipes de desenvolvimento e operações que buscam eficiência e confiabilidade em todo o ciclo de vida de uma aplicação.

# Docker Hub

### Conhecendo o Docker Hub e a Utilização de Imagens

Ao retornar ao terminal, o comando `docker run hello-world` é repetido para observar os resultados:

`docker run hello-world`

A saída informa que a imagem não está presente localmente, desencadeando o download. Após o término, o processo é validado pelo digest sha256, que será abordado posteriormente. Exemplo da saída:

 `Unable to find image 'hello-world:latest' locally`\n
 latest: Pulling from library/hello-world
 2db29710123e: Pull complete
 Digest: sha256:2498fce14358aa50ead0cc6c19990fc6ff866ce72aeb5546e1d59caac3d0d60f
 Status: Downloaded newer image for hello-world:latest`

O container exibe uma mensagem de "Hello from Docker" até o final do retorno. Após limpar o terminal, realiza-se um novo teste com o comando docker run, mas desta vez inserindo uma sequência aleatória de caracteres:
```bash
   docker run cmsdokcmsdocmsdcoiscmdsoicmdiocsmdicosdmciosdmcidsocmsdiocms

Como retorno, a seguinte mensagem de erro é obtida:
```bash
   Unable to find image 'cmsdokcmsdocmsdcoiscmdsoicmdiocsmdicosdmciosdmcidsocmsdiocms:latest' locally
   docker: Error response from daemon: pull access denied for cmsdokcmsdocmsdcoiscmdsoicmdiocsmdicosdmciosdmcidsocmsdiocms, repository does not exist or may require 'docker login': denied: requested access to the resource is denied.
   See 'docker run --help'.

Inicialmente, é mencionado que a busca pela imagem local não teve êxito. Em seguida, o erro aponta para uma negação de acesso ou inexistência do repositório. Isso destaca a importância de fornecer um nome válido, como hello-world, que é localizado com sucesso.

### Localização de Imagens: Docker Hub

Para que o comando docker run funcione corretamente, é necessário localizar uma entidade denominada imagem. O Docker utiliza o Docker Hub, um repositório central de imagens, onde é possível pesquisar e encontrar imagens confiáveis e oficiais. Executando o comando docker run --help, a estrutura básica do comando é observada:

plaintext
Copiar código
Usage: docker run [OPTIONS] IMAGE [COMMAND] [ARG...]
Aqui, o docker run requer opções e o nome da imagem a ser executada. Ao buscar "hello-world" no Docker Hub, uma imagem oficial é encontrada, mantida por desenvolvedores confiáveis e com reconhecimento da comunidade. Se um nome inválido for pesquisado, nenhuma imagem será encontrada, resultando em erro.

Exemplos de Imagens no Docker Hub
O Docker Hub abriga diversas imagens, incluindo algumas que replicam sistemas operacionais. Embora um container não precise de um sistema operacional completo, ele pode incluir um sistema base, como o Ubuntu. Ao pesquisar por "Ubuntu" no Docker Hub, uma imagem oficial é localizada que, ao ser executada, cria um container baseado no Ubuntu. A execução é realizada com o comando:

bash
Copiar código
docker run ubuntu
Este comando instrui o Docker a acessar o Docker Hub, baixar a imagem e iniciar o container. Alternativamente, o comando docker pull pode ser utilizado para baixar a imagem e, posteriormente, executá-la:

bash
Copiar código
docker pull ubuntu
A saída indicará o download e extração da imagem, mas o container ainda não será executado. Para iniciar a execução, utiliza-se:

bash
Copiar código
docker run ubuntu

