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

* **appclient**
* **bin**
* **client**
* **docs**
* **contrib**
* **scripts**
* **init.d**
* **service**
* **systemd**
* **examples**
* **configs**
* **licenses**
* **schema**
* **domain**
* **configuration**
* **data**
* **tmp**
* **modules**
* **standalone**
* **configuration**
* **standalone_xml_history**
* **current**
* **snapshot**
* **data**
* **deployments**
* **lib**
* **log**
* **tmp**
* **welcome-content**

