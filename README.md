#Projeto: plugin-deploy
Esse projeto foi criado com o intuito de demonstrar como pode ser feito o deploy automatizado com o plugin do tomcat.
    
    comando: mvn tomcat7:deploy
    
##Configurações utilizadas

     1 - Tomcat7
     2 - Projeto maven
     
###Passos

    1 - Configurar credenciais de deploy do Tomcat
    2 - Configurar credenciais tomcat no Maven
    3 - Configurar projeto para fazer o deploy
    4 - Execututar o deploy automatizado
    
#### 1 - Tomcat
Colocar credenciais utilizadas pra acessar as configurações do tomcat e fazer o deploy:

%TOMCAT_PATH%/conf/tomcat-users.xml

    <role rolename="manager-gui"/>
    <role rolename="manager-script"/>
    <user username="admin" password="admin" roles="manager-gui,manager-script" />
    
#### 2 - Maven
Colocar credenciais utilizadas pra acessar as configurações do tomcat e fazer o deploy:

%MAVEN_PATH%/conf/settings.xml

    <server>    
        <id>Tomcat7</id>
        <username>admin</username>
        <password>admin</password>
    </server>
    
#### 3 - Projeto web
Colocar configuração de build no pom.xml pra que o plugin do maven saiba onde deve procurar o tomcat e a credencial que irá utilizar. 

    <plugin>
        <groupId>org.apache.tomcat.maven</groupId>
        <artifactId>tomcat7-maven-plugin</artifactId>
        <version>2.2</version>
        <configuration>
            <url>http://localhost:8080/manager/text</url>
            <server>Tomcat7</server>
            <path>/plugin-deploy</path>
        </configuration>
    </plugin>
    
#### 4 - Executar o comando
Navegar até pasta do projeto e executar o comando

    mvn tomcat7:deploy
    
###Outros comandos disponíveis:
    
    mvn tomcat7:undeploy // undeploya o projeto, ou seja, retira o projeto do servidor
    mvn tomcat7:redeploy // faz o redeploy do projeto