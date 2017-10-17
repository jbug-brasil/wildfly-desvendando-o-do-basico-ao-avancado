# Instalando O WildFly como serviço em um Servidor Windows

Como descrito anteriormente em [Instalando como Serviço no Linux](/instalacao/instalando-como-servico-linux.md) executar Servidores de Aplicação como serviço é uma atividade muito comum e trás praticidade para o gerenciamento do servidor de aplicação.

Instalar o WildFly 10 como um serviço Windows está muito mais simples do que nas versões anteriores. Não é necessário instalar nenhuma biblioteca de terceiro uma vez que o WildFly prove tudo que você precisa para executar esta atividade.

Como comentado no capítulo anterior os arquivos para executar o WildFly como serviço estão localizados na pasta _JBOSS_HOME/docs/contrib/scripts/service_.

Para instalar o serviço em modo _standalone_ basta executar o seguinte comando dentro da pasta _JBOSS_HOME/docs/contrib/scripts/service_ pela linha de comando.

```bash
service install
```
Agora você pode gerenciar o serviço, realizando _start_, _stop_ ou _restart_ pelo Windows Service. Caso a instalação tenha ocorrido corretamente, será possível ver o serviço em Windows Service para isto acesse:

1.  Abra o menu "Iniciar"
2.  Digite " services.msc " na caixa de pesquisa na parte inferior do menu Iniciar
3.  Pressione "Enter" para abrir o utilitário Serviços
4. Procure o serviço chamado _Wildfly Application Server._

![Windos Service](images/windows_service.png)

Como alternativa é possível fazer os gerenciamentos básicos do serviço utilizando o _JBOSS_HOME/docs/contrib/scripts/service/service.bat_. Veja alguns exemplos a seguir:

```bash
service start
service restart
service stop
```

Para executar em modo domain, é necessário passar mais alguns parâmetros para o comando _service.bat_ como Domain controller (Por padrão é 127.0.0.1 e porta 9990) e também o nome do host (por padrão é "master").

Veja o exemplo a seguir:

```bash
service install /controller localhost:9990 /host master
```
