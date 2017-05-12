# Instalando O WildFly como serviço em um Servidor Linux

Executar Servidores de Aplicação como serviço é muito comum nos dias de hoje, pela praticidade de gerenciamento e também por ser muito simples a restauração do serviço após o _boot_ do Sistema Operacional.

No decorrer deste capítulo iremos descrever os passos necessários para configurar o WildFly Server como um serviço utilizando o **systemd** como gerenciador de serviços.

Nas versões anteriores do Wildfly, até as versão 9, os scripts estavam no diretório _$JBOSS\_HOME/bin/init.d_, mas n versão 10 os scripts foram movidos para o diretório _$JBOSS\_HOME/docs/contrib/scripts_, lembrando que os scripts encontrados neste diretório são contribuições de usuários e estão disponíveis na distribuíção do WildFly para serem utilizados como exemplo.

O a criação de um serviço com o **systemd **é muito simples quando comparado ao **init.d**. Para conhecer melhor o systemd acesse este [link](https://www.freedesktop.org/wiki/Software/systemd/).



