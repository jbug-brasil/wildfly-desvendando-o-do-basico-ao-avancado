# Definindo dependências explícitas de módulos em sua aplicação
Uma vez que criamos nosso módulo customizado, devemos agora definir as dependências para nossa aplicação. Para isso, utilizamos um arquivo de metadado chamado *jboss-deployment-structure.xml*. O arquivo deve estar dentro da raiz da aplicação, no *META-INF* ou no caso de aplicações WAR dentro do *WEB-INF*. Abaixo um exemplo:
```xml
<?xml version="1.0" encoding="UTF-8"?>  
<jboss-deployment-structure>  
    <deployment>  
         <dependencies>  
              <module name="com.myjars.jfreechart" slot="main"/> 
              <module name="com.myjars.jcommon" />
        </dependencies>  
    </deployment>  
</jboss-deployment-structure> 
```
O módulo *com.myjars.jfreechart:main* foi adicionado como uma dependência para a aplicação
em questão, permitindo então que as classes desse módulo sejam carregadas dentro do ClassLoader
da aplicação, assim como o módulo *com.myjars.jcommon*. Nesse caso, não há um atributo *slot*
especificando qual versão do módulo *com.myjars.jcommon* será usada, nesse caso o Wildfly
implicitamente busca por uma versão *main* e portanto caso o seu módulo possua somente a versão
*main* ela não será necessária, porém quando há mais de uma versão do módulo convém sempre 
definir o parâmetro para dizer qual versão será utilizada.