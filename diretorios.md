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
  │   │   └── configs
  │   ├── licenses
  │   └── schema
  ├── domain
  │   ├── configuration
  │   ├── data
  │   └── tmp
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

* **appclient** - asfsdasd


* **bin** - Todos os binários do servidor serão encontratos neste diretório, tais como standalone/domain.sh|bat, script para adição de usuários, etc.
  * **client** - Neste subdiretório está armazenados as bibliotecas necessárias para se conectar ao Wildfly utilizando JBoss CLI, EJB ou JMS.


* **docs** - Aqui você irá encontrar diversos tipos de arquivos como exemplos de configuração, exemplos se como executar o WildFLy como serviço, licenças e outros arquivos que lhe ajudarão a aprender mais sobre o WildFly.
  * **contrib** - Arquivos utilizados para executar o WildFly como serviço.
    * **scripts** - Scripts para configuração do WildFly como serviço.
      * **init.d** - Arquivos necessários para executar como serviço no Linux Linux baseado no gerenciador de serviços **init.d**.
      * **service** - Arquivos necessários para executar como serviço no Windows
      * **systemd** - Arquivos necessários para executar como serviço no Linux baseado no gerenciador de serviços **systemd**.
  * **examples** - 
    * **configs** - 
  * **licenses** - 
  * **schema** - 


* **domain** - 
* **configuration** - 
* **data** - 
* **tmp** - 
* **modules** - 
* **standalone** - 
* **configuration** - 
* **standalone_xml_history** - 
* **current** - 
* **snapshot** - 
* **data** - 
* **deployments** - 
* **lib** - 
* **log** - 
* **tmp** - 
* **welcome-content** - 

