# Downloads

No presente momento, iremos utilizar o Wildfly versão *10.0.0.Final* no decorrer dos próximos tópicos. Sendo este conteúdo atualizado conforme novas versões forem lançadas.

Além das versões Final existem também as *Beta* e *Alpha* que são lançadas antes da *Final* com o intuito de testar o Servidor de Aplicação para que a versão Final seja o mais perto possível de ser *bug free*.
  
Podemos encontrar todas as versões disponíveis para download neste [link](http://wildfly.org/downloads/), realize o download da versão *10.0.0.Final* ou clique [aqui]( http://download.jboss.org/wildfly/10.0.0.Final/wildfly-10.0.0.Final.tar.gz) para realizar o download.
  
Não se preocupe, caso esteja utilizando Windows os próximos passos serão muito semelhantes, os principais pontos diferentes serão nos arquivos selecionados para download, também está disponível para download o arquivo extensão *.zip*.
  
Após realizado o download do Wildlfy vamos a instalação do Java, caso já o possua instalado pule esta etapa. O WildFly 10 é Java ee 7, isso quer dizer que o WildFly implementa todas as especificações propostas pelo Java ee 7, mais detalhes neste [link](https://docs.oracle.com/javaee/7/api/toc.htm).

Se precisa usar Java 7 não se preocupe, o Wildfly também é compatível com a versão 7 do Java.

Neste caso irei utilizar a versão 8 do Java que pode ser encontrado neste [link](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html).

Lembre-se que para realizar o download do Java é necessário escolher o binário de acordo com o Sistema Operacional que estiver utilizando. Neste caso estaremos utilizando o seguinte binário: **jdk-8u101-linux-x64.rpm**. Se preferir você também pode utilizar o OpenJDK, o que torna a instalação bem mais simples no **Linux**

Exemplo (**Red Hat like**): 

CentOS 7+ ou Fedora 22+
```
$ sudo dnf install java -y
```
Ou
```    
$ sudo yum install java -y
```

Porém se estiver utilizando um Sistema **Debian Like**
    
```
sudo apt-get install openjdk-8-jdk
```
  
Após a finalização verifique se o Java foi corretamente instalado e configurado, para isso basta executar o seguinte comando:

```
$ java -version
openjdk version "1.8.0_101"
OpenJDK Runtime Environment (build 1.8.0_101-b14)
OpenJDK 64-Bit Server VM (build 25.101-b14, mixed mode)

```

Se o resultado for semelhante a este você já está pronto para ir para o próximo tópico.