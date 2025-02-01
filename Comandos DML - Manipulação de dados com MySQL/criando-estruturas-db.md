1 ) Abra o MYSQL Workbench e crie um novo script de comandos SQL.

2 ) Para criar uma base de dados podemos usar o comando CREATE. Digite o comando abaixo para criar uma nova base de dados:
````sql
CREATE DATABASE vendas_sucos;
````

3 ) Podemos usar algumas propriedades para definir o tipo de tabela de caracteres que podem ser usadas na armazenagem dos dados no banco. Digite o comando abaixo para criar um banco que utilize a tabela de caracteres UTF8:
````sql
CREATE DATABASE vendas_sucos2 DEFAULT CHARACTER SET utf8;
````

4 ) Se tivermos dúvida se o banco de dados a ser criado existe ou não, podemos usar o comando IF NOT EXISTS. Este comando é usado em diversas entidades do MYSQL e é usado para que o processo de criação aconteça apenas se o componente existe. Digite o comando abaixo para criar novo banco, somente se ele não existir:
````sql
CREATE DATABASE IF NOT exists vendas_sucos2;
````

5 ) Podemos apagar um banco de dados existente. Para isso digite o comando:
````sql
DROP DATABASE IF EXISTS vendas_sucos2;
````

6 ) Clique com o botão da direita do mouse sobre a área vazia na lista de bases de dados, a direita no Workbech, e escolha a opção Create Schema.

![](https://cdn3.gnarususercontent.com.br/1222-mysqlmanipulacaodedados/02/1.png)

7 ) Será apresentado um assistente que lhe ajuda a criar um banco de dados sem precisar usar os comandos. Digite no nome da base vendas_sucos2 e escolha as opções UTF16 para lista de caracteres.

![](https://cdn3.gnarususercontent.com.br/1222-mysqlmanipulacaodedados/02/2.png)

8 ) Clique em Apply. O comando SQL a ser executado é gerado dinamicamente. Confirme a execução e o banco será criado.

9 ) Clique com o botão da direita do mouse sobre vendas_sucos2 e escolha a opção DROP SCHEMA.

![](https://cdn3.gnarususercontent.com.br/1222-mysqlmanipulacaodedados/02/3.png)

A base será excluida com este comando.

10 ) Duplo clique sobre a base de dados vendas_sucos para que a mesma fique selecionada. O nome dela deverá ficar em negrito.

11 ) Crie um novo script de SQL e digite o comando:
````sql
USE vendas_sucos;
````

Este comando forçará a seleção da base de dados vendas_sucos;

12 ) Vamos criar a primeira tabela no nosso banco. Digite e execute:
````sql
CREATE TABLE PRODUTOS
(CODIGO VARCHAR(10) NOT NULL,
DESCRITOR VARCHAR(100) NULL,
SABOR VARCHAR(50) NULL,
TAMANHO VARCHAR(50) NULL,
EMBALAGEM VARCHAR(50) NULL,
PRECO_LISTA FLOAT NULL,
PRIMARY KEY (CODIGO));
````

13 ) Vamos criar a segunda tabela (vendedores). Digite:
````sql
CREATE TABLE VENDEDORES
(MATRICULA VARCHAR(5) NOT NULL,
NOME VARCHAR(100) NULL,
BAIRRO VARCHAR(50) NULL,
COMISSAO FLOAT NULL,
DATA_ADIMISSAO DATE NULL,
FERIAS BIT(1) NULL,
PRIMARY KEY (MATRICULA));
````

14 ) Note que houve um erro proposital ao selecionar o nome do campo que mostra a data de admissão do vendedor. Podemos alterar este nome mesmo com a tabela criada. Para isso digite execute::
````sql
ALTER TABLE VENDEDORES RENAME COLUMN DATA_ADIMISSAO TO DATA_ADMISSAO;
````

15 ) Clique com o botão da direita do mouse sobre o nó Table e selecione a opção Create Table.

![](https://cdn3.gnarususercontent.com.br/1222-mysqlmanipulacaodedados/02/4.png)

16 ) Temos a caixa de diálogo para criar uma tabela através de um assistente. Digite na caixa de diálogo:

![](https://cdn3.gnarususercontent.com.br/1222-mysqlmanipulacaodedados/02/5.png)

![](https://cdn3.gnarususercontent.com.br/1222-mysqlmanipulacaodedados/02/6.png)

![](https://cdn3.gnarususercontent.com.br/1222-mysqlmanipulacaodedados/02/7.png)

17 ) Confirme a criação da tabela acima.

18 ) Vamos criar mais uma tabela que é a tabela de vendas (Cabeçalho da nota fiscal). Para isso digite execute:
````sql
USE vendas_sucos;

CREATE TABLE TABELA_DE_VENDAS
(NUMERO VARCHAR(5) NOT NULL,
DATA_VENDA DATE NULL,
CPF VARCHAR(11) NOT NULL,
MATRICULA VARCHAR(5) NOT NULL,
IMPOSTO FLOAT NULL,
PRIMARY KEY (NUMERO));
````

19 ) Podemos criar relacionamentos entre esta tabela e a tabela de clientes e vendedores. Para isso digite e execute:
````sql
ALTER TABLE TABELA_DE_VENDAS ADD CONSTRAINT FK_CLIENTES
FOREIGN KEY (CPF) REFERENCES CLIENTES (CPF);

ALTER TABLE TABELA_DE_VENDAS ADD CONSTRAINT FK_VENDEDORES
FOREIGN KEY (MATRICULA) REFERENCES VENDEDORES (MATRICULA);
````

20 ) Da mesma maneira que fizemos em alguns passos anteriores, com o campo, o nome da tabela também pode ser alterado depois da mesma ser criada. Digite execute:
````sql
USE vendas_sucos;

ALTER TABLE tabela_de_vendas RENAME Notas;
````

## O que aprendemos?

- Aprendemos a criar o banco de dados.
- Aprendemos a criar uma tabela;
- Vimos que o nome dos campos podem ser modificados mesmo depois da tabela ter sido criada;
- Podemos criar as tabelas por um assistente. Foi mostrado isso nesta aula;
- Vimos como criar os relacionamentos entre as tabelas;
- Vimos que o nome da tabela também pode ser modificada após sua criação.