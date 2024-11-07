# Docker
**Container**: pacote de aplicação que funciona isoladamente do sistema operacional com todas as dependencias dentro de si. Aplicação contida que funciona no ambiente que está.

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

<img src="URL_da_Imagem" alt="Texto Alternativo">








