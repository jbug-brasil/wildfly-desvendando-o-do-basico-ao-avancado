# Adicionando um módulo customizado
Para criar um módulo customizado no Wildly, é necessário criar uma estrutura dentro do diretório *JBOSS_HOME/modules* com a seguinte estrutura:
```
Nome do módulo
  ├── main
  │   ├── module.xml
  |   └── biblioteca.jar
```
O módulo precisa ter uma estrutura similar aos pacotes em java, ou seja, se você possui um pacote chamado *br.com.empresa.aplicacao* então você precisa ter um diretório criado para cada nome. Nesse exemplo, teria que haver um diretório *com* dentro do diretório *br* contendo um subdiretório *empresa/aplicacao*. Dentro dessa estrutura há um diretório main, onde espera-se que seja a última versão daquele módulo (ou a versão padrão, como quer que queira chamar). Caso você queira criar várias versões do mesmo módulo, basta criar um subdiretório dentro do diretório do módulo contendo o nome da versão. Por fim, todos os arquivos *.jar* pertencentes a esse módulo devem ser copiados dentro do caminho *<módulo>/main* (ou *<módulo>/versao*, caso esteja criando uma nova versão do módulo) e o arquivo module.xml. Esse arquivo serve como um metadado dentro do módulo, especificando os jars pertencentes a esse módulo bem como suas dependências. Abaixo um exemplo:
```
com
  ├── myjars
  │   ├── jfreechart
  │   │      ├── main
  |   │      |    ├── jfreechart.jar
  |   │      |    ├── common.jar
  |   │      |    └── module.xml
  │   │      ├── 1.0.15
  |   │      |    ├── jfreechart.jar
  |   │      |    ├── common.jar
  |   │      |    └── module.xml
```
Nessa estrutura existem dois módulos: *com.myjars.jfreechart:main* e *com.myjars.jfreechart:1.0.15*. Assim, eu posso ter uma aplicação que utiliza a primeira versão do módulo e uma outra aplicação utilizando a segunda no mesmo servidor Wildfly.

## O arquivo module.xml 
Para descrever o módulo, é necessário criar um arquivo xml para indicar os jars pertencentes a este módulo bem como suas dependências.
```xml
<?xml version="1.0" encoding="UTF-8"?>
<module xmlns="urn:jboss:module:1.1" name="com.myjars.jfreechart">
       <resources>  
           <resource-root path="jfreechart.jar"/>  
           <resource-root path="jcommon.jar"/>  
       </resources>  
</module>
```