# Docker
**Container**: pacote de aplicação que funciona isoladamente do sistema operacional com todas as dependencias dentro de si. Aplicação contida que funciona no ambiente que está.

Conjunto de tecnologias presentes no kernel do Linux.

Tamanho bem menor que uma máquina virtual.

### Tecnologias chave
**namespaces**: isolam os processos dos containers e tambem os pontos de montagem, diretórios, discos, redes...

**cgroups (control groups)**: limitam o acesso a recursos da máquina como CPU, memória e tráfego de rede.

**union mount**: características dos sistemas de arquivos que trabalham com camadas. Estas camadas pode ser compartilhadas.

### Imagens

Dentro da imagem está a aplicação, suas dependências, bibliotecas, binários e outros arquivos.
Uma imagem pode ter uma ou mais camadas. As camadas são, de certa forma, independentes umas das outras.

### Container x Máquinas Virtuais

Container não é uma máquina virtual.

Contêineres e máquinas virtuais são tecnologias de virtualização de recursos muito semelhantes. A virtualização é o processo no qual um recurso singular do sistema, como RAM, CPU, Disco ou Rede, pode ser "virtualizado" e representado como vários recursos. 

O principal diferencial entre contêineres e máquinas virtuais é que as **VMs** virtualizam uma máquina inteira até as camadas de hardware, enquanto os **contêineres** virtualizam apenas camadas de software acima do nível do sistema operacional.

Quando abordamos temas como virtualização ou mesmo containers, temos um conceito em comum, a máquina hospedeira. A máquina hospedeira é a máquina pela qual as máquinas virtuais e/ou os containers executam, já a máquina convidada é somente a máquina virtual dentro de uma hospedeira.

<img src="https://github.com/douglas-vp/curso-docker/blob/main/images/contianer_vm.png" alt="Container x VM">

**Primeira Camada**
No nível mais baixo temos a infraestrutura, que pode ser nossa própria máquina ou um servidor.

**Segunda Camada**
Para máquinas que rodarão suas aplicações em containers temos apenas o sistema operacional, já para aqueles que rodarão máquinas virtuais temos a figura do Hypervisor, que pode ser o próprio sistema (XEN, KVM ou VMWare) ou uma aplicação dentro do sistema operacional (VirtualBox, KVM, Hyper-V).

**Terceira Camada**
Não colocamos uma terceira camada nas máquinas virtuais pois não há uma definição clara a respeito de Hypervisors do tipo 1 e do tipo 2, principalmente com o surgimento do KVM. Do lado dos containers aparece a figura do Container Runtime, que no nosso caso podemos entender como o Docker que veremos mais adiante, mas é interessante saber que existem outras ferramentas para criar containers no Linux.

Container runtimes são implementações de baixo nível, elas que de fato criam os containers no sistema operacional, geralmente utilizados por uma Container Engine, por exemplo, o Docker, RKT, LXD ou CRI-O.

**Última Camada**
Na última camada temos os nossos containers ou as nossas máquinas virtuais, cada qual com suas devidas aplicações. As máquinas virtuais são sistemas completos, com todos os seus processos, drivers e kernel, quando iniciam verificam se todo o hardware está funcional, fazem o boot do sistema operacional e então começam a rodar as aplicações. Já os containers, por sua vez, apenas iniciam a aplicação, compartilhando o kernel com o sistema hospedeiro.

### Quando utilizar VMs:
* Quando o sistema operacional a ser executado não é um Linux, por exemplo um Unix, ou um Windows;
* Quando procura-se um nível de persistência de dados maior do que os próprios dados da aplicação;
* Quando a arquitetura da aplicação for diferente da arquitetura da máquina hospedeira, por exemplo amd64 vs arm64, ou mesmo x86;
* Quando a aplicação for antiga (legada) e sua forma de trabalho é completamente monolítica (sem sessão externa, banco local, etc).

### Quando utilizar containers

* Quando construirmos aplicações “voltadas para cloud”, ou seja, podem trabalhar em qualquer lugar;
* Quando estamos criando microsserviços;
* Quando queremos aplicar práticas DevOps ou de CI/CD de forma mais agressiva;
* Quando o projeto é escalável e pode se espalhar em uma infraestrutura que compartilha o mesmo sistema operacional;

### ***Uma das grandes vantagens na adoção dos contêineres é a padronização criada pela "Open Container Initiative" que garante compatibilidade entre diferentes ferramentas, evitando que fiquemos presos a um único fornecedor.***

### Modelo bimodal

Gerência de dois estilos de trabalho diferentes mas coerentes.

* O primeiro com foco em previsibilidade e manutenção dos ambientes para o mundo digital.
* O segundo com foco em ploração, ou inovação. Tentam solucionar novos problemas, trabalham com incerteza.

### Monolito

Monolito em TI é um software composto de um único grande pedaço, quase sempre em uma única linguagem.

* **Vantagem**: mais fácil de desenvolver e mais simples de provisionar e testar.
* **Desvantagem**: uma mínima alteração exige teste em todo o pacote, recompilação e reprovisionamento completo.

### SOAP (Simṕle object access protocol)

Protocolo de troca de informações baseado e XML utilizando RPC ou HTTP.

### SOA (Service Oriented Architecture)

Padrão de arquitetura de software onde as funcionalidades são disponibilizadas na forma de serviços, geralmente distribuidos.

### ESB (Enterprise Service Bus)

Implementa a comunicação entre aplicações que interagem entre si no SOA. É responsável por interpretar e traduzir mensagens entre as aplicações.

### Microsserviços

Microserviço é um tipo de arquitetura de software que organiza a aplicação em uma coleção de serviços fracamente acoplados.

Microsserviços são uma variação do SOA sem a figura do ESB, a comunicação é direta e padronizada.

### Vantagens:
* Aplicações mais resilientes, sem o gargalo ou SPOF do ESB
* Fraca acoplação, componentes de diferentes tecnologias
* Fácil escalabilidade, já que são independentes


### SLA / SLO (Orquestradores)

**SLA**: Service-level Agreement, o nível de serviço prestado entre duas partes. Uma espécie de direitos e deveres.

**SLO**: Service-level objective mensura os acordos específicos no SLA.

### Orquestradores

Gerenciam e monitoram os containers. Fornecem self-healing para restaurar os containers com problemas. O **Self-healing** permite que uma aplicação tenha ciência sobre seu estado e seja reprovisionada caso ocorra um problema.

O **Autoscaling** aumenta ou diminui a quantidade de réplicas de um container para suprir uma determinada demanda.

O **Service Discovery** quando uma aplicação é adicionada ao cluster, existe um mecanismo para encontrá-la de forma automática.

O **Rolling Update** uma atualização acontece em apenas uma parte das réplicas e não se espalaha em caso de problemas.

### Sysadmin

O papel do sysadmin, ou o time de operações, é trabalhar com os orquestradores, como Kubernetes ou Swarm, e também trabalhar com as máquinas que possuem contêineres soltos, que apesar de não ser o cenário ideal, é bastante comum. Isso significa que saber criar as imagens não é essencial, essencial é conseguir levantar ambientes de testes, rodar contêineres locais ou em um orquestrador, entender como estes contêineres se comunicam e como os dados são persistidos em volumes. Além do mais, é papel dos administradores de sistema aplicar alguma forma de observabilidade nas aplicações para poder auxiliar o time de desenvolvimento em relação a melhores práticas relacionadas a comunicação, limites de memória/CPU além de possíveis alternativas para contornar instabilidades.

### Programador

O papel do programador, ou do time de desenvolvimento, é criar imagens e testá-las. Isso inclui praticamente todos os comandos e possibilidades disponíveis no Docker. A maioria dos testes mais básicos acontecem localmente, sendo assim é essencial criar imagens, levantar ambientes de testes e rodar contêineres locais. Também é preciso entender a respeito de sessões e volumes distribuídos, bem como configurações externas a aplicação e variáveis de ambiente. Um pouquinho de conhecimento em orquestradores fará bem, cedo ou tarde será necessário.

### DBA

Os DBAs também estão fadados a trabalhar com contêineres, apesar de ser um pouco menos comum, nos últimos anos as comunidades do MySQL, MongoDB e PostgreSQL criaram formas de automatizar e gerenciar os bancos dentro do Kubernetes através do que chamamos de Operators, controlando-os de uma maneira mais inteligente e facilitando tarefas como backups e replicação. Então um DBA precisa entender como levantar ambientes de testes, rodar contêineres locais e aprender o funcionamento dos orquestradores e estas novas possibilidades de administração.

### Docker

Docker é uma plataforma de código aberto, escrita em Go, que utiliza virtualização em nível do sistema operacional para construir, provisionar e gerenciar aplicações em um formato conhecido
como contêineres. De forma simplista, Docker é uma ferramenta para criar contêineres. o Docker uniu a facilidade em manipular contêineres, que já existia de certa forma na época, com a simplicidade de criar, transferir, provisionar e compartilhar imagens.

### Principais comandos Docker














