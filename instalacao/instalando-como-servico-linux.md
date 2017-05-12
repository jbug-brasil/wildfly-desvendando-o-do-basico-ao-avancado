# Instalando O WildFly como serviço em um Servidor Linux

Executar Servidores de Aplicação como serviço é muito comum nos dias de hoje, pela praticidade de gerenciamento e também por ser muito simples a restauração do serviço após o _boot_ do Sistema Operacional.

No decorrer deste capítulo iremos descrever os passos necessários para configurar o WildFly Server como um serviço utilizando o **systemd** como gerenciador de serviços.

Nas versões anteriores do Wildfly, até as versão 9, os scripts estavam no diretório _$JBOSS\_HOME/bin/init.d_, mas n versão 10 os scripts foram movidos para o diretório _$JBOSS\_HOME/docs/contrib/scripts_, lembrando que os scripts encontrados neste diretório são contribuições de usuários e estão disponíveis na distribuíção do WildFly para serem utilizados como exemplo.

O a criação de um serviço com o **systemd **é muito simples quando comparado ao **init.d**. Para conhecer melhor o systemd acesse este [link](https://www.freedesktop.org/wiki/Software/systemd/).

Neste capítulo será exemplificado a instalação do serviço utilizando o **init.d** e o **systemd**.

## Init.d

Under development

## Systemd

O arquivo de configuração do **systemd** disponibilizado na instalação do WildFly já está pronto para uso, sendo necessário realizar somente alguns passos antes de executá-lo como serviço.

Neste ponto, será necessário ter efetuado os passos descritos no tópico [Instalação passo a passo](instalacao_passo_a_passo.md). Com o ambiente pré configurado, siga os passos abaixo:

```bash
# mkdir /etc/wildfly 
# cp /opt/wildfly/docs/contrib/scripts/systemd/wildfly.conf /etc/wildfly/
# cp /opt/wildfly/docs/contrib/scripts/systemd/wildfly.service /etc/systemd/system/
# cp /opt/wildfly/docs/contrib/scripts/systemd/launch.sh /opt/wildfly/bin/
# chmod +x /opt/wildfly/bin/launch.sh
# chown wildfly. /opt/wildfly/bin/launch.sh
```

Como os scripts já estão pré configurados, depois de executar todos os passos acima, já estamos prontos para iniciar o wildfly.

Primeiramente vamos habilitá-lo para ser executado durante o boot do Sustema Operacional:

```bash
# systemctl enable wildfly
# systemctl start wildfly
```

E para parar o serviço:

```bash
# systemctl stop wildfly
```

Para configurar o serviço do WildFly para usar o modo **Domain** ao invés do modo **Standalone** \(padrão\), edite o arquivo **wildfly.service** localizado em _/etc/wildfly_ conforme o exemplo abaixo:

```
# The configuration you want to run
WILDFLY_CONFIG=domain.xml

# The mode you want to run
WILDFLY_MODE=domain
```

Por padrão o endereço de bind vem configurado c omo **0.0.0.0**, não é uma boa prática deixá-lo com essa configuração, altere o endeço de bind para o endereço de IP do servidor em que o WildFly será executado. Para alterar o endereço de bind edite o mesmo arquivo citado acima da seguinte maneira, como exemplo será utilizado o ip **192.168.1.10**:

```
# The address to bind to
WILDFLY_BIND=192.168.1.10
```



