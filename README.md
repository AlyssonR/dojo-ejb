ejb-remote: Cliente EJB remoto
=====================================
Autor: jáder belarmino  
nível: básico  
Tecnologias: EJB, JNDI  
Resumo: Como executar um EJB remoto.  
Target Product: WildFly  
Source: <https://github.com/jcbelarmino/dojo-ejb>  

Construir e implantar o projeto
-------------------------

1. Iniciar o servidor WildFly.
2. Abrir um prompt de comando na pasta dojo-ejb
3. Construir e instalar a cama servidor:

            cd server-side
            mvn clean install        
            mvn wildfly:deploy
4. Construir e executar o código Cliente

            cd ../client
            mvn clean compile
            mvn exec:exec


Configurar o servidor para executar remoto:
--------------------
1. Adicionar o usuario do arquivo ``client/src/main/resources/jboss-ejb-client.properties`` 

```
remote.connectionprovider.create.options.org.xnio.Options.SSL_ENABLED=false

remote.connections=default

remote.connection.default.host=192.168.0.13
remote.connection.default.port = 8080
remote.connection.default.connect.options.org.xnio.Options.SASL_POLICY_NOANONYMOUS=false

remote.connection.default.username=nome_usuario
remote.connection.default.password=senha
```
2. No servidor wildfly com o comando: ``<PASTA DE INSTALACAO WILDFLY>/bin/add-user.sh -a -u nome_usuario -p senha``


Desinstalar o EJB:
--------------------

        cd ../server-side

        mvn wildfly:undeploy
