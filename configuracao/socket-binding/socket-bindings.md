# Socket-bindings

_Socket Bindings_ define o conjunto de Sockets a serem utilizados pelos Subsystems do Wildfly. Nele, você pode definir um nome lógico para esse socket, a porta a ser utilizada, a qual Interface irá responder, se o tráfego é somente de saída, etc. Além disso, com a tag `<socket-binding-group>`, é possível definir um offset[^3] de portas para que instâncias diferentes rodando na mesma máquina física não tenham conflito de portas. Abaixo temos uma configuração de Socket Binding para o perfil Web:

```xml
    <socket-binding-group name="standard-sockets" default-interface="public" port-offset="${jboss.socket.binding.port-offset:0}">
        <socket-binding name="management-http" interface="management" port="${jboss.management.http.port:9990}"/>
        <socket-binding name="management-https" interface="management" port="${jboss.management.https.port:9993}"/>
        <socket-binding name="ajp" port="${jboss.ajp.port:8009}"/>
        <socket-binding name="http" port="${jboss.http.port:8080}"/>
        <socket-binding name="https" port="${jboss.https.port:8443}"/>
        <socket-binding name="txn-recovery-environment" port="4712"/>
        <socket-binding name="txn-status-manager" port="4713"/>
        <outbound-socket-binding name="mail-smtp">
            <remote-destination host="localhost" port="25"/>
        </outbound-socket-binding>
    </socket-binding-group>
```

## Como configurar