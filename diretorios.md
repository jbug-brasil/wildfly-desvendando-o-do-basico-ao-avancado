# Diretórios

O WildFly manteve a mesma estrutura de diretórios do JBoss AS 7, bastante enxuta e muito centralizada. Para aqueles que ainda não estão familiarizados com esta nova estrutura, abiaixo irei descrevê-la em detalhes.

#### Como está dividia a estrutura?

Bom, temos a seguinte estrutura de diretórios

```sh
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

* **appclient** - Este diretório é utilizado para armazenar arquivos de deployments, configuração e também utilizado como área de escrita utilizados pelo *application client container*.

* **bin** - Todos os binários do servidor serão encontratos neste diretório, tais como standalone/domain.sh|bat, script para adição de usuários, etc.
  * **client** - Neste subdiretório está armazenados as bibliotecas necessárias para se conectar ao Wildfly utilizando JBoss CLI, EJB ou JMS.

* **docs** - Aqui você irá encontrar diversos tipos de arquivos como exemplos de configuração, exemplos se como executar o WildFLy como serviço, licenças e outros arquivos que lhe ajudarão a aprender mais sobre o WildFly.
  * **contrib** - Arquivos utilizados para executar o WildFly como serviço.
    * **scripts** - Scripts para configuração do WildFly como serviço.
      * **init.d** - Arquivos necessários para executar como serviço no Linux Linux baseado no gerenciador de serviços **init.d**.
      * **service** - Arquivos necessários para executar como serviço no Windows
      * **systemd** - Arquivos necessários para executar como serviço no Linux baseado no gerenciador de serviços **systemd**.
  * **examples** - Contém exempls arquivos de configuração do modo standaloe pré configurados.
  * **licenses** - Contém todas as licenças sob o qual o código fonte do WildFLy está protegido.
  * **schema** - São os arquivos que definem as configurações/parâmetros aceitos nos *subsystems* presentes nos arquivos de configuração do Wildly, note que sua nomenclatura contém a versão do schema, asim como no arquivo de configuração contém a versão do schema que será utilizado para a configuração de determinado *subsystem*, Exemplo: Dado o seguinte *subsystem*: 
   
    ```xml
    <subsystem xmlns="urn:jboss:domain:logging:3.0">
    ```
    Note que ele está utilizando a versão 3.0 do schema **logging**. Este mesmo padrão é válido para todos os outros *subsystems*.
   
    
* **domain** - Abriga toda a configuração do modo domain bem como os arquivos dos servidores gerenciados (veremos melhor sobre isso mais a frente) e arquivos de deployments, arquivos temporários e arquivos de logs.
  * **configuration** - Contém todos os arquivos de configuração do modo domínio.
      * **domain_xml_history** - Contém todo o histórico dos arquivos de configuração.
        * **current** - Armazena a configuração corrente com sufixos v1, v2, vX.
        * **snapshot** - Armazena os snapshots, obtidos através do comando *CLI* **/host=HOSTNAME:take-snapshot**
  * **servers** - Diretório utilizado para armazenar informações referentes aos servidores gerenciados controlados pelo domínio em questão. Dentro do diretório com o respectivo nome do servidor gerenciado existem também seus subdiretórios **data**, **tmp** e **log** cujo o objetivo é o mesmo do descrito no modo *standalone*.
  * **data** - Diretório utilizado para persistir dados para que seja possível um restart sem perda de imformação.
  * **tmp** - Utilizado e gerado em Runtime, reponsável por armazenar todos os arquivos temporários gerados durante a execução do servidor.
  * **lib/ext ** - Local utilizado para instalar bibliotecas utilizadas pelas aplicações através do mecanismo **Extension-List**.

* **modules** - O WildFly é baseado em um *classloader* modular (explicado em detalhes nos próximos tópicos), todos os módulos necessários para a execução do WildFly estão armazenados neste diretório, bem como os módulos customizados.


* **standalone** - Contém todos os arquivos necessários para a execuçaõ do WildFly no modo *standalone*.
  * **configuration** - Contém todo o histórico dos arquivos de configuração.
    * **standalone_xml_history** - Contém todo o histórico dos arquivos de configuração.
      * **current** -  Armazena a configuração corrente com sufixos v1, v2, vX.
      * **snapshot** - Armazena os snapshots, obtidos através do comando *CLI* **:take-snapshot**
  * **data** -  Diretório utilizado para persistir dados para que seja possível um restart sem perda de imformação.
  * **deployments** - Existente somente no modo *standalone* é utilizado para realizar deployments utilizando o método **Deployment Scanner**.
  * **lib/ext ** - Local utilizado para instalar bibliotecas utilizadas pelas aplicações através do mecanismo **Extension-List**.
  * **log** - Contém os logs do servidor em execuçaõ.
  * **tmp** - Diretório para escrita de arquivos temporários utilizados pelas aplicações em execução.
* **welcome-content** - 
