1 ) Nesta aula iremos ver exemplos de funções.

2 ) Primeiro vimos as funções do tipo texto. Veja alguns exemplos com seus respectivos retornos:
````sql
SELECT LTRIM('    OLÁ') AS RESULTADO;
````
![](https://cdn3.gnarususercontent.com.br/1221-mysqlconsultasavancadas/05/1.png)

````sql
SELECT RTRIM('OLÁ     ') AS RESULTADO;
````
![](https://cdn3.gnarususercontent.com.br/1221-mysqlconsultasavancadas/05/2.png)

````sql
SELECT TRIM('    OLÁ    ') AS RESULTADO;
````
![](https://cdn3.gnarususercontent.com.br/1221-mysqlconsultasavancadas/05/3.png)

````sql
SELECT CONCAT('OLÁ', ' ', 'TUDO BEM','?') AS RESULTADO;
````
![](https://cdn3.gnarususercontent.com.br/1221-mysqlconsultasavancadas/05/4.png)

````sql
SELECT UPPER('olá, tudo bem?') AS RESULTADO;
````
![](https://cdn3.gnarususercontent.com.br/1221-mysqlconsultasavancadas/05/5.png)

````sql
SELECT LOWER('OLÁ, TUDO BEM?') AS RESULTADO;
````
![](https://cdn3.gnarususercontent.com.br/1221-mysqlconsultasavancadas/05/6.png)

````sql
SELECT SUBSTRING('OLÁ, TUDO BEM?', 6) AS RESULTADO;
````
![](https://cdn3.gnarususercontent.com.br/1221-mysqlconsultasavancadas/05/7.png)

````sql
SELECT SUBSTRING('OLÁ, TUDO BEM?', 6, 4) AS RESULTADO;
````
![](https://cdn3.gnarususercontent.com.br/1221-mysqlconsultasavancadas/05/8.png)

````sql
SELECT CONCAT(NOME, ' (', CPF, ') ') AS RESULTADO FROM TABELA_DE_CLIENTES;
````
![](https://cdn3.gnarususercontent.com.br/1221-mysqlconsultasavancadas/05/9.png)


3 ) Temos as funções de datas. Execute os comandos abaixo:
````sql
SELECT CURDATE();
````
![](https://cdn3.gnarususercontent.com.br/1221-mysqlconsultasavancadas/05/10.png)

````sql
SELECT CURRENT_TIME();
````
![](https://cdn3.gnarususercontent.com.br/1221-mysqlconsultasavancadas/05/11.png)

````sql
SELECT CURRENT_TIMESTAMP();
````
![](https://cdn3.gnarususercontent.com.br/1221-mysqlconsultasavancadas/05/12.png)

````sql
SELECT YEAR(CURRENT_TIMESTAMP());
````
![](https://cdn3.gnarususercontent.com.br/1221-mysqlconsultasavancadas/05/13.png)

````sql
SELECT DAY(CURRENT_TIMESTAMP());
````
![](https://cdn3.gnarususercontent.com.br/1221-mysqlconsultasavancadas/05/14.png)

````sql
SELECT MONTH(CURRENT_TIMESTAMP());
````
![](https://cdn3.gnarususercontent.com.br/1221-mysqlconsultasavancadas/05/15.png)

````sql
SELECT MONTHNAME(CURRENT_TIMESTAMP());
````
![](https://cdn3.gnarususercontent.com.br/1221-mysqlconsultasavancadas/05/16.png)

````sql
SELECT DATEDIFF(CURRENT_TIMESTAMP(), '2019-01-01') AS RESULTADO;
````
![](https://cdn3.gnarususercontent.com.br/1221-mysqlconsultasavancadas/05/17.png)

````sql
SELECT DATEDIFF(CURRENT_TIMESTAMP(), '1965-09-04') AS RESULTADO;
````
![](https://cdn3.gnarususercontent.com.br/1221-mysqlconsultasavancadas/05/18.png)

````sql
SELECT CURRENT_TIMESTAMP() AS DIA_HOJE
, DATE_SUB(CURRENT_TIMESTAMP(), INTERVAL 5 DAY) AS RESULTADO;
````
![](https://cdn3.gnarususercontent.com.br/1221-mysqlconsultasavancadas/05/19.png)

````sql
SELECT DISTINCT DATA_VENDA,
DAYNAME(DATA_VENDA) AS DIA, MONTHNAME(DATA_VENDA) AS MES
, YEAR(DATA_VENDA) AS ANO FROM NOTAS_FISCAIS;
````
![](https://cdn3.gnarususercontent.com.br/1221-mysqlconsultasavancadas/05/20.png)


4 ) Alguns exemplos de funções matemáticas:
````sql
SELECT (23+((25-2)/2)*45) AS RESULTADO;
````
![](https://cdn3.gnarususercontent.com.br/1221-mysqlconsultasavancadas/05/21.png)

````sql
SELECT CEILING(12.33333232323) AS RESULTADO;
````
![](https://cdn3.gnarususercontent.com.br/1221-mysqlconsultasavancadas/05/22.png)

````sql
SELECT ROUND(12.7777232323) AS RESULTADO;
````
![](https://cdn3.gnarususercontent.com.br/1221-mysqlconsultasavancadas/05/23.png)

````sql
SELECT FLOOR(12.7777232323) AS RESULTADO;
````
![](https://cdn3.gnarususercontent.com.br/1221-mysqlconsultasavancadas/05/24.png)

````sql
SELECT RAND() AS RESULTADO;
````
![](https://cdn3.gnarususercontent.com.br/1221-mysqlconsultasavancadas/05/25.png)

````sql
SELECT NUMERO, QUANTIDADE, PRECO, QUANTIDADE * PRECO AS FATURAMENTO
FROM ITENS_NOTAS_FISCAIS;
````
![](https://cdn3.gnarususercontent.com.br/1221-mysqlconsultasavancadas/05/26.png)

````sql
SELECT NUMERO, QUANTIDADE, PRECO, ROUND(QUANTIDADE * PRECO, 2) AS FATURAMENTO
FROM ITENS_NOTAS_FISCAIS;
````
![](https://cdn3.gnarususercontent.com.br/1221-mysqlconsultasavancadas/05/27.png)


5 ) Temos também funções de conversão. Execute os exemplos abaixo:
````sql
SELECT CURRENT_TIMESTAMP() AS RESULTADO;
````
![](https://cdn3.gnarususercontent.com.br/1221-mysqlconsultasavancadas/05/28.png)

````sql
SELECT CONCAT('O dia de hoje é : ', CURRENT_TIMESTAMP()) AS RESULTADO;
````
![](https://cdn3.gnarususercontent.com.br/1221-mysqlconsultasavancadas/05/29.png)

````sql
SELECT CONCAT('O dia de hoje é : ',

DATE_FORMAT(CURRENT_TIMESTAMP(),'%W, %d/%m/%Y - %U') ) AS RESULTADO;
````
![](https://cdn3.gnarususercontent.com.br/1221-mysqlconsultasavancadas/05/30.png)

````sql
SELECT SUBSTRING(CONVERT(23.3, CHAR),1,1) AS RESULTADO;
````
![](https://cdn3.gnarususercontent.com.br/1221-mysqlconsultasavancadas/05/31.png)


## O que aprendemos?

- Algumas funções de texto;
- Funções matemáticas;
- Foi mostrado funções de datas;
- Abordamos funções de conversão.