1 ) Acesse MySQL Workbench.

2 ) Crie a tabela de cliente digitando o comando abaixo:
````sql
CREATE TABLE tbcliente
( CPF VARCHAR (11) ,
NOME VARCHAR (100) ,
ENDERECO1 VARCHAR (150) ,
ENDERECO2 VARCHAR (150) ,
BAIRRO VARCHAR (50) ,
CIDADE VARCHAR (50) ,
ESTADO VARCHAR (2) ,
CEP VARCHAR (8) ,
IDADE SMALLINT,
SEXO VARCHAR (1) ,
LIMITE_CREDITO FLOAT ,
VOLUME_COMPRA FLOAT ,
PRIMEIRA_COMPRA BIT )
````

3 ) Execute o comando e depois atualize a árvore do Workbench para observar a nova tabela criada.

4 ) Podemos criar tabela pelo assistente. Botão da direita do mouse sobre Tables, abaixo do banco de dados Sucos, e escolha Create Table.

![](https://cdn3.gnarususercontent.com.br/1220-mysqlintroducaoaosql/03/1.png)

5 ) Digite o nome da tabela como tbProduto.

6 ) Inclua os campos conforme mostrado abaixo:
````sql
PRODUTO VARCHAR(20)
NOME VARCHAR(150)
EMBALAGEM VARCHAR(50)
TAMANHO VARCHAR(50)
SABOR VARCHAR(50)
PRECO_LISTA FLOAT
````

7 ) Clique no botão Apply.

8 ) Verifique o comando a ser executado. Clique em Apply novamente e a tabela é criada.

9 ) A tabela pode ser apagada. Para isso digite o comando para criar novas tabelas:
````sql
CREATE TABLE tbcliente2
( CPF VARCHAR (11) ,
NOME VARCHAR (100) ,
ENDERECO1 VARCHAR (150) ,
ENDERECO2 VARCHAR (150) ,
BAIRRO VARCHAR (50) ,
CIDADE VARCHAR (50) ,
ESTADO VARCHAR (2) ,
CEP VARCHAR (8) ,
IDADE SMALLINT,
SEXO VARCHAR (1) ,
LIMITE_CREDITO FLOAT ,
VOLUME_COMPRA FLOAT ,
PRIMEIRA_COMPRA BIT );
````
````sql
CREATE TABLE tbcliente3
( CPF VARCHAR (11) ,
NOME VARCHAR (100) ,
ENDERECO1 VARCHAR (150) ,
ENDERECO2 VARCHAR (150) ,
BAIRRO VARCHAR (50) ,
CIDADE VARCHAR (50) ,
ESTADO VARCHAR (2) ,
CEP VARCHAR (8) ,
IDADE SMALLINT,
SEXO VARCHAR (1) ,
LIMITE_CREDITO FLOAT ,
VOLUME_COMPRA FLOAT ,
PRIMEIRA_COMPRA BIT );
````

10 ) Foram criadas duas tabelas. Agora vamos apaga-las. A primeira por comando:
````sql
DROP TABLE TB_CLIENTES3;
````

11 ) Pelo assistente basta com o botão da direita do mouse sobre o nome da tabela TB_CLIENTES2:

![](https://cdn3.gnarususercontent.com.br/1220-mysqlintroducaoaosql/03/2.png)

Apague a tabela <code>TABELA_DE_VENDEDORES2</code> usando script SQL.

Para criar a tabela antes de apagá-la execute:
````sql
CREATE TABLE TABELA_DE_VENDEDORES2 (
  MATRICULA varchar(5),
  NOME varchar(100),
  PERCENTUAL_COMISSAO float
);
````

Após criar a tabela conforme o enunciado, apague-a utilizando o comando:
````sql
DROP TABLE TABELA_DE_VENDEDORES2;
````

## O que aprendemos?

- Os tipos de dados que compõem uma tabela;
- Como criar uma tabela, tanto por script como por assistente;
- Como apagar uma tabela.
