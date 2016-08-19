# Criando usuário de gerenciamento

  Para conseguirmos utilizar a console de gerenciamento do WildFly é necessário criar um usário de gerenciamento, também existe usuários de aplicação, segue uma pequena diferença entre eles:
  
  * Management: Usuários utilizados para gerenciar o WildFly utilizando os seguintes métodos:
    * Console de gerenciamento
    * JBoss CLI

Ambos estão disponíveis na porta **9990**.

Neste tópico iremos abordar somente a criação de usuário de gerenciamento bem como acessar a console de gerenciamento.

Caso você tente acessar a console de gerenciamento sem ter antes, criado o usuário você será redirecionado para a página abaixo informando que é necessário executar o script **add-user.sh|bat** para adicionar um usuário de gerenciamento utilizando o realm **ManagementRealm**:

* Acesse **http://localhost:9990**

![](Screenshot from 2016-08-19 15-22-34.png)

Para adicionar o usuário siga os passos a seguir:

*  Execute o script **add-user.sh**
    ```
    $WFLY_HOME/bin/add-user.sh
    
    What type of user do you wish to add? 
     a) Management User (mgmt-users.properties) 
     b) Application User (application-users.properties)
    (a): 
    ```
Por padrão o **ManagementRealm** é selecionado, apenas aperte *enter* para prosseguir.
O próximo passo será definir o nome do usuário, escolha um username e prossiga:
```
Enter the details of the new user to add.
Using realm 'ManagementRealm' as discovered from the existing property files.
Username : admin  
```
Logo a seguir você será informado que o usuário **admin** já existe porém está desativado e irá lhe mostrar as opções disponíveis:
```
User 'admin' already exists and is disabled, would you like to... 
 a) Update the existing user password and roles 
 b) Enable the existing user 
 c) Type a new username
(a): 
```
Você terá a opção de atualizar usuário existente e seus grupos, ativar o usuário existente ou digitar um novo username.
Neste caso iremos somente atualizar a senha do usuário **admin**, por default esta opção já está selecionada, apenas tecle *enter*.
Agora defina a senha:
```
Password recommendations are listed below. To modify these restrictions edit the add-user.properties configuration file.
 - The password should be different from the username
 - The password should not be one of the following restricted values {root, admin, administrator}
 - The password should contain at least 8 characters, 1 alphabetic character(s), 1 digit(s), 1 non-alphanumeric symbol(s)
Password : 
Re-enter Password : 
```
O próximo passo é definir os grupos, no momento não será necessário definir nenhum, apenas prossiga:?
```
What groups do you want this user to belong to? (Please enter a comma separated list, or leave blank for none)[  ]: 
Updated user 'admin' to file '/dados/server/wildfly-10.0.0.Final/standalone/configuration/mgmt-users.properties'
Updated user 'admin' to file '/dados/server/wildfly-10.0.0.Final/domain/configuration/mgmt-users.properties'
Updated user 'admin' with groups  to file '/dados/server/wildfly-10.0.0.Final/standalone/configuration/mgmt-groups.properties'
Updated user 'admin' with groups  to file '/dados/server/wildfly-10.0.0.Final/domain/configuration/mgmt-groups.properties'
```






















