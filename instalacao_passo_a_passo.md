# Instalação passo a passo

  Neste capítulos iremos abordar a instalação do WildFly partindo do princípio que os downloads descritos no capítulo anterior já foram realizados.

Bom, como todos nós temos o direito de escolha, para ilustrar os exemplos deste tópico e dos demais irei usar a seguinte configuração:

* Sistema Operacional: Fedora 23 x86_64, Server Edition
* Banco de dados: MariaDB 10.0.25-1.fc23

Obs: O banco de dados não será necessário neste primeiro momento, mas será utilizado em capítulos futuros.


##### Primeiro passo: Definindo um usuário para Runtime

  Segurança em primeiro lugar, evite ao máximo utilizar o usuário **root** para executar o WildFly porque desta forma estaremos protegendo o servidor como um todo de forma que uma aplicação que permita execução de códigos arbritrários não execute nada no servidor com um usuário privilegiado.
  Neste case utilizarei um usuário chamado **wildfly**, para criar o usuário execute o seguinte comando:
  
  ```
  # useradd wildfly
  ```


##### Segundo passo: Escolhendo o diretório de instalação

  Esta é realmente a primeira dúvida que temos ao realizar a instalação de qualquer aplicação em nossos servidores, com o WildFly não é diferente. Em poucas palavras, não existe um padrão definido que todos devem seguir, porém muitos administradores acabam escolhendo um determinado modelo a seguir para que todos os servidores possuam os mesmos diretórios/estrutura, isso que, facilita e muito a administração.
  
  Eu sempre costumo usar o diretório **/opt**, lembrando, isto não é uma regra.
  Vamos agora descompactar o WildFly no diretório escolhido:

```
# tar -xzvf wildfly-10.1.0.CR1.tar.gz --directory /opt
```

Ou se prefere utilizar o arquivo com extensão *.zip*:

```
unzip wildfly-10.1.0.CR1.zip -d /opt
```

Neste momento já temos o servidor WildFLy descompactado no diretório **/opt**:

```
# ll /opt
total 0
drwxr-xr-x. 10 root root 220 Jul 28 01:02 wildfly-10.1.0.CR1
```

Note que as permissões de usuário e grupo estão configuradas para o usuário root, como boas práticas não iremos utilizar o usuário root para execução do WildFly, e sim o usuário criado anteriormente, altere as permissões com o seguinte comando:

```
# chown -R wildfly. /opt/wildfly-10.1.0.CR1/
```

Agora podemos utilizar o usuário **wildfly** para executar o Servidor.
Abra um shell utilizando este usuário e em seguida acesso o diretório *wildfly-10.1.0.CR1*:

```
[root@wfly-server ~]# su - wildfly
[wildfly@wfly-server ~]$ cd /opt/wildfly-10.1.0.CR1/
[wildfly@wfly-server wildfly-10.1.0.CR1]$ 
```


