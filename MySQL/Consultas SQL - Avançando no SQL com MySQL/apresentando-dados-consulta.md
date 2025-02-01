1 ) Voltando ao Workbench, vamos ver formas diferentes de exibir os resultados. Digite:
````sql
SELECT EMBALAGEM, TAMANHO FROM tabela_de_produtos;
````
![](https://cdn3.gnarususercontent.com.br/1221-mysqlconsultasavancadas/03/1.png)

Veja que temos linhas onde o conjunto EMBALAGEM / TAMANHO se repete.

2 ) Agora digite o comando:
````sql
SELECT DISTINCT EMBALAGEM, TAMANHO FROM tabela_de_produtos;
````
![](https://cdn3.gnarususercontent.com.br/1221-mysqlconsultasavancadas/03/2.png)

O simples fato de incluirmos a cláusula DISTINCT faz com que os registros não se repitam.

3 ) Podemos aplicar filtros a seleção com DISTINCT.
````sql
SELECT DISTINCT EMBALAGEM, TAMANHO FROM tabela_de_produtos
WHERE SABOR = 'Laranja';
````
![](https://cdn3.gnarususercontent.com.br/1221-mysqlconsultasavancadas/03/3.png)

4 ) E podemos acrescentar mais campos à seleção DISTINCT.
````sql
SELECT DISTINCT EMBALAGEM, TAMANHO, SABOR FROM tabela_de_produtos;
````
![](https://cdn3.gnarususercontent.com.br/1221-mysqlconsultasavancadas/03/4.png)

5 ) Podemos limitar o número de linhas exibidas na saída. Digite:
````sql
SELECT * FROM tabela_de_produtos LIMIT 5;
````
![](https://cdn3.gnarususercontent.com.br/1221-mysqlconsultasavancadas/03/5.png)

Temos acima nossa saída limitada aos primeiros 5 registros.

6 ) Podemos exibir os registros dentro de um intervalo de linhas. Digite:
````sql
SELECT * FROM tabela_de_produtos LIMIT 2,3;
````
![](https://cdn3.gnarususercontent.com.br/1221-mysqlconsultasavancadas/03/6.png)

7 ) As saídas de uma comando SELECT podem ser apresentadas de forma ordenada. Veja abaixo:
````sql
SELECT * FROM tabela_de_produtos ORDER BY PRECO_DE_LISTA;
````
![](https://cdn3.gnarususercontent.com.br/1221-mysqlconsultasavancadas/03/7.png)

Temos os valores ordenados por preço de lista, do menor para o maior.

8 ) Podemos mudar esta ordem. Digite:
````sql
SELECT * FROM tabela_de_produtos ORDER BY PRECO_DE_LISTA DESC;
````
![](https://cdn3.gnarususercontent.com.br/1221-mysqlconsultasavancadas/03/8.png)

9 ) Os valores podem vir ordenados alfabeticamente quando incluímos um campo texto no critério de ordenação. Digite:
````sql
SELECT * FROM tabela_de_produtos ORDER BY NOME_DO_PRODUTO;
````
![](https://cdn3.gnarususercontent.com.br/1221-mysqlconsultasavancadas/03/9.png)

10 ) Também, no critério de ordenação do tipo texto, podemos mudar a ordem para do maior para o menor. Digite:
````sql
SELECT * FROM tabela_de_produtos ORDER BY NOME_DO_PRODUTO DESC;
````
![](https://cdn3.gnarususercontent.com.br/1221-mysqlconsultasavancadas/03/10.png)

11 ) O critério de ordenação pode ser diferente para cada tipo. Veja o exemplo abaixo onde usamos dois campos como critério de ordenação e a ordem diferente para cada um deles:
````sql
SELECT * FROM tabela_de_produtos ORDER BY EMBALAGEM DESC, NOME_DO_PRODUTO ASC;
````
![](https://cdn3.gnarususercontent.com.br/1221-mysqlconsultasavancadas/03/11.png)

12 ) Os dados podem ser agrupados. Quando isso acontece, temos que aplicar um critério de agrupamento para os campos numéricos. Podemos usar SUM, AVG, MAX, MIN, e outros mais. Digite o comando abaixo:
````sql
SELECT ESTADO, LIMITE_DE_CREDITO FROM tabela_de_clientes;
````
![](https://cdn3.gnarususercontent.com.br/1221-mysqlconsultasavancadas/03/12.png)

Note que temos várias linhas para RJ e SP. Como fazemos para somar todos os limites de crédito para RJ e SP?

13 ) A solução está no comando abaixo:
````sql
SELECT ESTADO, SUM(LIMITE_DE_CREDITO) AS LIMITE_TOTAL FROM tabela_de_clientes GROUP BY ESTADO;
````
![](https://cdn3.gnarususercontent.com.br/1221-mysqlconsultasavancadas/03/13.png)

14 ) Podemos usar outros critérios como o valor máximo.
````sql
SELECT EMBALAGEM, MAX(PRECO_DE_LISTA) AS MAIOR_PRECO FROM tabela_de_Produtos GROUP BY EMBALAGEM;
````
![](https://cdn3.gnarususercontent.com.br/1221-mysqlconsultasavancadas/03/14.png)

Aqui vemos o maior preço de lista para cada tipo de embalagem.

15 ) O comando COUNT conta o número de ocorrências na tabela. Digite:
````sql
SELECT EMBALAGEM, COUNT(*) AS CONTADOR FROM tabela_de_produtos GROUP BY EMBALAGEM;
````
![](https://cdn3.gnarususercontent.com.br/1221-mysqlconsultasavancadas/03/15.png)

Temos acima o número de produtos PET, Garrafa e Lata.

16 ) O filtro pode ser aplicado sobre o agrupamento, como uma consulta qualquer. Digite:
````sql
SELECT BAIRRO, SUM(LIMITE_DE_CREDITO) AS LIMITE FROM tabela_de_clientes
WHERE CIDADE = 'Rio de Janeiro' GROUP BY BAIRRO;
````
![](https://cdn3.gnarususercontent.com.br/1221-mysqlconsultasavancadas/03/16.png)

17 ) Além disso, o agrupamento também pode ser feito por mais de um campo. Digite:
````sql
SELECT ESTADO, BAIRRO, SUM(LIMITE_DE_CREDITO) AS LIMITE FROM tabela_de_clientes
GROUP BY ESTADO, BAIRRO;
````
![](https://cdn3.gnarususercontent.com.br/1221-mysqlconsultasavancadas/03/17.png)

18 ) Podemos mesclar agrupamento com ordenação. Digite:
````sql
SELECT ESTADO, BAIRRO, SUM(LIMITE_DE_CREDITO) AS LIMITE FROM tabela_de_clientes
WHERE CIDADE = 'Rio de Janeiro'
GROUP BY ESTADO, BAIRRO
ORDER BY BAIRRO;
````
![](https://cdn3.gnarususercontent.com.br/1221-mysqlconsultasavancadas/03/18.png)

19 ) Veja a consulta abaixo:
````sql
SELECT ESTADO, SUM(LIMITE_DE_CREDITO) AS SOMA_LIMITE FROM tabela_de_clientes
GROUP BY ESTADO;
````
![](https://cdn3.gnarususercontent.com.br/1221-mysqlconsultasavancadas/03/19.png)

20 ) Queremos aplicar um filtro sobre o resultado desta consulta. Logo digite:
````sql
SELECT ESTADO, SUM(LIMITE_DE_CREDITO) AS SOMA_LIMITE FROM tabela_de_clientes
WHERE SOMA_LIMITE > 900000
GROUP BY ESTADO;
````
Veja que a consulta acima vai ocasionar um erro.

21 ) Usamos o HAVING para filtrar a saída de uma consulta usando como critério o valor agrupado. Digite:
````sql
SELECT ESTADO, SUM(LIMITE_DE_CREDITO) AS SOMA_LIMITE FROM tabela_de_clientes
GROUP BY ESTADO HAVING SUM(LIMITE_DE_CREDITO) > 900000;
````
![](https://cdn3.gnarususercontent.com.br/1221-mysqlconsultasavancadas/03/20.png)

22 ) O critério usado no HAVING não precisa ser o mesmo usado no filtro. Veja o comando abaixo:
````sql
SELECT EMBALAGEM, MAX(PRECO_DE_LISTA) AS MAIOR_PRECO,
MIN(PRECO_DE_LISTA) AS MENOR_PRECO FROM tabela_de_produtos
GROUP BY EMBALAGEM;
````
![](https://cdn3.gnarususercontent.com.br/1221-mysqlconsultasavancadas/03/21.png)

Ele usa o MIN para agrupamento.

23 ) Porém, na consulta abaixo, o critério do HAVING pede a soma. Digite:
````sql
SELECT EMBALAGEM, MAX(PRECO_DE_LISTA) AS MAIOR_PRECO,
MIN(PRECO_DE_LISTA) AS MENOR_PRECO FROM tabela_de_produtos
GROUP BY EMBALAGEM HAVING SUM(PRECO_DE_LISTA) <= 80;
````
![](https://cdn3.gnarususercontent.com.br/1221-mysqlconsultasavancadas/03/22.png)

24 ) No HAVING podemos usar mais de um critério usando AND ou OR.
````sql
SELECT EMBALAGEM, MAX(PRECO_DE_LISTA) AS MAIOR_PRECO,
MIN(PRECO_DE_LISTA) AS MENOR_PRECO FROM tabela_de_produtos
GROUP BY EMBALAGEM HAVING SUM(PRECO_DE_LISTA) <= 80 AND MAX(PRECO_DE_LISTA) >= 5;
````
![](https://cdn3.gnarususercontent.com.br/1221-mysqlconsultasavancadas/03/23.png)

25 ) O comando CASE permite que possa ser classificado cada registro da tabela. Digite o comando abaixo:
````sql
SELECT NOME_DO_PRODUTO, PRECO_DE_LISTA,
CASE
   WHEN PRECO_DE_LISTA >= 12 THEN 'PRODUTO CARO'
   WHEN PRECO_DE_LISTA >= 7 AND PRECO_DE_LISTA < 12 THEN 'PRODUTO EM CONTA'
   ELSE 'PRODUTO BARATO'
END AS STATUS_PRECO
FROM tabela_de_produtos;
````
![](https://cdn3.gnarususercontent.com.br/1221-mysqlconsultasavancadas/03/24.png)

Com o CASE foi possível classificar os produtos como CARO, BARATO ou EM CONTA conforme o valor do seu preço de lista.

26 ) Podemos usar o CASE como critério de agrupamento, Digite o comando abaixo:
````sql
SELECT EMBALAGEM,
CASE
   WHEN PRECO_DE_LISTA >= 12 THEN 'PRODUTO CARO'
   WHEN PRECO_DE_LISTA >= 7 AND PRECO_DE_LISTA < 12 THEN 'PRODUTO EM CONTA'
   ELSE 'PRODUTO BARATO'
END AS STATUS_PRECO, AVG(PRECO_DE_LISTA) AS PRECO_MEDIO
FROM tabela_de_produtos
WHERE sabor = 'Manga'
GROUP BY EMBALAGEM,
CASE
   WHEN PRECO_DE_LISTA >= 12 THEN 'PRODUTO CARO'
   WHEN PRECO_DE_LISTA >= 7 AND PRECO_DE_LISTA < 12 THEN 'PRODUTO EM CONTA'
   ELSE 'PRODUTO BARATO'
END
ORDER BY EMBALAGEM;
````
![](https://cdn3.gnarususercontent.com.br/1221-mysqlconsultasavancadas/03/25.png)


## O que aprendemos?

- Como apresentar somente linhas distintas numa seleção;
- Como ordenar a saída da seleção;
- Como agrupar linhas por um conjunto de campos e aplicando um critério de agrupamento sobre os campos numéricos (SUM, MIN, MAX, AVG, etc ..).
- Como utilizar o comando HAVING para aplicar um filtro usando os campos numéricos agrupados como condição.
- Como limitar a saída das consultas;
- Como usar o CASE para classificar um determinado campo por um critério.