# SQL Injection
Esta aplicação foi feita atendendo os requisitos da atividade avaliativa da matéria de Banco de Dados 2 do curso de Ciência da Computação – UNIFEI.
#### Dupla:
**Flavio Mota Gomes -- 2018005379**

**Rafael Antunes Vieira -- 2018000980**

## Descrição dos arquivos
- ### index.php
   Contem o código em HTML, responsavel por capturar o login e senha do usuario e passar para o arquivo login.php.
- ### login.php
   Contem o código em PHP, responsavel por fazer a conexão com o banco.
- ### Style.css
   Contem o código em CSS, responsavel pelo estilo de cores, imagens e fonte da pagina da aplicação.
- ### SQLInjection.backup
   Arquivo com o banco de dados do PostgreSQL, disponibilizado para restaurar e testar a aplicação.
   
## Como Funciona

O SQL Injection consiste em uma técnica de injeção de código com capacidade de acessar ao banco de dados, o que representa um risco. Ocorre, geralmente, durante a entrada de um usuário. Quando solicita-se ao usuário a entrada no sistema, como um nome/senha, o usuário fornece, em vez disso, uma instrução em SQL que será executada no banco de dados sem o conhecimento do administrador do banco.

No arquivo ```login.php```, o login será concretizado se o usuário e senha digitados corresponderem a um dos pares usuário-senha cadastrados no banco de dados. Para realizar essa conferência, há uma query na aplicação que, por meio de um SELECT, varre o banco para verificar os pares usuário-senha cadastrados. Essa query é da seguinte forma:

```SELECT * FROM cliente WHERE nome='$usuario' AND senha='$senha'```

As variáveis $usuario e $senha são recebidas na página login.php e correspondem ao que for digitado pelo usuário da aplicação. Há apenas um usuário cadastrado, "teste", com senha "12345". É possível realizar login utilizando-o. Contudo, ao deixar o campo de login em branco e digitar ```'or''='```no campo de senha, manipula-se a SQL, que será lida da seguinte forma:

```SELECT * FROM cliente WHERE nome='' AND senha=''or''=''```

O SQL Injection ocorre, portanto, porque há uma manipulação da SQL através do uso do caracter ', de modo que nome e senha estão vazios e '' = '', ou seja, a aplicação permitirá o login porque vazio é igual a vazio.

   
## Como Executar a aplicação:  

#### 1. Primeiramente precisamos criar uma database nova com o nome ```sqlinjection```. Depois, restaure o arquivo ``` SQLInjection.backup``` no database ```sqlinjection``` que foi criado. 

![imagemsql](https://user-images.githubusercontent.com/46981155/91649266-68803900-ea48-11ea-9cba-d9457d067ad5.png)

#### 2. Após a configuração do PostgreSQL, abra o arquivo ```login.php``` e na linha **17** coloque o host e a porta do servidor. Na linha **18** coloque o usuário e na linha **19** coloque a senha de acesso do servidor onde você restaurou o databese.

![Imagem1sqli](https://user-images.githubusercontent.com/46981155/91649055-dc6d1200-ea45-11ea-90f1-ba2eb8397b30.png)

#### 3. Após ter mostrado o caminho do PostgreSQL para a aplicação, vamos instalar o servidor ``` APACHE ``` para executar a aplicação. Recomendamos instalar a ferramenta ```XAMPP``` para ter acesso ao servidor;

![imagem2sqli](https://user-images.githubusercontent.com/46981155/91649060-edb61e80-ea45-11ea-9963-5a9e0b467426.png)


#### 4. Agora, iremos configurar o servidor e colocar os arquivos dentro dele para executar. Procure pelo arquivo ```php.ini``` na pasta do ```XAMPP```. Na instalação padrão do sistema Windows, ela se encontra em ```C:\xampp\php```.

![imagem3sqli](https://user-images.githubusercontent.com/46981155/91649066-f9094a00-ea45-11ea-9dc5-9e2a121e8db2.png)


#### 5. Abra com o bloco de notas e procure pelo comando ```;extension=pgsql``` e retire o ```;``` e salve o arquivo.

![imagem4sqli](https://user-images.githubusercontent.com/46981155/91649073-06becf80-ea46-11ea-8ab9-3de5bedb7383.png)

#### 6. Copie os arquivos ```index.php```, ```Style.css```, ```login.php``` e a pasta ```image``` para a pasta chamada ```htdocs``` que se encontra dentro da pasta onde está instalado o ```XAMPP```. Na instalação padrão do sistema Windows, ela se encontra em ``` C:\xampp\htdocs```.


#### 7. Para finalizar, ligue o servidor APACHE no XAMPP:

![imagem5sqli](https://user-images.githubusercontent.com/46981155/91649079-11796480-ea46-11ea-88c4-02153df2e108.png)

#### 8. Após ligar o servidor, abra o navegador e digite o endereço: http://localhost/index.php (esse endereço pode variar de acordo com o nome do projeto criado):

![imagem6sqli](https://user-images.githubusercontent.com/46981155/91649082-1a6a3600-ea46-11ea-82d3-442c0778d21c.png)

#### Pronto! Agora pode se replicar a falha SQL Ingection conforme explicado no tópico ```Como funciona```.

   


