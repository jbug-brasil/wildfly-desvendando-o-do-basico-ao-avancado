# Introdução

Java é o nome dado tanto à linguagem de programação largamente conhecida quanto à plataforma por trás da linguagem. Sua popularidade se deve ao fato de que a linguagem é compilada em um código intermediário \(conhecida como Bytecode\) para execução dentro da Máquina Virtual Java \(ou JVM\). Isso proporcionou ao Java uma série de facilidades na programação que permite ao desenvolvedor se preocupar somente em programar o que realmente é necessário para a programação, deixando questões como coleta de lixo \(Garbage Collection\), performance de execução de código nativo, gerenciamento de memória e outros para a Máquina Virtual Java. Tal característica hoje é utilizada em outras linguagens de programação, como .NET e Python, tamanha a importância da Máquina Virtual nos paradigmas atuais de linguagens de programação.

Isso proporcionou à Máquina Virtual Java não somente executar programas escritas na linguagem Java como também outras linguagens. Atualmente, é possível executar programas escritos em Groovy, Scala, Python, Ruby e outros na Máquina Virtual Java por conta dessas linguagens disponibilizarem compiladores especiais que permitem criar o Bytecode para executar na JVM.

![Processo de execução da JVM](images/Java-program-execution.png)

A plataforma Java, desde a sua concepção, recebeu algumas divisões com o objetivo de tornar a evolução da plataforma focado em seus devidos objetivos, dentre eles podemos citar:

* _Java Standard Edition \(ou Java SE\)_: É o nome dado à plataforma nas sua mais básica utilização, cobrindo toda a implementação da Linguagem Java, do Bytecode e da JVM.
* _Java Enterprise Edition \(ou Java EE\)_: É o nome dado à plataforma com foco em aplicações corporativas \(objetivo desde livro\), cobrindo características como persistência de dados, distributabilidade, segurança e outros assuntos pertinentes. Desde a versão 1.6 do Java EE a plataforma se dividiu em dois perfis \(profiles\):
  _web_: Onde tudo o que será utilizado/disponibilidado por um fornecedor serão características que permitem o desenvolvimento de uma aplicação Web
  _full_: Onde o que será utilizado/disponibilizado pelo fornecedor serão todo o perfil Web mais características adicionais que permitem o uso de componentes como EJB e outros
* _Java Micro Edition \(ou Java ME\)_: É o nome dado à plataforma cujo objetivo é o foco em dispositivos embarcados \(Smartphones, Impressoras, Set-top boxes, Microcontroladores em geral e outros\). Essa plataforma em específico é dividida dois perfis, sendo eles:
  * _Connected Limited Device Configuration \(ou CLDC\)_: Um perfil com foco em dispositivos que possuem conexão limitada ou nenhuma conexão com a Internet
  * _Connected Device Configuration \(ou CDC\)_: Um perfil com foco em dispositivos que possuem conexão com Internet
* _Java Card_: Uma plataforma muito específica com foco no desenvolvimento de aplicações que utilizam Smart Cards
* _Java TV_: Uma plataforma com foco para TV Digital \(O Ginga, plataforma brasileira para TV Digital, utiliza partes dessa plataforma\)

Há outras plataformas criadas para outros fins, mas não iremos extender em descrever todas. Conforme já mencionado, o objetivo deste livro está no foco ao Java EE, onde o Wildfly implementa suas características.

## Como assim o Wildfly implementa o Java EE?

As plataformas Java SE e Java ME são administradas pela Oracle, já o Java EE foi incorporado recentemente e será administrada pela Eclipse Foundation. Além da Oracle e Eclipse Foundation, outras empresas, Java User Groups \(ou JUGs\) e indivíduos que definem as próximas tecnologias a serem desenvolvidas para as próximas versões de suas plataformas, conhecido como Java Community Process \(ou JCP\). Nela, é possível discutir com todos os envolvidos na comunidade Java \(ela é livre para quem quiser contribuir\) quais serão as novas tecnologias a serem adicionadas nas próximas versões de suas plataformas. Todo o processo de adicionar ou até mesmo melhorar um determinado componente ou tecnologia da Plataforma Java é feita por um processo formal chamado de Java Specification Request \(ou JSR\), onde é atribuído a ela um _Expert Group_ que trabalha para discutir a especificação daquele componente ou tecnologia.

Sendo assim, a JCP define como determinada plataforma deve ser construída, ficando a cargo das empresas interessadas em ter um software alinhado àquela plataforma literalmente implementar aquelas especificações. Hoje, empresas como Oracle, Red Hat e IBM são as principais que trabalham para implementar essas especificações em suas soluções.

O Wildfly, então, é uma implementação da plataforma Java EE. Isso significa que todas as especificações determinadas para uma determinada versão do Java EE \(a versão mais recente é a Java EE 1.7\) foram implementadas no Wildfly.

## Mas afinal de contas o que é Java EE?

Java EE é o conjunto de JSRs que focam no desenvolvimento de aplicações corporativas cujo foco está nas seguintes características:

* Distributabilidade
* Persistência
* Segurança
* Gerenciamento de Transações
* Mensageria
* Entre outros...

![Diagrama de blocos das principais tecnologias da plataforma Java EE versão 1.7](http://i.vimeocdn.com/video/543009775_1280x720.jpg)

É importante lembrar que o objetivo da especificação Java EE \(sim, Java EE também é uma especificação, conhecida como _Umbrella Specification_\) é padronizar o uso de determinadas tecnologias e portanto ela não tem como objetivo criar inovações tecnológicas em torno da plataforma. Seu objetivo principal é evitar o fenômeno chamado de _Vendor Lock-In_, que é um fornecedor "prender" seus clientes a uma característica muito específica e que altera uma funcionalidade do Java EE. Claro que há outros aspectos que o Java EE não pretende controlar, como por exemplo _Clustering_, sendo esse livre para o fornecedor criar sua própria implementação. A este caso específico foi dada essa liberdade de implementação para permitir a livre concorrência entre seus fornecedores e atraí-os para a comunidade Java.

## Por que Utilizar Um Servidor de Aplicação?

Um servidor de aplicação fornece todo um ambiente para o _deploy_ e manutenção de aplicações, seguindo as especificações Java EE, além de possuir uma API para acesso a todos estes recursos. O Wildfly implementa as especificações Java EE 7, também conhecida como JEE 7, e é compatível com vários profiles que foram definidos no Java EE 7.

#### Por que Utilizar Wildfly?

Os principais motivos para utilizar o Wildfly são:

1. **Unparalleled Speed:** O Wildfly possui um startup mais veloz, o processo de boot foi otimizado desde o Wildfly 8, agora os processos são iniciado paralelamente para eliminar esperas desnecessárias e aproveitar o poder dos processadores multi-core. Os serviços não críticos são mantidos em gelo até o primeiro uso.A partir do Wildfly 8 foi inserido um novo web server de alta performance, o [undertow](http://undertow.io/) que tem a habilidade de escalar mais de um milhão de conexões. Isso nos dá a capacidade de atender alguns requisitos de modernas aplicações web, como: Conectividade, Responsividade e Habilidade de escalar.

2. **Exceptionally Lightweight:** O Wildfly fez mudanças significaticas no gerenciamento de memória. Os serviços de runtime foram desenvolvidos para que alocassem o mínimo de heap. Com o uso de class loading modular o servidor de aplicação evita classes duplicadas e que seja iniciado mais módulos que o necessário. Com isso o uso de memória inicial é reduzido, e também evita-se que o garbage collector fique pausando o sistema. Ainda é possível adicionar

3. **Powerful Administration:** As configurações do Wildfly são facilmente gerenciadas, de compreensão simples e desenvolvida com foco no usuário. Existem tres formas de gerenciar as configurações no servidor de aplicação: Edição de XML, Por linha de comando e utilizando o Gerenciar web. Não se preocupe, iremos abordar esses temas nos próximos capítulos. Ainda é possível executar o Wildfly de dois modos: Standalone \(uma JVM\) ou Domain \(várias JVMs\), isto também será abordado em capítulos futuros.

4. **Supports Latest Standards and Technology:** O Wildfly foi todo desenvolvido baseando-se nas especificações Java EE 7. Com isso o servidor de aplicação provém ao desenvolvedor capacidade de criar aplicações web com mais facilidade e agilidade. O Wilfdly também possibilita trabalhar com as novas especificações para web moderna, como Websockets, JSON-P, REST, JAX-RS 2, etc. Tudo isso graças ao Undertow.

5. **Modular Java:** O Class loading hierarquico é um problema conhecido, causando entre outros falhas no momento do deploy de aplicação. O Wildfly faz uso correto de classloading por meio de módulos que fazem a isolação da aplicação escondendo as classes de implementação do servidor da aplicação, e apenas “linkando” os Jars que sua aplicação necessita.

6. **Easily Testable:** Com a melhora de performance do Wildfly, as aplicações são facilmente testadas utilizando [arquilian](http://arquillian.org/).

7. **Based on the Best of Open Source:** RestEasy, Weld, Hibernate, HornetQ e Arquillian são algumas das tecnologias que estão presentes no Wildfly.

## O que virá nos próximos capítulos?

O livro irá trazer uma breve introdução ao Wildfly, sua arquitetura e depois mostraremos algumas das tarefas administrativas que podem ser feitas para configurar os componentes do Java EE, bem como fazer o _deployment_ de aplicações Java EE dentro do Wildfly.

> Observação: Todos as aplicações de exemplo utilizadas no decorrer do livro estão disponíveis no [GitHub.](https://github.com/jbug-brasil/wildfly-desvendando-o-do-basico-ao-avancado/tree/master/exemplos)



