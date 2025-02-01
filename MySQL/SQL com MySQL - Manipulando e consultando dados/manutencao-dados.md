1 ) Acesse o Workbench.

2 ) Crie uma nova consulta e digite o comando abaixo:
````sql
USE sucos;

INSERT INTO tbproduto (
PRODUTO,  NOME, EMBALAGEM, TAMANHO, SABOR,
PRECO_LISTA) VALUES (
'1040107', 'Light - 350 ml - Melância',
'Lata', '350 ml', 'Melância', 4.56);
````

O comando acima irá inserir um registro na tabela.

3 ) Execute o comando:
````sql
SELECT * FROM tbproduto;
````

Você verá que o registro foi inserido na tabela.

4 ) Crie um novo Script no Workbench.

5 ) Digite:
````sql
USE sucos;

INSERT INTO tbproduto (
PRODUTO,  NOME, EMBALAGEM, TAMANHO, SABOR,
PRECO_LISTA) VALUES (
'1037797', 'Clean - 2 Litros - Laranja',
'PET', '2 Litros', 'Laranja', 16.01);

INSERT INTO tbproduto (
PRODUTO,  NOME, EMBALAGEM, TAMANHO, SABOR,
PRECO_LISTA) VALUES (
'1000889', 'Sabor da Montanha - 700 ml - Uva',
'Garrafa', '700 ml', 'Uva', 6.31);

INSERT INTO tbproduto (
PRODUTO,  NOME, EMBALAGEM, TAMANHO, SABOR,
PRECO_LISTA) VALUES (
'1004327', 'Videira do Campo - 1,5 Litros - Melância',
'PET', '1,5 Litros', 'Melância', 19.51);
````
Agora o comando acima irá inserir diversos produtos na tabela.

6 ) Execute o comando:
````sql
SELECT * FROM tbproduto;
````

Você verá que vários registros foi inseridos na tabela.

7 ) Crie um novo Script no Workbench.

8 ) Digite o comando abaixo para inserir outros registros na tabela:
````sql
USE sucos;

INSERT INTO tbproduto (
PRODUTO,  NOME, EMBALAGEM, TAMANHO, SABOR,
PRECO_LISTA) VALUES
('544931', 'Frescor do Verão - 350 ml - Limão', 'PET', '350 ml','Limão',3.20);

INSERT INTO tbproduto (
PRODUTO,  NOME, EMBALAGEM, TAMANHO, SABOR,
PRECO_LISTA) VALUES
('1078680', 'Frescor do Verão - 470 ml - Manga', 'Lata', '470 ml','Manga',5.18);
````

9 ) Agora vamos alterar algumas informações dos registros acima incluídos. Digite:
````sql
USE sucos;

UPDATE tbproduto SET EMBALAGEM = 'Lata', PRECO_LISTA = 2.46
WHERE PRODUTO = '544931';

UPDATE tbproduto SET EMBALAGEM = 'Garrafa'
WHERE PRODUTO = '1078680';
````

10 ) Você verá que os registros foram alterados executando:
````sql
SELECT * FROM tbproduto;
````

11 ) Podemos excluir registros já existentes na tabela. Para isso digite, em um outro script do Workbench, os comandos abaixo:
````sql
USE sucos;

DELETE FROM tbproduto WHERE PRODUTO = '1078680';
````

12 ) Você verá que o registro foi apagado executando:
````sql
SELECT * FROM tbproduto;
````

13 ) Vimos, nas definições de banco de dados, que uma tabela pode ter uma chave primária. Vamos, abaixo, criar uma chave primária para a tabela de produtos. Faça em um novo script do Workbench:
````sql
USE sucos;

ALTER TABLE tbproduto ADD PRIMARY KEY (PRODUTO);
````

14 ) Execute o comando abaixo duas vezes:
````sql
INSERT INTO tbproduto (
PRODUTO,  NOME, EMBALAGEM, TAMANHO, SABOR,
PRECO_LISTA) VALUES
('1078680', 'Frescor do Verão - 470 ml - Manga', 'Lata', '470 ml','Manga',5.18);

INSERT INTO tbproduto (
PRODUTO,  NOME, EMBALAGEM, TAMANHO, SABOR,
PRECO_LISTA) VALUES
('1078680', 'Frescor do Verão - 470 ml - Manga', 'Lata', '470 ml','Manga',5.18);
````

Note que, da segunda vez, o comando não pode ser executado apresentando erro porque viola a chave primária.

15 ) Caso você deseje mudar algo neste registro deve altera-lo:
````sql
UPDATE tbproduto SET EMBALAGEM = 'Garrafa'
WHERE PRODUTO = '1078680';
````

16 ) Crie um novo script e inclua uma chave primária na tabela de clientes:
````sql
USE sucos;

ALTER TABLE tbcliente ADD PRIMARY KEY (CPF);
````

17 ) mesmo com a tabela já criada podemos incluir novas colunas com o comando:
````sql
ALTER TABLE tbcliente ADD COLUMN (DATA_NASCIMENTO DATE);
````

18 ) Abaixo temos o comando para incluir um novo cliente. Note como tratamos a inclusão de um campo do tipo data (DATA_NASCIMENTO) e do tipo lógico (PRIMEIRA_COMPRA).
````sql
INSERT INTO tbcliente (
CPF, NOME, ENDERECO1, ENDERECO2, BAIRRO, CIDADE, ESTADO, CEP, IDADE, SEXO, 
LIMITE_CREDITO, VOLUME_COMPRA, PRIMEIRA_COMPRA, DATA_NASCIMENTO)
VALUES ('00388934505','João da Silva','Rua projetada A número 10','',
'VILA ROMAN', 'CARATINGA', 'AMAZONAS','2222222',30,'M', 10000.00, 2000,
0, '1989-10-05');
````

---
##  Modificando a tabela de Vendedores

Vamos incluir novos campos na tabela de vendedores. Eles serão a data de admissão
````sql
(Nome do campo DATA_ADMISSÃO)
````

e se o vendedor está ou não de férias
````sql
(Nome do campo DE_FERIAS). 
````

Não esqueça de recriar a chave primária e depois inclua as informações abaixo:
````sql
Matrícula - 00235
Nome: Márcio Almeida Silva
Comissão: 8%
Data de admissão: 15/08/2014
Está de férias? Não

Matrícula - 00236
Nome: Cláudia Morais 
Comissão: 8%
Data de admissão: 17/09/2013
Está de férias? Sim

Matrícula - 00237
Nome: Roberta Martins
Comissão: 11%
Data de admissão: 18/03/2017
Está de férias? Sim

Matrícula - 00238
Nome: Péricles Alves
Comissão: 11%
Data de admissão: 21/08/2016
Está de férias? Não
````

---

````sql
DROP TABLE TABELA_DE_VENDEDORES;
````

````sql
CREATE TABLE TABELA_DE_VENDEDORES
( MATRICULA varchar(5),
NOME varchar(100),
PERCENTUAL_COMISSAO float,
DATA_ADMISSAO date,
DE_FERIAS bit);
````

````sql
ALTER TABLE TABELA_DE_VENDEDORES ADD PRIMARY KEY (MATRICULA);
````

````sql
INSERT INTO TABELA_DE_VENDEDORES
(MATRICULA, NOME, DATA_ADMISSAO, PERCENTUAL_COMISSAO, DE_FERIAS)
VALUES
('00235','Márcio Almeida Silva','2014-08-15',0.08,0);
````

````sql
INSERT INTO TABELA_DE_VENDEDORES
(MATRICULA, NOME, DATA_ADMISSAO, PERCENTUAL_COMISSAO, DE_FERIAS)
VALUES
('00236','Cláudia Morais','2013-09-17',0.08,1);
````

````sql
INSERT INTO TABELA_DE_VENDEDORES
(MATRICULA, NOME, DATA_ADMISSAO, PERCENTUAL_COMISSAO, DE_FERIAS)
VALUES
('00237','Roberta Martins','2017-03-18',0.11,1);
````

````sql
INSERT INTO TABELA_DE_VENDEDORES
(MATRICULA, NOME, DATA_ADMISSAO, PERCENTUAL_COMISSAO, DE_FERIAS)
VALUES
('00238','Pericles Alves','2016-08-21',0.11,0);
````

## O que aprendemos?

- Aprendemos a incluir dados em uma tabela, de diversas formas;
- Vimos como alterar um dado já existente na tabela;
- Vimos como apagar uma linha da tabela;
- Conhecemos a importância das chaves primárias e o cuidado que devemos ter ao criá-las;
- Aprendemos a manipular campos do tipo lógicos e do tipo date.