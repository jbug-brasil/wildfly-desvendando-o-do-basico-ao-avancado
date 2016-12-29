# Configurando WildFly 10

Nos próximos tópicos, iremos conhecer como configurar cada componente Java EE do Wildfly e seus componentes de infraestrutura (como logging), mas antes de darmos início é necessário entendermos como eles foram desenvolvidos no Wildfly.

Diferente de versões anteriores, o Wildfly centralizou a configuração do servidor em um (no máximo dois em modo Domain) arquivo de configuração e que através dele é possível configurar qualquer coisa dentro do servidor. Na verdade, se considerarmos o que seria o Wildfly, ele é simplesmente uma espécie de Kernel do Wildly (conhecido como _Wildfly Core_) onde é possível adicionar funcionalidades a ele (permitindo assim a extensibilidade na sua arquitetura interna). Para suas funcionalidades foi introduzido os conceitos de _extension_ e _subsystem_, que são os blocos lógicos para adicionar/remover das funcionalidades do servidor e sua configuração. Mas o que significa esses dois conceitos? Veremos em detalhes a seguir.

## Extension

O Extension do Wildfly é a forma como o Wildfly Core pode reconhecer novas funcionalidades e assim agregar ao seu funcionamento principal. Basicamente, a função do extension é registrar uma funcionalidade para o Wildfly Core carregar em memória e também gerenciar o ciclo de vida dela. Por exemplo, as extensions listadas no perfil padrão (standalone.xml) são as seguintes:

* org.jboss.as.clustering.infinispan
* org.jboss.as.connector
* org.jboss.as.deployment-scanner
* org.jboss.as.ee
* org.jboss.as.ejb3
* org.jboss.as.jaxrs
* org.jboss.as.jdr
* org.jboss.as.jmx
* org.jboss.as.jpa
* org.jboss.as.jsf
* org.jboss.as.logging
* org.jboss.as.mail
* org.jboss.as.naming
* org.jboss.as.pojo
* org.jboss.as.remoting
* org.jboss.as.sar
* org.jboss.as.security
* org.jboss.as.transactions
* org.jboss.as.webservices
* org.jboss.as.weld
* org.wildfly.extension.batch.jberet
* org.wildfly.extension.bean-validation
* org.wildfly.extension.io
* org.wildfly.extension.request-controller
* org.wildfly.extension.security.manager
* org.wildfly.extension.undertow

## Subsystem

Subsystem nada mais é que a funcionalidade em si implementada e que é registrada no Wildfly Core pela Extenstion. Nela, é possível extender a funcionalidade através da configuração via xml. O Subsystem é onde realmente você terá o suporte a Servlets no Wildfly, EJB, Transações, Logging, etc. Como exemplo, abaixo temos a configuração do subsystem Logging:

```xml
        <subsystem xmlns="urn:jboss:domain:logging:3.0">
            <console-handler name="CONSOLE">
                <level name="INFO"/>
                <formatter>
                    <named-formatter name="COLOR-PATTERN"/>
                </formatter>
            </console-handler>
            <periodic-rotating-file-handler name="FILE" autoflush="true">
                <formatter>
                    <named-formatter name="PATTERN"/>
                </formatter>
                <file relative-to="jboss.server.log.dir" path="server.log"/>
                <suffix value=".yyyy-MM-dd"/>
                <append value="true"/>
            </periodic-rotating-file-handler>
            <logger category="com.arjuna">
                <level name="WARN"/>
            </logger>
            <logger category="org.jboss.as.config">
                <level name="DEBUG"/>
            </logger>
            <logger category="sun.rmi">
                <level name="WARN"/>
            </logger>
            <root-logger>
                <level name="INFO"/>
                <handlers>
                    <handler name="CONSOLE"/>
                    <handler name="FILE"/>
                </handlers>
            </root-logger>
            <formatter name="PATTERN">
                <pattern-formatter pattern="%d{yyyy-MM-dd HH:mm:ss,SSS} %-5p [%c] (%t) %s%e%n"/>
            </formatter>
            <formatter name="COLOR-PATTERN">
                <pattern-formatter pattern="%K{level}%d{HH:mm:ss,SSS} %-5p [%c] (%t) %s%e%n"/>
            </formatter>
        </subsystem>
```

## Interfaces

Interfaces são denominações lógicas para interfaces de rede que irão se associar aos sockets (ver próxima seção) para expor algum serviço de rede para os Subsystems. As Interfaces podem associar os sockets para um IP em específico ou até mesmo para uma NIC[^2] da máquina física, permitindo então dedicar o tráfego de rede dos Subsystems do Wildfly passar por uma interface específica de rede. Abaixo temos um exemplo de Interfaces:

```xml
    <interfaces>
        <interface name="public">
            <inet-address value="${jboss.bind.address:127.0.0.1}"/>
        </interface>
        <interface name="internal">
            <nic name="eth1"/>
        </interface>
    </interfaces>
```

## Histórico de alterações

Uma das maiores funcionalidades no Wildfly é o registro histórico de configurações. Dessa forma, se houver qualquer alteração nos arquivos de configuração (seja ela editando manualmente o arquivo, via JBoss CLI ou Console Web), o Wildfly irá criar um backup das alterações. Isso permite que no caso de alguma alteração afetar negativamente o ambiente é possível reverter a alteração apenas copiando a última versão alterada.

A estrutura de histório está descrita no capítulo [Diretórios](../../estrutura/diretorios.md). Para recuperar o arquivo, basta sobreesrcrever o atual com um dos snapshots que ficam dentro do diretório `snapshots` (o snapshot é o nome do arquivo de configuração seguido da data e hora de alteração).

[^2]: NIC = _Network Interface Card_, ou simplesmente Interface de Rede
[^3]: Definimos _offset_ a soma a ser colocada no número da porta de cada Socket Binding definido no grupo. Ex. Se definir um offset de 150 e a porta definida para o Socket Binding `http` é 8080, então o número da porta é 8230.