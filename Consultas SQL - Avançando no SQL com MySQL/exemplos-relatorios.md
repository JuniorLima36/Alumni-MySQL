1 ) Vamos por em prática o nosso conhecimento.

2 ) Primeiro montamos uma seleção que determina se as vendas mensais por cliente são válidas ou não. Consideramos válidas vendas abaixo da quantidade limite e não válidas acima da quantidade limite existente no cadastro do cliente. A consulta é a mostrada abaixo:
````sql
SELECT X.CPF, X.NOME, X.MES_ANO, X.QUANTIDADE_VENDAS, X.QUANTIDADE_LIMITE,
CASE WHEN (X.QUANTIDADE_LIMITE - X.QUANTIDADE_VENDAS) < 0 THEN 'INVÁLIDA'
ELSE 'VÁLIDA' END AS STATUS_VENDA
FROM (SELECT NF.CPF, TC.NOME, DATE_FORMAT(NF.DATA_VENDA, '%Y-%m') AS MES_ANO
, SUM(INF.QUANTIDADE) AS QUANTIDADE_VENDAS
, MAX(TC.VOLUME_DE_COMPRA) AS QUANTIDADE_LIMITE FROM NOTAS_FISCAIS NF
INNER JOIN ITENS_NOTAS_FISCAIS INF
ON NF.NUMERO = INF.NUMERO
INNER JOIN TABELA_DE_CLIENTES TC
ON TC.CPF = NF.CPF
GROUP BY NF.CPF, TC.NOME, DATE_FORMAT(NF.DATA_VENDA, '%Y-%m')) X;
````

![](https://cdn3.gnarususercontent.com.br/1221-mysqlconsultasavancadas/06/1.png)

3 ) Outro exemplo de relatório é o que determina a venda por sabores, para o ano de 2016, apresentando o percentual de participação de cada um destes sabores, ordenados.
````sql
SELECT VENDA_SABOR.SABOR, VENDA_SABOR.ANO, VENDA_SABOR.QUANTIDADE,
ROUND((VENDA_SABOR.QUANTIDADE/VENDA_TOTAL.QUANTIDADE) * 100, 2) AS PARTICIPACAO FROM
(SELECT TP.SABOR, YEAR(NF.DATA_VENDA) AS ANO, SUM(INF.QUANTIDADE) AS QUANTIDADE FROM
TABELA_DE_PRODUTOS TP
INNER JOIN ITENS_NOTAS_FISCAIS INF ON TP.CODIGO_DO_PRODUTO = INF.CODIGO_DO_PRODUTO
INNER JOIN NOTAS_FISCAIS NF ON NF.NUMERO = INF.NUMERO
WHERE YEAR(NF.DATA_VENDA) = 2016
GROUP BY TP.SABOR, YEAR(NF.DATA_VENDA)) AS VENDA_SABOR
INNER JOIN
(SELECT YEAR(NF.DATA_VENDA) AS ANO, SUM(INF.QUANTIDADE) AS QUANTIDADE FROM
TABELA_DE_PRODUTOS TP
INNER JOIN ITENS_NOTAS_FISCAIS INF ON TP.CODIGO_DO_PRODUTO = INF.CODIGO_DO_PRODUTO
INNER JOIN NOTAS_FISCAIS NF ON NF.NUMERO = INF.NUMERO
WHERE YEAR(NF.DATA_VENDA) = 2016
GROUP BY YEAR(NF.DATA_VENDA)) AS VENDA_TOTAL
ON VENDA_SABOR.ANO = VENDA_TOTAL.ANO
ORDER BY VENDA_SABOR.QUANTIDADE DESC
````

![](https://cdn3.gnarususercontent.com.br/1221-mysqlconsultasavancadas/06/2.png)


## O que aprendemos?

- Colocarmos em prática o nosso conhecimento montando dois relatórios conforme especificado pela empresa de suco de frutas.