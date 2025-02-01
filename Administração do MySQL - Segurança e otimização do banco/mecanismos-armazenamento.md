1 ) As variáveis que estão declaradas no C:\ProgramData\MySQL\MySQL Server 8.0\my.ini serão inicializadas com os valores declarados no arquivo sempre que o MySQL for inicializado.

2 ) [Aqui](https://dev.mysql.com/doc/refman/8.0/en/server-system-variables.html), você pode ver a documentação de inúmeras variáveis de ambiente.

3 ) O valor das variáveis durante a seção pode ser vista pelo Workbench. Entre no Workbench e, na base de dados sakila, digite no editor de comandos SQL:
````sql
SHOW GLOBAL STATUS LIKE 'Created_tmp_disk_tables';
````
![](https://cdn3.gnarususercontent.com.br/1224-mysql-adminstracao/02/image1.png)

4 ) Ainda na base de dados sakila, outra variável pode ser observada:
````sql
SHOW GLOBAL STATUS LIKE 'Created_tmp_tables';
````
![](https://cdn3.gnarususercontent.com.br/1224-mysql-adminstracao/02/image15.png)

Estas duas variáveis estão relacionadas com o número de tabelas temporárias que podem ser abertas durante uma seção em memória e em disco. Claro que isso influencia na performance do banco, caso seja necessário usar o HD para armazenar tabelas temporárias criadas pelo MySQL durante os comandos SQL.

5 ) A variável <code>tmp_table_size</code>, que foi inicializada pelo my.ini, tem o valor de 103 e ele pode ser visto pelo comando do WorkBench:
````sql
SHOW GLOBAL VARIABLES LIKE 'tmp_table_size';
````

6 ) A variável de ambiente pode ser modificada pelo usuário que tenha privilégios para isso. Para isso, novamente na base de dados sakila, digite o seguinte comando:
````sql
SET GLOBAL tmp_table_size = 208003328;
````

7 ) Assim, é possível modificar o valor desta variável e ignorar o que estava, inicialmente, especificado no my.ini.

8 ) Já sobre mecanismos de armazenamentos, durante a criação da tabela, é possível determinar qual mecanismo a mesma irá utilizar. Crie uma tabela, na base de dados sakila, conforme o comando abaixo:
````sql
CREATE TABLE DEFAULT_TABLE (ID INTEGER, NOME VARCHAR(100));
````

9 ) Se você for na tabela, na árvore de objetos do Workbench e clicar sobre o ícone de informações, verá as características de armazenamento desta tabela que foi criada:

![](https://cdn3.gnarususercontent.com.br/1224-mysql-adminstracao/02/image45.png)

10 ) Você pode ver que, por padrão, as tabelas são criadas com o mecanismo de armazenamento <code>InnoDB</code>:

![](https://cdn3.gnarususercontent.com.br/1224-mysql-adminstracao/02/image5.png)

11 ) É possível alterar a propriedade do mecanismo de armazenamento da tabela, com o comando:
````sql
ALTER TABLE DEFAULT_TABLE ENGINE = MyISAM;
````

12 ) Além disso, você pode definir o tipo de mecanismo de armazenamento que será usado na tabela no momento de sua criação. Para isso, digite:
````sql
CREATE TABLE DEFAULT_TABLE2 (ID INTEGER, NOME VARCHAR(100)) ENGINE = MEMORY;
````

13 ) Quando você cria uma tabela pelo assistente do Workbench, você pode ver a opção de seleção do mecanismos de armazenamento, sempre apresentando o InnoDB como padrão:

![](https://cdn3.gnarususercontent.com.br/1224-mysql-adminstracao/02/image20.png)

## O que aprendemos?

- A importância das variáveis de ambiente
- Como modificar a variável de ambiente pelo Workbench
- O que são os mecanismos de armazenamento e os tipos principais, com suas características
- Como determinar o mecanismo de armazenamento no momento da criação das tabelas