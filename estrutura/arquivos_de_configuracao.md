# Arquivos de configuração

Desde o JBoss AS 7, a configuração é centralizada o que, de certa forma facilita muito o gerenciamento do seu servidor ou parque de servidores.

A estrutura, quando comparada com o JBoss AS 7 não teve alterações, porém se você ainda não a conhece irá achar um pouco estranho a forma como está distribuída agora. QUando comparada com a versões mais antigas do JBoss, temo uma grande diferença, principalmente porque os arquivos de configuração eram diversos, em diferentes diretórios, componentes, etc. Se você está migrando do JBoss AS 6 ou versões anteriores, é de extrema importância que você leia este capítulo para ficar antenado com a estrutura dos arquivos de configuração do WildFly.

O intuíto deste tópico será somente descrever os principais arquivos de configurações e sua aplicabilidade, será tratado em tópicos posteriores como configurar o WildFly.

Para facilitar assunto, o livro dividiremos em três partes:
* Configurações em geral;
* Configurações do modo standalone;
* Configurações do modo domínio.

## Configurações Gerais

Iremos começar com as confiugurações bem básicas que são as configurações realizadas dentro do diterório _bin_. Nele temos os seguintes arquivos de configuração:

* _add-user.properties_ - Configuração da política de senha na criação de usuários
* _appclient.conf_ - Arquivo que define as configurações do _appclient_, utilitário para execução de applicações sem a necessidade de executar o WildFly
* _domain.conf_ - Define as configurações utilizadas para iniciar o modo domínio.
* _jboss-cli-logging.properties_ - Definições de log do JBoss CLI.
* _jboss-cli.xml_ - Define as configurações que serão utilizadas pelo JBoss CLI, através do script _jboss-cli.sh_ tais como _connection timeout_ e _controller_.
* _standalone.conf_ - Define as configurações utilizadas para iniciar o modo standalone.

_Obs_: O wildFly 10 já possui suporte ao _PowerShell_, note que já há vários scripts com o sufixo _ps1_ no diretório *bin*.

## Configurações modo Standalone

Todos os arquivos de configuração do modo _Standalone_ estão no diretório _$JBOSS_HOME/standalone/configuration_, neste diretório iremos encontrar os seguintes arquivos:

* _application-roles.properties_: Neste arquivo é configurado as permissões (Roles) dos usuários utilizados em aplicações.
* _application-users.properties_: Armazena usuários utilizados para autenticação realizada por aplicações.
* _logging.properties_: Arquivo que define as configurações de log do Wildfly, este arquivo é alterado de acordo com as definições de logging realizadas no subsystem *logging*.
* _mgmt-groups.properties_: Grupos dos usuários de gerenciamento, note os grupos são usados quando o _RBAC_ (_Role Based Access Control_, falaremos sobre isso nos próximos capítulos) ou Controle de Acesso Baseado em Roles.
* _mgmt-users.properties_: Define usuários e senha utilizados para autenticar usuários de gerenciamento.
* _standalone.xml_: Todas as definições e configurações do Wildfly são feitas através deste arquivo.

## Configurações modo Domínio

No modo _Domain_ temos os mesmos arquivos de configuração com a exceção do _standalone.xml_ e adição dos seguintes arquivos:

* _domain.xml_: Define todas as configurações do modo domínio. Emn adição ao domain.xml temos mais 3 arquivos:
* _host-master.xml_: Este arquivo define as configuração da instância do WildFly que irá atuar somente como Controlador de Domínio.
* _host-slave.xml_: Um modo domínio distribuído tem seus host masters e slaves, este arquivo define as configurações do slaves.
* _host.xml_: Se por acaso desejar executar o WildFly no modo domínio em somente um servidor, é neste arquivo que estará contidos todas as informações referentes ao host. Note que também é possível utilizá-lo como host master ou slave.
* _default-server-logging.properties_: Arquivo que define as configurações de log padrão dos servidores gerenciados.
