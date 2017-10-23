# Instalando O WildFly como serviço em um Servidor Linux

Executar Servidores de Aplicação como serviço é muito comum nos dias de hoje, pela praticidade de gerenciamento e também por ser muito simples a restauração do serviço após o _boot_ do Sistema Operacional.

No decorrer deste capítulo iremos descrever os passos necessários para configurar o WildFly Server como um serviço utilizando o **systemd** como gerenciador de serviços.

Nas versões anteriores do Wildfly, até as versão 9, os scripts estavam no diretório _$JBOSS\_HOME/bin/init.d_, mas n versão 10 os scripts foram movidos para o diretório _$JBOSS\_HOME/docs/contrib/scripts_, lembrando que os scripts encontrados neste diretório são contribuições de usuários e estão disponíveis na distribuíção do WildFly para serem utilizados como exemplo.

O a criação de um serviço com o **systemd **é muito simples quando comparado ao **init.d**. Para conhecer melhor o systemd acesse este [link](https://www.freedesktop.org/wiki/Software/systemd/).

Neste capítulo será exemplificado a instalação do serviço utilizando o **init.d** e o **systemd**.

## Init.d

Executar o WildFly como serviso utilizando o **init.d** é um tarefa simples, assim como utilizando o **systemd** que será abordado a seguir. Todos os scripts utilizando estão localizados no diretório _$JBOSS\_HOME/docs/contrib/scripts/init.d/_. Dentro deste diretório podemos ver os seguintes arquivos:

* **wildfly-­init­-redhat.sh** : Arquivo a ser utilizado para distribuições Red Hat Enterprise Linux, como RHEL e Centos;

* **wildfly­-init­-debian.sh**: Arquivo a ser utilizado para distribuições Debian Linux, como o Debian e Ubuntu por exemplo;

* **wildfly.conf**: Por fim, o arquivo de configuração utilizado pelos dois arquivos init descritos acima.

O primeiro passo é copiar o o arquivo de script, de arcordo com sua distribuição Linux, para o diretório _/etc/init.d_. Como utilizamos o Fedora, iremos executar o seguinte comando:

```bash
cp /opt/wildfly/docs/contrib/scripts/init.d/wildfly-init-redhat.sh /etc/init.d/wildfly
```

Agora precisamos copiar o arquivo de configuração **wildfly.conf** para onde o script espera que ele esteja, em _/etc/default_ como podemos observar no script copiado anteriormente:

```bash
(...)

# Load JBoss AS init.d configuration.
if [ -z "$JBOSS_CONF" ]; then
        JBOSS_CONF="/etc/default/${WILDFLY_NAME}.conf"
fi

[ -r "$JBOSS_CONF" ] && . "${JBOSS_CONF}"

(...)
```

Para copiar o arquivo, execute o seguinte comando:

```bash
mkdir -p /etc/default
cp /opt/wildfly/docs/contrib/scripts/init.d/wildfly.conf /etc/default
```

O próximo passo será editar o arquivo **wildfly.conf** previamente copiado com as seguintes informações:

```bash
#Location of Java
JAVA_HOME=/usr/java/jdk1.8.0_45

# Location of WildFly
JBOSS_HOME=/opt/wildfly/

# The username who should own the process.
JBOSS_USER=wildfly

# The mode WildFly should start, standalone or domain
JBOSS_MODE=standalone

# Configuration for standalone mode
JBOSS_CONFIG=standalone.xml
```

Note que é possível executar em modo domain, além de passar outros parâmetros, como:

```bash
## The amount of time to wait for startup
STARTUP_WAIT=60

## The amount of time to wait for shutdown
SHUTDOWN_WAIT=60

## Location to keep the console log
# JBOSS_CONSOLE_LOG="/var/log/wildfly/console.log"

## Additionals args to include in startup
# JBOSS_OPTS="--admin-only -b 127.0.0.1"
```

Dando continuidade, o passo seguinte é instalar o wildfly como um serviço utilizando o comando **chkconfig**.

```bash
chkconfig --add wildfly
```

Em seguida, configurar o nível de inicialização onde o serviço será iniciado:

```bash
chkconfig --level 2345 wildfly on
```

Por fim vamos iniciar o serviço:

```bash
sudo service wildfly start
```

Caso tudo ocorra bem, a seguinte saída deve ser mostrada no console:

```bash
sudo service wildfly start
Starting wildfly (via systemctl):                          [  OK  ]
```

Para encerar o serviço, basta executar o comando:

```bash
sudo service wildfly stop
```

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

Por padrão o endereço de bind vem configurado como **0.0.0.0**, não é uma boa prática deixá-lo com essa configuração, altere o endeço de bind para o endereço de IP do servidor em que o WildFly será executado. Para alterar o endereço de bind edite o mesmo arquivo citado acima da seguinte maneira, como exemplo será utilizado o ip **192.168.1.10**:

```
# The address to bind to
WILDFLY_BIND=192.168.1.10
```



