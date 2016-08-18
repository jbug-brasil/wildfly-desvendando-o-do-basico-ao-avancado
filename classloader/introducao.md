# ClassLoader Modular
ClassLoaders são parte de qualquer aplicação Java, nela reserva a responsabilidade de carregar dinamicamente as classes para a Máquina Virtual Java (JVM) para então criar objetos a partir daquela classe. Geralmente essas classes são carregadas sob demanda, ou seja, à medida que objetos são instanciados o ClassLoader carrega a classe em memória. 

O ClassLoader é dividido em:

1. Bootstrap
2. Extension
3. System

![Classloader da JRE](./images/classloader.svg)

No Bootstrap ClassLoader todas as classes dentro de JRE/lib/rt.jar são carregadas, bem como qualquer outra classe de qualquer arquivo .jar que esteja dentro deste diretório, já no Extension ClassLoader todas as classes pertencentes aos arquivos .jar localizados em JRE/lib/ext são carregadas e por fim o System ClassLoader carrega as classes que estejam dentro do ClassPath, seja ela especificada dentro da variável de ambiente CLASSPATH ou então através da opção -classpath ou -cp do comando java.  Ao inicializar a JVM, esses três ClassLoaders são criados e inicializados.
Como pode ver na figura acima, a estrutura do ClassLoader é hierárquica, ou seja, antes de inicializar o System ClassLoader o Boostrap ClassLoader e o Extension ClassLoader devem ser carregados primeiro. No Wildfly, a estrutura muda um pouco e ela é baseada em módulos. Veremos na próxima seção como ela funciona.