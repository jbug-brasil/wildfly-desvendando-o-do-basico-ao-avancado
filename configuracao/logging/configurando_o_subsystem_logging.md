# Subsystem Logging

* Em modo Standalone: `WILDLFY_HOME/standalone/server/log`
* Em modo Domain: `WILDFLY_HOME/domain/servers/SERVIDOR/log/server.log`

## Configurando Logging

* Em modo Standalone: `WILDFLY_HOME/standalone/configuration/logging.properties`
* Em modo Domain: `WILDFLY_HOME/domain/servers/SERVIDOR/data/server.log`

## Inspecionando erros em tempo de bootstrap

```
/core-service=management:read-boot-errors
```

## Configurando Logging por aplicação

```xml
<dependency>
	<groupId>org.jboss.logging</groupId>
	<artifactId>jboss-logging</artifactId>
	<version>3.3.0.Final-redhat-1</version>
	<scope>provided</scope>
</dependency>
```

```java
import org.jboss.logging.Logger;
```

```java
private static final Logger LOGGER = Logger.getLogger(MinhaClasse.class);
```

```java
LOGGER.debug("debug");
LOGGER.info("info");
LOGGER.error("error");
LOGGER.trace("trace");
LOGGER.fatal("fatal");
```

* Para empacotamentos EAR, no diretório `META-INF`
* Para empacotamentos WAR, no diretório `WEB-INF/classes`

### Desabilitando Logging por aplicação

```
/subsystem=logging:write-attribute(name=use-deployment-logging-config,value=false)
```

## Visualizando arquivos de log