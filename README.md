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

### ***O padrão é um diferencial na utilização de containers***

### Modelo bimodal

Gerência de dois estilos de trabalho diferentes mas coerentes.

* O primeiro com foco em previsibilidade e manutenção dos ambientes para o mundo digital.
* O segundo com foco em ploração, ou inovação. Tentam solucionar novos problemas, trabalham com incerteza.















