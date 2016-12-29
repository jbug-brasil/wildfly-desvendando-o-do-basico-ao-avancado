# Subsystem datasources

```xml
<subsystem xmlns="urn:jboss:domain:datasources:4.0">
    <datasources>
        <datasource jndi-name="java:jboss/datasources/ExampleDS" pool-name="ExampleDS">
            <connection-url>jdbc:h2:mem:test;DB_CLOSE_DELAY=-1</connection-url>
            <driver>h2</driver>
            <pool>
                <min-pool-size>10</min-pool-size>
                <max-pool-size>20</max-pool-size>
                <prefill>true</prefill>
            </pool>
            <security>
                <user-name>sa</user-name>
                <password>sa</password>
            </security>
        </datasource>
        <xa-datasource jndi-name="java:jboss/datasources/ExampleXADS" pool-name="ExampleXADS">
           <driver>h2</driver>
           <xa-datasource-property name="URL">jdbc:h2:mem:test</xa-datasource-property>
           <xa-pool>
                <min-pool-size>10</min-pool-size>
                <max-pool-size>20</max-pool-size>
                <prefill>true</prefill>
           </xa-pool>
           <security>
                <user-name>sa</user-name>
                <password>sa</password>
           </security>
        </xa-datasource>
        <drivers>
            <driver name="h2" module="com.h2database.h2">
                <xa-datasource-class>org.h2.jdbcx.JdbcDataSource</xa-datasource-class>
            </driver>
        </drivers>
  </datasources>
 
</subsystem>
```

## Utilizando driver JDBC como deployment

* Baixe o Driver JDBC
* Se o Driver JDBC do fornecedor ainda não é compatível com a versão JDBC 4, veja na seção [Tornando o Driver JDBC compatível com a versão 4](#tornando-o-driver-jdbc-compatível-com-a-versão-4) para converter o Driver.
* Faça o deploy do Driver JDBC:

```bash
$ EAP_HOME/bin/jboss-cli.sh
$ deploy driver-jdbc.jar
```

* Caso o deploy tenha sido feito com sucesso, você verá a seguinte mensagem no log do servidor:

```
WFLYJCA0018: Started Driver service with driver-name = jdbc-driver.jar_com.sua.classe.jdbc
```


## Instalando driver JDBC como módulo

* Baixe o Driver JDBC
* Se o Driver JDBC do fornecedor ainda não é compatível com a versão JDBC 4, veja na seção [Tornando o Driver JDBC compatível com a versão 4](#tornando-o-driver-jdbc-compatível-com-a-versão-4) para converter o Driver.
* Execute o JBoss CLI

```bash
$ EAP_HOME/bin/jboss-cli.sh
```

* No prompt do JBoss CLI, execute o seguinte comando:

```
module add --name=MODULE_NAME --resources=PATH_TO_JDBC_JAR --dependencies=DEPENDENCIES
```

Um exemplo para adicionar o Driver JDBC seria assim:

```
module add --name=com.mysql --resources=/caminho/do/mysql-connector-java-5.1.36-bin.jar --dependencies=javax.api,javax.transaction.api
```

* Ao executar o comando anterior, o Wildfly irá:
    * Criar um subdiretório WILDFLY_HOME/modules/com/seu/modulo/jdbc/main
    * Copiar o JAR dentro desse diretório
    * Criar um arquivo _module.xml_ contendo a configuração para o módulo (Veja a seção [Adicionando um módulo customizado](../classloader/modulo_customizado.html#adicionando-um-módulo-customizado) para maiores detalhes)

* Conecte-se à instância do Wildfly com o seguinte comando:

```
connect
```

* Registre o Driver JDBC, passando o nome do módulo recém-adicionado:

```
/subsystem=datasources/jdbc-driver=DRIVER_NAME:add(driver-name=DRIVER_NAME,driver-module-name=MODULE_NAME,driver-xa-datasource-class-name=XA_DATASOURCE_CLASS_NAME, driver-class-name=DRIVER_CLASS_NAME)
```

Um exemplo para adicionar o Driver JDBC do MySQL seria:

```
/subsystem=datasources/jdbc-driver=mysql:add(driver-name=mysql,driver-module-name=com.mysql,driver-xa-datasource-class-name=com.mysql.jdbc.jdbc2.optional.MysqlXADataSource, driver-class-name=com.mysql.jdbc.Driver)
```

## Tornando o Driver JDBC compatível com a versão 4

* Crie um diretório temporário para hospedar os arquivos.
* Crie dentro desse diretório um subdiretório _META-INF/services_
* Dentro do subdiretório _META-INF/services_, crie um arquivo chamado _java.sql.Driver_
* Abra o arquivo e escreva em uma única linha o nome completo da classe com o seu pacote(denominado Fully-Qualified Class Name). Exemplo para o Driver do MySQL;

```
com.mysql.jdbc.Driver
```

* Utilize o comando `jar` do Java para incluir o novo arquivo no Driver JDBC:

```bash
$ jar \-uf driver-jdbc.jar META-INF/services/java.sql.Driver
```