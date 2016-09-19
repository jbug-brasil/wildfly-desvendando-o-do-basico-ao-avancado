# Arquivos de configuração

Desde o JBoss AS 7, a configuração é centralizada o que, de certa forma facilita muito o gerenciamento do seu servidor ou parque de servidores.

A estrutura, quando comparada com o JBoss AS 7 não teve alterações, porém se você ainda não a conhece irá achar um pouco estranho a forma como está distribuída agora. QUando comparada com a versões mais antigas do JBoss, temo uma grande diferença, principalmente porque os arquivos de configuração eram diversos, em diferentes diretórios, componentes, etc. Se você está migrando do JBoss AS 6 ou versões anteriores, é de extrema importância que você leia este capítulo para ficar antenado com a estrutura dos arquivos de configuração do WildFly.

O intuíto deste tópico será somente descrever os principais arquivos de configurações e sua aplicabilidade, será tratado em tópicos posteriores *como* configurar o WildFly.

Para facilitar, irei dividir em três partes:
* Configurações em geral;
* Configurações do modo standalone;
* Configurações do modo domínio.


#### Configurações Gerais


Iremos começar com as confiugurações bem básicas que são as configurações realizadas dentro do diterório **bin**. Nele temos os seguintes arquivos de configuração:

* **add-user.properties** - Configuração da política de senha na criação de usuários


* **appclient.conf** - Arquivo que define as configurações do **appclient**, utilitário para execução de applicações sem a necessidade de executar o WildFly


* **domain.conf** - Define as configurações utilizadas para iniciar o modo domínio.


* **jboss-cli-logging.properties** - Definições de log do JBoss CLI.


* **jboss-cli.xml** - Define as configurações que serão utilizadas pelo JBoss CLI, através do script **jboss-cli.sh** tais como **connection timeout** e **controller**.


* **standalone.conf** - Define as configurações utilizadas para iniciar o modo standalone.


**Obs**: O wildFly 10 já possui suporte ao **PowerShell**, note que já há vários scripts com o sufixo **ps1** no diretório *bin*.


#### Configurações modo Standalone

Todos os arquivos de configuração do modo *Standalone* estão no diretório **$JBOSS_HOME/standalone/configuration**, neste diretório iremos encontrar os seguintes arquivos:

* **application-roles.properties**: Neste arquivo é configurado as permissões (Roles) dos usuários utilizados em aplicações.


* **application-users.properties**: Armazena usuários utilizados para autenticação realizada por aplicações.


* **logging.properties**: Arquivo que define as configurações de log do Wildfly, este arquivo é alterado de acordo com as definições de logging realizadas no subsystem *logging*.


* **mgmt-groups.properties**: Grupos dos usuários de gerenciamento, note os grupos são usasdos quando o **RBAC (Role Based Access Control)** ou Controle de Acesso Baseardo em Roles.


* **mgmt-users.properties**: Define usuários e senha utilizados para autenticar usuários de gerenciamento.


* **standalone.xml:


#### Configurações modo Domínio

No modo *Domínio* temos os mesmos arquivos de configuração com a exceção do **stadanloe.xml** e adição dos seguintes arquivos:



