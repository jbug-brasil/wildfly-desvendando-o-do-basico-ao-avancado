# Definindo dependências explícitas de módulos em sua aplicação
Uma vez que criamos nosso módulo customizado, devemos agora definir as dependências para nossa aplicação. Para isso, utilizamos um arquivo de metadado chamado *jboss-deployment-structure.xml*. O arquivo deve estar dentro da raiz da aplicação, no *META-INF* ou no caso de aplicações WAR dentro do *WEB-INF*. Abaixo um exemplo:
```xml
<?xml version="1.0" encoding="UTF-8"?>  
<jboss-deployment-structure>  
    <deployment>  
         <dependencies>  
              <module name="com.myjars.jfreechart" slot="main" ou slot="1.2...."/>  correto?
              <module name="com.myjars.jcommon" />  "Não seria só o nome do módulo aqui?"
        </dependencies>  
    </deployment>  
</jboss-deployment-structure> 
```