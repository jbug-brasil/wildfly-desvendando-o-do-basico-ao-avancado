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
    
> s


