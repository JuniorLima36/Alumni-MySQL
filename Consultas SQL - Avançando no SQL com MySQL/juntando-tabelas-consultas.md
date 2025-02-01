1 ) Aqui veremos como conectar as consultas de tabelas diferentes. Chamamos esta união de JOIN.

2 ) Veja o conteúdo de duas tabelas digitando os comandos abaixo:
````sql
SELECT * FROM tabela_de_vendedores;
````
![](https://cdn3.gnarususercontent.com.br/1221-mysqlconsultasavancadas/04/1.png)
````sql
SELECT * FROM notas_fiscais;
````
![](https://cdn3.gnarususercontent.com.br/1221-mysqlconsultasavancadas/04/2.png)

3 ) Podemos conectar essas duas tabelas pelo campo em comum (MATRICULA). Digite:
````sql
SELECT * FROM tabela_de_vendedores A
INNER JOIN notas_fiscais B
ON A.MATRICULA = B.MATRICULA;
````
![](https://cdn3.gnarususercontent.com.br/1221-mysqlconsultasavancadas/04/3.png)

4 ) Podemos aplicar agrupamentos ao resultado da consulta que conecta uma ou mais tabelas:
````sql
SELECT A.MATRICULA, A.NOME, COUNT(*) FROM
tabela_de_vendedores A
INNER JOIN notas_fiscais B
ON A.MATRICULA = B.MATRICULA
GROUP BY A.MATRICULA, A.NOME;
````
![](https://cdn3.gnarususercontent.com.br/1221-mysqlconsultasavancadas/04/4.png)

5 ) Nem sempre todas as linhas podem ser conectadas. Existem outros tipos de JOINs que nos permite identificar quem não pode ser conectado. Veja a consulta abaixo:
````sql
SELECT COUNT(*) FROM tabela_de_clientes;
````
![](https://cdn3.gnarususercontent.com.br/1221-mysqlconsultasavancadas/04/5.png)

Ela mostra que temos 15 clientes.

6 ) Vamos fazer um JOIN com a tabela de notas fiscais e ver quantos clientes possuem notas emitidas. Digite:

![](https://cdn3.gnarususercontent.com.br/1221-mysqlconsultasavancadas/04/6.png)

Se você contar verá que, na consulta acima, temos 14 linhas. Existe um cliente que está no cadastro mas não teve nota fiscal emitida.

7 ) Podemos usar o LEFT JOIN. Digite:
````sql
SELECT DISTINCT A.CPF, A.NOME, B.CPF FROM tabela_de_clientes A
LEFT JOIN notas_fiscais B ON A.CPF = B.CPF
````
![](https://cdn3.gnarususercontent.com.br/1221-mysqlconsultasavancadas/04/7.png)

O cliente que possui o CPF vindo da tabela de notas com o valor nulo, é o cliente que nunca emitiu nota fiscal.

8 ) A seleção correta seria:
````sql
SELECT DISTINCT A.CPF, A.NOME, B.CPF FROM tabela_de_clientes A
LEFT JOIN notas_fiscais B ON A.CPF = B.CPF
WHERE B.CPF IS NULL;
````
![](https://cdn3.gnarususercontent.com.br/1221-mysqlconsultasavancadas/04/8.png)

9 ) Podemos juntar duas ou mais consultas, Desde que os campos selecionados sejam os mesmos. Digite:
````sql
SELECT DISTINCT BAIRRO FROM tabela_de_clientes
UNION
SELECT DISTINCT BAIRRO FROM tabela_de_vendedores;
````
![](https://cdn3.gnarususercontent.com.br/1221-mysqlconsultasavancadas/04/9.png)

10 ) O UNION ALL não faz a seleção com um DISTINCT. As linhas se repetem se existirem em ambas as tabelas. Digite:
````sql
SELECT DISTINCT BAIRRO FROM tabela_de_clientes
UNION ALL
SELECT DISTINCT BAIRRO FROM tabela_de_vendedores;
````
![](https://cdn3.gnarususercontent.com.br/1221-mysqlconsultasavancadas/04/10.png)

Veja que Santo Amaro aparece duas vezes. Uma vindo da tabela de clientes e outra da tabela de produtos.

11 ) Podemos simular o FULL JOIN, que não é suportado pelo MYSQL, usando o LEFT JOIN e RIGHT JOIN com UNION. Digite:
````sql
SELECT tabela_de_vendedores.BAIRRO,
tabela_de_vendedores.NOME, DE_FERIAS,
tabela_de_clientes.BAIRRO,
tabela_de_clientes.NOME  FROM tabela_de_vendedores LEFT JOIN tabela_de_clientes
ON tabela_de_vendedores.BAIRRO = tabela_de_clientes.BAIRRO
UNION
SELECT tabela_de_vendedores.BAIRRO,
tabela_de_vendedores.NOME, DE_FERIAS,
tabela_de_clientes.BAIRRO,
tabela_de_clientes.NOME  FROM tabela_de_vendedores RIGHT JOIN tabela_de_clientes
ON tabela_de_vendedores.BAIRRO = tabela_de_clientes.BAIRRO;
````
![](https://cdn3.gnarususercontent.com.br/1221-mysqlconsultasavancadas/04/11.png)

12 ) As sub-consultas permitem que possa ser feita seleções usando como critérios outras seleções. Digite:
````sql
SELECT * FROM tabela_de_clientes WHERE BAIRRO 
IN (SELECT DISTINCT BAIRRO FROM tabela_de_vendedores);
````
![](https://cdn3.gnarususercontent.com.br/1221-mysqlconsultasavancadas/04/12.png)

13 ) Podemos aplicar uma consulta, em vez de sobre uma tabela, sobre outra consulta. Digite:
````sql
SELECT X.EMBALAGEM, X.PRECO_MAXIMO FROM 
(SELECT EMBALAGEM, MAX(PRECO_DE_LISTA) AS PRECO_MAXIMO FROM tabela_de_produtos
GROUP BY EMBALAGEM) X WHERE X.PRECO_MAXIMO >= 10;
````
![](https://cdn3.gnarususercontent.com.br/1221-mysqlconsultasavancadas/04/13.png)

14 ) Podemos transformar uma consulta numa visão (View) que depois pode ser usada em outras consultas como uma tabela. Crie a visão. Para isso, expanda na árvore do canto esquerdo, onde temos o nome do banco, e vá em Views.

![](https://cdn3.gnarususercontent.com.br/1221-mysqlconsultasavancadas/04/14.png)

15 ) Botão da direita do mouse sobre Views e crie uma nova visão.

![](https://cdn3.gnarususercontent.com.br/1221-mysqlconsultasavancadas/04/15.png)

16 ) Digite o seguinte comando:
````sql
CREATE VIEW `VW_MAIORES_EMBALAGENS` AS
SELECT EMBALAGEM, MAX(PRECO_DE_LISTA) AS PRECO_MAXIMO FROM tabela_de_produtos
GROUP BY EMBALAGEM
````
17 ) Clique em Apply e siga os passos até a criação da visão.

18 ) Podemos manipular a visão como uma tabela. Digite:
````sql
SELECT * FROM VW_MAIORES_EMBALAGENS;
````
![](https://cdn3.gnarususercontent.com.br/1221-mysqlconsultasavancadas/04/16.png)

19 ) Logo a consulta:
````sql
SELECT X.EMBALAGEM, X.PRECO_MAXIMO FROM 
(SELECT EMBALAGEM, MAX(PRECO_DE_LISTA) AS PRECO_MAXIMO FROM tabela_de_produtos
GROUP BY EMBALAGEM) X WHERE X.PRECO_MAXIMO >= 10;
````
![](https://cdn3.gnarususercontent.com.br/1221-mysqlconsultasavancadas/04/17.png)

Pode ser substituída por:
````sql
SELECT X.EMBALAGEM, X.PRECO_MAXIMO FROM 
VW_MAIORES_EMBALAGENS X WHERE X.PRECO_MAXIMO >= 10;
````
![](https://cdn3.gnarususercontent.com.br/1221-mysqlconsultasavancadas/04/18.png)


## O que aprendemos?

- Como conectar duas ou mais tabelas através de JOINs;
- Os tipos de JOINs existentes e quais são suportados pelo MYSQL;
- Os comandos UNION e UNION ALL, para juntar duas ou mais seleções desde que tenham os mesmos campos selecionados;
- Usar uma consulta como critério de filtro de outra consulta;
- Como usar uma consulta dentro de outra consulta;
- Criar e usar visões (Views);