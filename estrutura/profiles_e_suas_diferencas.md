# Profiles e suas diferenças

No Java EE, conforme descrevemos na [Introdução](../introducao.md), é dividido em dois perfis: Web e Full. Esses perfis (ou profiles) definem o quanto do Java EE será utilizado no desenvolvimento de suas aplicações. O Wildfly, pensando nesses perfis, criou arquivos de configuração para cada perfil Java EE bem como adicionou os componentes para _HA_ (_High Availability_, ou _Alta disponibilidade_), que são recursos que permitem o acesso às aplicações hospedadas no servidor mesmo em caso de falhas.

| Perfil       | Arquivo de configuração*  | Utilização                                                     |
|--------------|---------------------------|----------------------------------------------------------------|
| Web          | standalone.xml            | Permite o uso do perfil Java EE Web                            |
| Full         | standalone-full.xml       | Permite o uso do perfil Java EE Full                           |
| Web c/ HA    | standalone-ha.xml         | Permite o uso do perfil Java EE Web com características de HA  |
| Full c/ HA   | standalone-full-ha.xml    | Permite o uso do perfil Java EE Full com características de HA |
\* Apenas no modo standalone

## Rodando o Wildfly utilizando os profiles

Para rodar o Wildfly utilizando o profiles descritos na seção anterior, basta adicionar a opção `-c` à linha de comando pasando o arquivo de configuração a ser utilizado. _Exemplo_: Se eu quiser utilizar o perfil Full com HA, basta eu rodar o seguinte comando para iniciar o Wildfly:

```bash
$ ./standalone.sh -c standalone-full-ha.xml
```