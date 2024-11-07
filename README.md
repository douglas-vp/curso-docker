# Docker
**Container**: pacote de aplicação que funciona isoladamente do sistema operacional com todas as dependencias dentro de si. Aplicação contida que funciona no ambiente que está.

### Tecnologias chave
**namespaces**: isolam os processos dos containers e tambem os pontos de montagem, diretórios, discos, redes...

**cgroups (control groups)**: limitam o acesso a recursos da máquina como CPU, memória e tráfego de rede.

**union mount**: características dos sistemas de arquivos que trabalham com camadas. Estas camadas pode ser compartilhadas.

### Imagens

Dentro da imagem está a aplicação, suas dependências, bibliotecas, binários e outros arquivos.
Uma imagem pode ter uma ou mais camadas. As camadas são, de certa forma, independentes umas das outras.






