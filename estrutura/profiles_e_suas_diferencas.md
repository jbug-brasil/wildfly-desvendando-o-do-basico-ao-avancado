# Profiles e suas diferenças

No Java EE, conforme descrevemos na [Introdução](../introducao.md), é dividido em dois perfis: Web e Full. Esses perfis \(ou profiles\) definem o quanto do Java EE será utilizado no desenvolvimento de suas aplicações. O Wildfly, pensando nesses perfis, criou arquivos de configuração para cada perfil Java EE bem como adicionou os componentes para _HA_ \(_High Availability_, ou _Alta disponibilidade_\), que são recursos que permitem o acesso às aplicações hospedadas no servidor mesmo em caso de falhas.

| Perfil | Arquivo de configuração\* | Utilização |
| --- | --- | --- |
| Web | standalone.xml | Permite o uso do perfil Java EE Web |
| Full | standalone-full.xml | Permite o uso do perfil Java EE Full |
| Web c/ HA | standalone-ha.xml | Permite o uso do perfil Java EE Web com características de HA |
| Full c/ HA | standalone-full-ha.xml | Permite o uso do perfil Java EE Full com características de HA |

\* Apenas no modo standalone

## Rodando o Wildfly utilizando os profiles

Para rodar o Wildfly utilizando o profiles descritos na seção anterior, basta adicionar a opção `-c` à linha de comando pasando o arquivo de configuração a ser utilizado. _Exemplo_: Se eu quiser utilizar o perfil Full com HA, basta eu rodar o seguinte comando para iniciar o Wildfly:

```bash
$ ./standalone.sh -c standalone-full-ha.xml
```

## E no modo Domain, como seleciono meu profile?

O modo domain, assim como explicado no tópico anterior ele é gerenciado por um host master e cada host slave possui o seu host controller. As configurações dos profiles são definidas no arquivo **domain.xml** do Domain Controller que são replicadas a todos os membros do Domínio.

> Todos os arquivos de configuração do modo Domínio estão no diretório _$JBOSS\_HOME/configuration/domain_

Os profiles são estruturados da mesma maneira que os profiles do modo standalone, porém com uma pequena diferença, repare na tabela abaixo:

| Perfil | Nome do profile | Utilização |
| --- | --- | --- |
| Web | default | Permite o uso do perfil Java EE Web |
| Full | full | Permite o uso do perfil Java EE Full |
| Web c/ HA | ha | Permite o uso do perfil Java EE Web com características de HA |
| Full c/ HA | full-ha | Permite o uso do perfil Java EE Full com características de HA |

Veja abaixo um exemplo de uma definição de profile encontrada no arquivo **domain.xml:**

```xml
    <profiles>
        <profile name="default">
            <subsystem xmlns="urn:jboss:domain:logging:3.0">
            ...
        <profile name="full">
        ...
    </profiles>
```

A escolha do profile a ser utilizado por grupo de servidores é feita no também no arquivo **domain.xml** da seguinte maneira:

```xml
    <server-groups>
        <server-group name="main-server-group" profile="full">
            <jvm name="default">
                <heap size="64m" max-size="512m"/>
            </jvm>
            <socket-binding-group ref="full-sockets"/>
        </server-group>
        <server-group name="other-server-group" profile="full-ha">
            <jvm name="default">
                <heap size="64m" max-size="512m"/>
            </jvm>
            <socket-binding-group ref="full-ha-sockets"/>
        </server-group>
    </server-groups>
```

O treco a acima é encontrado no final do arquivo e note que em cada definição de grupo de servidores temos o parâmetro **profile **para cada um deles.

> Para iniciar o WildFly no modo domínio basta executar o arquivo _$JBOSS\_HOME_/_bin/domain.sh_



