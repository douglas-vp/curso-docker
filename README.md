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

