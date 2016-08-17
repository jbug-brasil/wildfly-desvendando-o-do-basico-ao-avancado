# Instalação passo a passo

  Neste capítulos iremos abordar a instalação do WildFly partindo do princípio que os downloads descritos no capítulo anterior já foram realizados.

Bom, como todos nós temos o direito de escolha, para ilustrar os exemplos deste tópico e dos demais irei usar a seguinte configuração:

* Sistema Operacional: Fedora 23 x86_64, Server Edition
* Banco de dados: MariaDB 10.0.25-1.fc23

Obs: O banco de dados não será necessário neste primeiro momento, mas será utilizado em capítulos futuros.


##### Primeiro passo: Definindo um usuário para Runtime

  Segurança em primeiro lugar, evite ao máximo utilizar o usuário **root** para executar o WildFly porque desta forma estaremos protegendo o servidor como um todo de forma que uma aplicação que permita execução de códigos arbritrários não execute nada no servidor com um usuário privilegiado.
  Neste case utilizarei um usuário chamado **wildfly**, para criar o usuário execute o seguinte comando:
  
  ```
  # useradd wildfly
  ```


##### Segundo passo: Escolhendo o diretório de instalação

  Esta é realmente a primeira dúvida que temos ao realizar a instalação de qualquer aplicação em nossos servidores, com o WildFly não é diferente. Em poucas palavras, não existe um padrão definido que todos devem seguir, porém muitos administradores acabam escolhendo um determinado modelo a seguir para que todos os servidores possuam os mesmos diretórios/estrutura, isso que, facilita e muito a administração.
  
  Eu sempre costumo usar o diretório **/opt**, lembrando, isto não é uma regra.
  Vamos agora descompactar o WildFly no diretório escolhido:

```
# tar -xzvf wildfly-10.1.0.CR1.tar.gz --directory /opt
```

Ou se prefere utilizar o arquivo com extensão *.zip*:

```
unzip wildfly-10.1.0.CR1.zip -d /opt
```

Neste momento já temos o servidor WildFLy descompactado no diretório **/opt**:

```
# ll /opt
total 0
drwxr-xr-x. 10 root root 220 Jul 28 01:02 wildfly-10.1.0.CR1
```

Note que as permissões de usuário e grupo estão configuradas para o usuário **root**, como boas práticas não iremos utilizar o usuário **root** para execução do WildFly, e sim o usuário criado anteriormente, altere as permissões com o seguinte comando:

```
# chown -R wildfly. /opt/wildfly-10.1.0.CR1/
```

Agora podemos utilizar o usuário **wildfly** para executar o Servidor.
Abra um shell utilizando este usuário e em seguida acesso o diretório *wildfly-10.1.0.CR1*:

```
[root@wfly-server ~]# su - wildfly
[wildfly@wfly-server ~]$ cd /opt/wildfly-10.1.0.CR1/
[wildfly@wfly-server wildfly-10.1.0.CR1]$ bin/standalone.sh
```

Com os comandos executados acima estamos:
* logando com o usuário **wildfly**
* Acessando o *JBOSS_HOME*
* Iniciando o WIldFLy

Caso ocorra tudo bem durante a inicialização do WildFly você terá um log muito semelhante a este: 

```
[wildfly@wfly-server wildfly-10.1.0.CR1]$ bin/standalone.sh 
=========================================================================

  JBoss Bootstrap Environment

  JBOSS_HOME: /opt/wildfly-10.1.0.CR1

  JAVA: java

  JAVA_OPTS:  -server -Xms64m -Xmx512m -XX:MetaspaceSize=96M -XX:MaxMetaspaceSize=256m -Djava.net.preferIPv4Stack=true -Djboss.modules.system.pkgs=org.jboss.byteman -Djava.awt.headless=true

=========================================================================

12:32:31,463 INFO  [org.jboss.modules] (main) JBoss Modules version 1.5.2.Final
12:32:36,598 INFO  [org.jboss.msc] (main) JBoss MSC version 1.2.6.Final
12:32:37,713 INFO  [org.jboss.as] (MSC service thread 1-4) WFLYSRV0049: WildFly Full 10.1.0.CR1 (WildFly Core 2.2.0.CR9) starting
12:33:08,472 INFO  [org.jboss.as.server] (Controller Boot Thread) WFLYSRV0039: Creating http management service using socket-binding (management-http)
12:33:09,280 INFO  [org.xnio] (MSC service thread 1-4) XNIO version 3.4.0.Beta3
12:33:09,424 INFO  [org.xnio.nio] (MSC service thread 1-4) XNIO NIO Implementation Version 3.4.0.Beta3
12:33:10,453 INFO  [org.jboss.as.clustering.infinispan] (ServerService Thread Pool -- 38) WFLYCLINF0001: Activating Infinispan subsystem.
12:33:11,294 INFO  [org.jboss.as.naming] (ServerService Thread Pool -- 46) WFLYNAM0001: Activating Naming Subsystem
12:33:11,259 INFO  [org.jboss.as.jsf] (ServerService Thread Pool -- 44) WFLYJSF0007: Activated the following JSF Implementations: [main]
12:33:11,960 WARN  [org.jboss.as.txn] (ServerService Thread Pool -- 54) WFLYTX0013: Node identifier property is set to the default value. Please make sure it is unique.
12:33:12,665 INFO  [org.jboss.as.naming] (MSC service thread 1-3) WFLYNAM0003: Starting Naming Service
12:33:12,893 INFO  [org.jboss.as.security] (ServerService Thread Pool -- 53) WFLYSEC0002: Activating Security Subsystem
12:33:12,900 INFO  [org.jboss.as.webservices] (ServerService Thread Pool -- 56) WFLYWS0002: Activating WebServices Extension
12:33:12,897 INFO  [org.wildfly.extension.io] (ServerService Thread Pool -- 37) WFLYIO001: Worker 'default' has auto-configured to 4 core threads with 32 task threads based on your 2 available processors
12:33:13,773 INFO  [org.jboss.as.security] (MSC service thread 1-4) WFLYSEC0001: Current PicketBox version=4.9.6.Final
12:33:13,872 INFO  [org.jboss.as.connector.subsystems.datasources] (ServerService Thread Pool -- 33) WFLYJCA0004: Deploying JDBC-compliant driver class org.h2.Driver (version 1.3)
12:33:16,526 INFO  [org.jboss.remoting] (MSC service thread 1-1) JBoss Remoting version 4.0.21.Final
12:33:16,550 INFO  [org.jboss.as.connector] (MSC service thread 1-2) WFLYJCA0009: Starting JCA Subsystem (WildFly/IronJacamar 1.3.4.Final)
12:33:17,059 INFO  [org.jboss.as.mail.extension] (MSC service thread 1-2) WFLYMAIL0001: Bound mail session [java:jboss/mail/Default]
12:33:17,359 INFO  [org.wildfly.extension.undertow] (MSC service thread 1-1) WFLYUT0003: Undertow 1.4.0.CR4 starting
12:33:17,405 INFO  [org.jboss.as.connector.deployers.jdbc] (MSC service thread 1-4) WFLYJCA0018: Started Driver service with driver-name = h2
12:33:19,060 INFO  [org.wildfly.extension.undertow] (ServerService Thread Pool -- 55) WFLYUT0014: Creating file handler for path '/opt/wildfly-10.1.0.CR1/welcome-content' with options [directory-listing: 'false', follow-symlink: 'false', case-sensitive: 'true', safe-symlink-paths: '[]']
12:33:20,814 INFO  [org.wildfly.extension.undertow] (MSC service thread 1-1) WFLYUT0012: Started server default-server.
12:33:21,160 INFO  [org.wildfly.extension.undertow] (MSC service thread 1-3) WFLYUT0018: Host default-host starting
12:33:22,573 INFO  [org.jboss.as.ejb3] (MSC service thread 1-3) WFLYEJB0481: Strict pool slsb-strict-max-pool is using a max instance size of 32 (per class), which is derived from thread worker pool sizing.
12:33:22,575 INFO  [org.jboss.as.ejb3] (MSC service thread 1-2) WFLYEJB0482: Strict pool mdb-strict-max-pool is using a max instance size of 8 (per class), which is derived from the number of CPUs on this host.
12:33:23,793 INFO  [org.wildfly.extension.undertow] (MSC service thread 1-1) WFLYUT0006: Undertow HTTP listener default listening on 127.0.0.1:8080
12:33:26,356 INFO  [org.infinispan.factories.GlobalComponentRegistry] (MSC service thread 1-1) ISPN000128: Infinispan version: Infinispan 'Chakra' 8.2.3.Final
12:33:26,456 WARN  [org.jboss.as.domain.management.security] (MSC service thread 1-2) WFLYDM0111: Keystore /opt/wildfly-10.1.0.CR1/standalone/configuration/application.keystore not found, it will be auto generated on first use with a self signed certificate for host localhost
12:33:26,582 INFO  [org.infinispan.configuration.cache.EvictionConfigurationBuilder] (ServerService Thread Pool -- 61) ISPN000152: Passivation configured without an eviction policy being selected. Only manually evicted entities will be passivated.
12:33:26,583 INFO  [org.infinispan.configuration.cache.EvictionConfigurationBuilder] (ServerService Thread Pool -- 61) ISPN000152: Passivation configured without an eviction policy being selected. Only manually evicted entities will be passivated.
12:33:26,612 INFO  [org.jboss.as.server.deployment.scanner] (MSC service thread 1-2) WFLYDS0013: Started FileSystemDeploymentService for directory /opt/wildfly-10.1.0.CR1/standalone/deployments
12:33:26,673 INFO  [org.infinispan.configuration.cache.EvictionConfigurationBuilder] (ServerService Thread Pool -- 61) ISPN000152: Passivation configured without an eviction policy being selected. Only manually evicted entities will be passivated.
12:33:26,674 INFO  [org.infinispan.configuration.cache.EvictionConfigurationBuilder] (ServerService Thread Pool -- 61) ISPN000152: Passivation configured without an eviction policy being selected. Only manually evicted entities will be passivated.
12:33:26,672 INFO  [org.infinispan.configuration.cache.EvictionConfigurationBuilder] (ServerService Thread Pool -- 59) ISPN000152: Passivation configured without an eviction policy being selected. Only manually evicted entities will be passivated.
12:33:26,693 INFO  [org.infinispan.configuration.cache.EvictionConfigurationBuilder] (ServerService Thread Pool -- 59) ISPN000152: Passivation configured without an eviction policy being selected. Only manually evicted entities will be passivated.
12:33:26,950 INFO  [org.jboss.as.connector.subsystems.datasources] (MSC service thread 1-4) WFLYJCA0001: Bound data source [java:jboss/datasources/ExampleDS]
12:33:28,091 INFO  [org.wildfly.extension.undertow] (MSC service thread 1-4) WFLYUT0006: Undertow HTTPS listener https listening on 127.0.0.1:8443
12:33:29,599 INFO  [org.jboss.ws.common.management] (MSC service thread 1-2) JBWS022052: Starting JBossWS 5.1.5.Final (Apache CXF 3.1.6) 
12:33:30,012 INFO  [org.jboss.as] (Controller Boot Thread) WFLYSRV0060: Http management interface listening on http://127.0.0.1:9990/management
12:33:30,013 INFO  [org.jboss.as] (Controller Boot Thread) WFLYSRV0051: Admin console listening on http://127.0.0.1:9990
12:33:30,013 INFO  [org.jboss.as] (Controller Boot Thread) WFLYSRV0025: WildFly Full 10.1.0.CR1 (WildFly Core 2.2.0.CR9) started in 4417ms - Started 331 of 577 services (393 services are lazy, passive or on-demand)
```

