1 ) Na base sucos_vendas, abra um novo script MySQL.

2 ) Digite as três consultas abaixo:
````sql
SELECT A.NOME_DO_PRODUTO FROM tabela_de_produtos A;

SELECT A.NOME_DO_PRODUTO, C.QUANTIDADE 
FROM tabela_de_produtos A
INNER JOIN itens_notas_fiscais C ON A.codigo_do_produto = C.codigo_do_produto;

SELECT A.NOME_DO_PRODUTO, YEAR(B.DATA_VENDA) AS ANO, C.QUANTIDADE 
FROM tabela_de_produtos A
INNER JOIN itens_notas_fiscais C ON A.codigo_do_produto = C.codigo_do_produto
INNER JOIN notas_fiscais B ON C.NUMERO = B.NUMERO;

SELECT A.NOME_DO_PRODUTO, YEAR(B.DATA_VENDA) AS ANO, SUM(C.QUANTIDADE) AS QUANTIDADE 
FROM tabela_de_produtos A
INNER JOIN itens_notas_fiscais C ON A.codigo_do_produto = C.codigo_do_produto
INNER JOIN notas_fiscais B ON C.NUMERO = B.NUMERO
GROUP BY A.NOME_DO_PRODUTO, YEAR(B.DATA_VENDA)
ORDER BY A.NOME_DO_PRODUTO, YEAR(B.DATA_VENDA);
````

3 ) Se você executar estas consultas, uma a uma, você verá que, a cada execução, o tempo de retorno das consultar passa a demorar cada vez mais. É que cada consulta vai exigindo mais processamento do banco de dados:

![](https://cdn3.gnarususercontent.com.br/1224-mysql-adminstracao/04/image43.png)

4 ) Na linha de comando do Windows, acesse o diretório do MySQL:
````
cd\
cd "Program Files"
cd "MySQL"
cd "MySQL 8.0"
cd Bin
````

5 ) Em seguida, acesse a interface de linha de comando do MySQL (a senha do usuário root será necessária):
````sql
mysql -uroot -p
````

6 ) Já dentro da interface de linha de comando do MySQL, digite:
````sql
explain SELECT A.NOME_DO_PRODUTO FROM tabela_de_produtos A;
````

7 ) Você verá alguns indicadores que refletem o custo de execução desta consulta.

8 ) Para visualizar em outro formato, digite:
````sql
explain format=JSON SELECT A.NOME_DO_PRODUTO FROM tabela_de_produtos A \G;
````
![](https://cdn3.gnarususercontent.com.br/1224-mysql-adminstracao/04/image38.png)

Acima, você terá o plano de execução desta consulta e o parâmetro cost_info expressa o custo de resolução desta query (no caso acima, 3.75).

9 ) Veja o custo de outra consulta. Digite:
````sql
explain format=JSON SELECT A.NOME_DO_PRODUTO, C.QUANTIDADE FROM tabela_de_produtos A INNER JOIN itens_notas_fiscais C ON A.codigo_do_produto = C.codigo_do_produto; \G;
````

![](https://cdn3.gnarususercontent.com.br/1224-mysql-adminstracao/04/image44.png)

Aqui, o custo da consulta, pelo plano de execução, passou a custar 76.517,94. Dezenas de vezes em relação à medição original.

10 ) Veja o custo de mais uma consulta. Digite:
````sql
explain format=JSON SELECT SELECT A.NOME_DO_PRODUTO, YEAR(B.DATA_VENDA) AS ANO, C.QUANTIDADE FROM tabela_de_produtos A INNER JOIN itens_notas_fiscais C ON A.codigo_do_produto = C.codigo_do_produto INNER JOIN notas_fiscais B ON C.NUMERO = B.NUMERO \G;
````
O custo aumenta mais ainda (260.242,51).

![](https://cdn3.gnarususercontent.com.br/1224-mysql-adminstracao/04/image40.png)

11 ) Você pode acompanhar o plano de execução pelo Workbench. Execute a consulta:
````sql
SELECT A.NOME_DO_PRODUTO FROM tabela_de_produtos A;
````

12 ) Exiba o resultado através da opção Execution Plan:

![](https://cdn3.gnarususercontent.com.br/1224-mysql-adminstracao/04/image22.png)

Você terá:

![](https://cdn3.gnarususercontent.com.br/1224-mysql-adminstracao/04/image16.png)

13 ) Comparar as outras consultas mais complexas. Primeiramente, execute:
````sql
SELECT A.NOME_DO_PRODUTO, C.QUANTIDADE FROM tabela_de_produtos A INNER JOIN itens_notas_fiscais C ON A.codigo_do_produto = C.codigo_do_produto;
````
14 ) Já na outra consulta mais complexa, digite:
````sql
SELECT SELECT A.NOME_DO_PRODUTO, YEAR(B.DATA_VENDA) AS ANO, C.QUANTIDADE FROM tabela_de_produtos A INNER JOIN itens_notas_fiscais C ON A.codigo_do_produto = C.codigo_do_produto INNER JOIN notas_fiscais B ON C.NUMERO = B.NUMERO
````

15 ) Quando você vê retângulos verdes, significa que a consulta utilizou algum tipo de índice. Quando você cria chaves primárias e estrangeiras, automaticamente, índices são criados e eles são usados nas consultas. Veja como isso acontece, primeiro criando três novas tabelas, com os comandos abaixo:
````sql
CREATE TABLE `itens_notas_fiscais2` (
  `NUMERO` int(11) NOT NULL,
  `CODIGO_DO_PRODUTO` varchar(10) NOT NULL,
  `QUANTIDADE` int(11) NOT NULL,
  `PRECO` float NOT NULL
) ENGINE=InnoDB DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_0900_ai_ci;

CREATE TABLE `notas_fiscais2` (
  `CPF` varchar(11) NOT NULL,
  `MATRICULA` varchar(5) NOT NULL,
  `DATA_VENDA` date DEFAULT NULL,
  `NUMERO` int(11) NOT NULL,
  `IMPOSTO` float NOT NULL
) ENGINE=InnoDB DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_0900_ai_ci;

CREATE TABLE `tabela_de_produtos2` (
  `CODIGO_DO_PRODUTO` varchar(10) NOT NULL,
  `NOME_DO_PRODUTO` varchar(50) DEFAULT NULL,
  `EMBALAGEM` varchar(20) DEFAULT NULL,
  `TAMANHO` varchar(10) DEFAULT NULL,
  `SABOR` varchar(20) DEFAULT NULL,
  `PRECO_DE_LISTA` float NOT NULL
) ENGINE=InnoDB DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_0900_ai_ci;
````

Estas tabelas são semelhantes às existentes, mas sem chaves primárias e estrangeiras.

16 ) Inclua dados nestas tabelas, executando:
````sql
INSERT INTO itens_notas_fiscais2 SELECT * FROM itens_notas_fiscais;
INSERT INTO notas_fiscais2 SELECT * FROM notas_fiscais;
INSERT INTO tabela_de_produtos2 SELECT * FROM tabela_de_produtos;
````

17 ) Observe o plano de execução da consulta original:
````sql
SELECT A.NOME_DO_PRODUTO, C.QUANTIDADE
FROM tabela_de_produtos A INNER JOIN itens_notas_fiscais C
ON A.codigo_do_produto = C.codigo_do_produto;
````

Aqui, o custo foi de 76517.94.

18 ) Já executando a consulta com as tabelas sem chaves primárias e estrangeiras:
````sql
SELECT A.NOME_DO_PRODUTO, C.QUANTIDADE
FROM tabela_de_produtos2 A INNER JOIN itens_notas_fiscais2 C
ON A.codigo_do_produto = C.codigo_do_produto;
````

O custo sobe para 769497.31.

19 ) Veja a influência do índice. Execute e veja o plano de execução:
````sql
SELECT * FROM NOTAS_FISCAIS WHERE DATA_VENDA = '20170101'
````
![](https://cdn3.gnarususercontent.com.br/1224-mysql-adminstracao/04/image7.png)

20 ) Crie o índice, executando:
````sql
ALTER TABLE NOTAS_FISCAIS ADD INDEX (DATA_VENDA);
````

21 ) Veja o plano de execução novamente:
````sql
SELECT * FROM NOTAS_FISCAIS WHERE DATA_VENDA = '20170101'
````
![](https://cdn3.gnarususercontent.com.br/1224-mysql-adminstracao/04/image3.png)

22 ) Agora, apague o índice:
````sql
ALTER TABLE NOTAS_FISCAIS DROP INDEX DATA_VENDA;
````

23 ) E execute novamente:

![](https://cdn3.gnarususercontent.com.br/1224-mysql-adminstracao/04/image11.png)

24 ) Há outra ferramenta, chamada mysqlslap, que simula acessos concorrentes a uma consulta. Você executa-o através da linha de comando. Logo, vá para:
````
cd\
cd "Program Files"
cd "MySQL"
cd "MySQL 8.0"
cd Bin
````

25 ) Execute:
````
MYSQLSLAP -uroot -p --concurrency=100 --iterations=10 --create-schema=sucos_vendas --query="SELECT * FROM NOTAS_FISCAIS WHERE DATA_VENDA = '20170101'";
````

26 ) Você terá:
````
Average number of seconds to run all queries: 0.548 seconds
Minimum number of seconds to run all queries: 0.203 seconds
Maximum number of seconds to run all queries: 1.281 seconds
Number of clients running queries: 100
Average number of queries per client: 1
````

A melhor execução da consulta retornou resultados em 0.548 segundos e a pior 1.281.

27 ) Use as tabelas sem chaves primárias e estrangeiras. Execute:
````
MYSQLSLAP -uroot -p --concurrency=100 --iterations=10 --create-schema=sucos_vendas --query="SELECT * FROM NOTAS_FISCAIS2 WHERE DATA_VENDA = '20170101'";
````

28 ) Você terá:
````
Average number of seconds to run all queries: 2.628 seconds
Minimum number of seconds to run all queries: 2.312 seconds
Maximum number of seconds to run all queries: 3.422 seconds
Number of clients running queries: 100
Average number of queries per client: 1
````

## O que aprendemos?

- O que é um índice
- Como funciona os algoritmos de Hash e BTree
- Como analisar um plano de execução
- Como o índice melhora o plano de execução
- Que as chaves primárias e estrangeiras criam índices e ajudam a melhorar o plano de execução
- A usar a ferramenta mysqlslap