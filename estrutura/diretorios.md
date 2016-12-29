# Diretórios

O WildFly manteve praticamente a mesma estrutura de diretórios do JBoss AS 7, enxuta e centralizada. Para aqueles que ainda não estão familiarizados com essa nova estrutura, a próxima seção descreverá em detalhes abaixo.

## Como está dividia a estrutura?

Bom, temos a seguinte estrutura de diretórios:
```
$JBOSS_HOME
  ├── appclient
  ├── bin
  │   ├── client
  ├── docs
  │   ├── contrib
  │   │   └── scripts
  │   │       ├── init.d
  │   │       ├── service
  │   │       └── systemd
  │   ├── examples
  │   ├── licenses
  │   └── schema
  ├── domain
  │   ├── configuration
  │   │   └── domain_xml_history
  │   │       ├── current
  │   │       ├── snapshot
  │   ├── data
  │   └── tmp
  │   └── servers
  ├── modules
  ├── standalone
  │   ├── configuration
  │   │   └── standalone_xml_history
  │   │       ├── current
  │   │       ├── snapshot
  │   ├── data
  │   ├── deployments
  │   ├── lib
  │   ├── log
  │   └── tmp
  └── welcome-content
```
Veremos agora a função de cada diretório e o que é armazenado em cada um:

* _appclient_ - Este diretório é utilizado para armazenar arquivos de deployments, configuração e também utilizado como área de escrita utilizados pelo __application client container__.
* _bin_ - Todos os binários do servidor serão encontratos neste diretório, tais como standalone/domain.sh|bat, script para adição de usuários, etc.
  * _client_ - Neste subdiretório está armazenados as bibliotecas necessárias para se conectar ao Wildfly utilizando JBoss CLI, EJB ou JMS.
* _docs_ - Aqui você irá encontrar diversos tipos de arquivos como exemplos de configuração, exemplos se como executar o WildFLy como serviço, licenças e outros arquivos que lhe ajudarão a aprender mais sobre o WildFly.
  * _contrib_ - Arquivos utilizados para executar o WildFly como serviço.
    * _scripts_ - Scripts para configuração do WildFly como serviço.
      * _init.d_ - Arquivos necessários para executar como serviço no Linux Linux baseado no gerenciador de serviços **init.d**.
      * _service_ - Arquivos necessários para executar como serviço no Windows
      * _systemd_ - Arquivos necessários para executar como serviço no Linux baseado no gerenciador de serviços **systemd**.
    * _examples_ - Contém exempls arquivos de configuração do modo standaloe pré configurados.
    * _licenses_ - Contém todas as licenças sob o qual o código fonte do WildFLy está protegido.
    * _schema_ - São os arquivos que definem as configurações/parâmetros aceitos nos *subsystems* presentes nos arquivos de configuração do Wildly, note que sua nomenclatura contém a versão do schema, asim como no arquivo de configuração contém a versão do schema que será utilizado para a configuração de determinado *subsystem*, Exemplo: Dado o seguinte *subsystem*: 
    ```xml
    <subsystem xmlns="urn:jboss:domain:logging:3.0">
    ```
    Note que ele está utilizando a versão 3.0 do schema **logging**. Este mesmo padrão é válido para todos os outros *subsystems*.
* _domain_ - Abriga toda a configuração do modo domain bem como os arquivos dos servidores gerenciados (veremos melhor sobre isso mais a frente) e arquivos de deployments, arquivos temporários e arquivos de logs.
  * _configuration_ - Contém todos os arquivos de configuração do modo domínio.
      * _domain_xml_history_ - Contém todo o histórico dos arquivos de configuração.
        * _current_ - Armazena a configuração corrente com sufixos v1, v2, vX.
        * _snapshot_ - Armazena os snapshots, obtidos através do comando *CLI* **/host=HOSTNAME:take-snapshot**
  * _servers_ - Diretório utilizado para armazenar informações referentes aos servidores gerenciados controlados pelo domínio em questão. Dentro do diretório com o respectivo nome do servidor gerenciado existem também seus subdiretórios **data**, **tmp** e **log** cujo o objetivo é o mesmo do descrito no modo *standalone*.
  * _data_ - Diretório utilizado para persistir dados para que seja possível um restart sem perda de imformação.
  * _tmp_ - Utilizado e gerado em Runtime, reponsável por armazenar todos os arquivos temporários gerados durante a execução do servidor.
  * _lib/ext_ - Local utilizado para instalar bibliotecas utilizadas pelas aplicações através do mecanismo **Extension-List**.
* _modules_ - O WildFly é baseado em um *classloader* modular (explicado em detalhes nos próximos tópicos), todos os módulos necessários para a execução do WildFly estão armazenados neste diretório, bem como os módulos customizados.
* _standalone_ - Contém todos os arquivos necessários para a execuçaõ do WildFly no modo *standalone*.
  * _configuration_ - Contém todo o histórico dos arquivos de configuração.
    * _standalone_xml_history_ - Contém todo o histórico dos arquivos de configuração.
      * _current_ -  Armazena a configuração corrente com sufixos v1, v2, vX.
      * _snapshot_ - Armazena os snapshots, obtidos através do comando *CLI* **:take-snapshot**
  * _data_ -  Diretório utilizado para persistir dados para que seja possível um restart sem perda de imformação.
  * _deployments_ - Existente somente no modo *standalone* é utilizado para realizar deployments utilizando o método **Deployment Scanner**.
  * _lib/ext_ - Local utilizado para instalar bibliotecas utilizadas pelas aplicações através do mecanismo **Extension-List**.
  * _log_ - Contém os logs do servidor em execuçaõ.
  * _tmp_ - Diretório para escrita de arquivos temporários utilizados pelas aplicações em execução.
* _welcome-content_ - É um diretório de uso interno do servidor que não deve ser modificado por usuários finais, sua alteração pode influenciar no funcionamento do WildFly bem como páginas de boas vindas e páginas de erros.