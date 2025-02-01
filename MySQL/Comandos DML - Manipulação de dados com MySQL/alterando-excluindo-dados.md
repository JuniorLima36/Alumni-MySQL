1 ) Vamos verificar a lista de produtos.
````sql
SELECT * FROM produtos;
````

![](https://cdn3.gnarususercontent.com.br/1222-mysqlmanipulacaodedados/04/1.png)

2 ) Vamos alterar o preço de lista de um dos produtos. Para isso digite:
````sql
UPDATE produtos SET PRECO_LISTA = 5 WHERE CODIGO = '1000889';
````

3 ) Podemos alterar os dados da tabela em forma de lote. Digite e execute:
````sql
UPDATE produtos SET EMBALAGEM = 'PET', TAMANHO = '1 Litro', DESCRITOR =

'Sabor da Montanha - 1 Litro - Uva' WHERE CODIGO = '1000889';
````

4 ) Também podemos alterar o preço de lista baseado no mesmo campo que será alterado. Digite e execute:
````sql
UPDATE produtos SET PRECO_LISTA = PRECO_LISTA * 1.10 WHERE SABOR = 'Maracujá';
````

5 ) Da mesma maneira que incluímos dados na tabela baseado nos dados de uma outra tabela, podemos também alterar dados desta mesma maneira. Digite e execute:
````sql
UPDATE VENDEDORES A INNER JOIN SUCOS_VENDAS.TABELA_DE_VENDEDORES B

ON A.MATRICULA = SUBSTRING(B.MATRICULA,3,3)

SET A.FERIAS = B.DE_FERIAS;
````

6 ) É possível apagar dados da tabela. Antes disto vamos incluir novos registros que depois serão excluídos. Digite e execute:
````sql
INSERT INTO PRODUTOS (CODIGO,DESCRITOR,SABOR,TAMANHO,EMBALAGEM,PRECO_LISTA)

  VALUES ('1001001','Sabor dos Alpes 700 ml - Manga','Manga','700 ml','Garrafa',7.50),

    ('1001000','Sabor dos Alpes 700 ml - Melão','Melão','700 ml','Garrafa',7.50),

    ('1001002','Sabor dos Alpes 700 ml - Graviola','Graviola','700 ml','Garrafa',7.50),

    ('1001003','Sabor dos Alpes 700 ml - Tangerina','Tangerina','700 ml','Garrafa',7.50),

    ('1001004','Sabor dos Alpes 700 ml - Abacate','Abacate','700 ml','Garrafa',7.50),

    ('1001005','Sabor dos Alpes 700 ml - Açai','Açai','700 ml','Garrafa',7.50),

    ('1001006','Sabor dos Alpes 1 Litro - Manga','Manga','1 Litro','Garrafa',7.50),

    ('1001007','Sabor dos Alpes 1 Litro - Melão','Melão','1 Litro','Garrafa',7.50),

    ('1001008','Sabor dos Alpes 1 Litro - Graviola','Graviola','1 Litro','Garrafa',7.50),

    ('1001009','Sabor dos Alpes 1 Litro - Tangerina','Tangerina','1 Litro','Garrafa',7.50),

    ('1001010','Sabor dos Alpes 1 Litro - Abacate','Abacate','1 Litro','Garrafa',7.50),

    ('1001011','Sabor dos Alpes 1 Litro - Açai','Açai','1 Litro','Garrafa',7.50);
````

7 ) Vamos apagar um registro apenas. Digite e execute:
````sql
DELETE FROM PRODUTOS WHERE CODIGO = '1001000';
````

8 ) Podemos aplicar um filtro para selecionar dados a serem excluidos. Digite e execute:
````sql
DELETE FROM PRODUTOS WHERE TAMANHO = '1 Litro' AND SUBSTRING(DESCRITOR,1,15) = 'Sabor dos Alpes';
````

9 ) Outra forma é apagar usando a seleção de dados de outra tabela. Digite e execute:
````sql
DELETE FROM PRODUTOS WHERE CODIGO NOT IN ( SELECT CODIGO_DO_PRODUTO FROM SUCOS_VENDAS.TABELA_DE_PRODUTOS);
````

10) Os comandos UPDATE e DELETE podem ser executados sobre a tabela inteira. Vamos então criar uma tabela de forma temporária para depois alterá-la e apagá-la. Digite e execute:
````sql
CREATE TABLE `produtos2` (

  `CODIGO` varchar(10) NOT NULL,

  `DESCRITOR` varchar(100) DEFAULT NULL,

  `SABOR` varchar(50) DEFAULT NULL,

  `TAMANHO` varchar(50) DEFAULT NULL,

  `EMBALAGEM` varchar(50) DEFAULT NULL,

  `PRECO_LISTA` float DEFAULT NULL,

  PRIMARY KEY (`CODIGO`)

) ;
````

11 ) Depois inclua os dados nesta tabela:
````sql
INSERT INTO produtos2 SELECT * FROM produtos;
````

12 ) Altere os dados para toda a tabela:
````sql
UPDATE produtos2 SET preco_lista = 8;
````

13 ) O comando abaixo apaga todos os registros da tabela. Digite o comando abaixo e execute para apagar os dados da tabela:
````sql
DELETE FROM produtos2;
````

14 ) Vamos criar uma transação. Digite e execute o comando abaixo para iniciar uma transação:
````sql
START TRANSACTION;
````

15 ) Vamos verificar a tabela de vendedores:
````sql
SELECT * FROM VENDEDORES;
````
![](https://cdn3.gnarususercontent.com.br/1222-mysqlmanipulacaodedados/04/2.png)

16 ) Modifique os dados referentes a comissão. Digite e execute:
````sql
UPDATE VENDEDORES SET COMISSAO = COMISSAO * 1.15;


SELECT * FROM VENDEDORES;
````
![](https://cdn3.gnarususercontent.com.br/1222-mysqlmanipulacaodedados/04/3.png)

17 ) Vamos refazer o comando acima. Digite e execute:
````sql
ROLLBACK;
````

18 ) Verifique a tabela. Digite e execute:
````sql
SELECT * FROM VENDEDORES;
````
![](https://cdn3.gnarususercontent.com.br/1222-mysqlmanipulacaodedados/04/4.png)

19 ) Vamos repetir a modificação iniciando nova transação. Digite e execute:
````sql
START TRANSACTION;

UPDATE VENDEDORES SET COMISSAO = COMISSAO * 1.15;

SELECT * FROM VENDEDORES;
````
![](https://cdn3.gnarususercontent.com.br/1222-mysqlmanipulacaodedados/04/5.png)

20 ) Agora iremos confirmar a inclusão destes dados. Para isso digite:
````sql
COMMIT;
````

21 ) Verifique novamente a tabela. Para isso digite:
````sql
SELECT * FROM VENDEDORES;
````
![](https://cdn3.gnarususercontent.com.br/1222-mysqlmanipulacaodedados/04/6.png)

## O que aprendemos?

- Alterar e excluir dados de uma tabela, através de comando ou em lotes;
- Vimos que podemos alterar ou excluir todos os dados de uma tabela;
- O que é uma transação e como podemos desfazer modificações efetuadas anteriormente na base de dados.