1 ) Para que possam ser efetuadas as consultas na base de dados, é preciso conhecer as suas tabelas e seus relacionamentos. Para isso, vá no Workbench e verifique se o banco de dados Sucos_Vendas está disponível.

2 ) Expandindo a árvore de estrutura de base de dados sobre Sucos_Vendas, podemos ver os componentes de um banco de dados. Para as consultas, um dos elementos mais importantes são as tabelas que podem ser vistas em mais detalhe até a sua estrutura de campos.

![](https://cdn3.gnarususercontent.com.br/1221-mysqlconsultasavancadas/02/1.png)

3 ) Vá no menu e selecione Database / Reverse Engineer.

4 ) Clique em Next duas vezes e depois escolha o banco no qual a engenharia reversa será efetuada.

5 ) Continue no assistente confirmando as seleções padrões até o final.

6 ) Você poderá ver um esquema visual das suas tabelas. Este esquema pode ser um guia para suas consultas.

![](https://cdn3.gnarususercontent.com.br/1221-mysqlconsultasavancadas/02/2.png)

7 ) Sabendo como é nossa base, podemos fazer nossas consultas. Selecione um novo script de SQL, com a base de dados selecionada, e digite:
````sql
USE sucos_vendas;
SELECT CPF, NOME, ENDERECO_1, ENDERECO_2, BAIRRO, CIDADE, ESTADO,
CEP, DATA_DE_NASCIMENTO,
IDADE, SEXO, LIMITE_DE_CREDITO, VOLUME_DE_COMPRA, PRIMEIRA_COMPRA
FROM tabela_de_clientes;
````

![](https://cdn3.gnarususercontent.com.br/1221-mysqlconsultasavancadas/02/3.png)

Aqui veremos todos os campos da tabela Tabela_de_Clientes. Isso porque os campos foram selecionados um a um.

8 ) Digite abaixo:
````sql
SELECT * FROM tabela_de_clientes;
````

![](https://cdn3.gnarususercontent.com.br/1221-mysqlconsultasavancadas/02/4.png)

Este resultado foi semelhante a consulta anterior. Isso porque, ao colocar * estamos selecionado todos os campos.

9 ) Digite:
````sql
SELECT CPF, NOME FROM tabela_de_clientes;
````
![](https://cdn3.gnarususercontent.com.br/1221-mysqlconsultasavancadas/02/5.png)

Agora podemos ver que não é necessário selecionar todos os campos de uma tabela. Basta eu destacar os campos que serão vistos.

10 ) Digite:
````sql
SELECT CPF as INDENTIFICADOR, NOME AS CLIENTE FROM tabela_de_clientes;
````

![](https://cdn3.gnarususercontent.com.br/1221-mysqlconsultasavancadas/02/6.png)

Nem sempre o nome original da coluna é o nome que queremos que seja retornado pela consulta. Por isso, podemos criar Alias (Apelidos) para os campos escrevendo algo após o comando AS.

11 ) Podemos filtrar nossa consulta. Digite:
````sql
SELECT * FROM tabela_de_produtos WHERE CODIGO_DO_PRODUTO = '1000889';
````

![](https://cdn3.gnarususercontent.com.br/1221-mysqlconsultasavancadas/02/7.png)

Aqui, o nosso retorno foi uma linha, porque selecionamos um filtro através da chave primária, que não repete.

12 ) Mas podemos implementar filtros que retornem mais linhas. Veja:
````sql
SELECT * FROM tabela_de_produtos WHERE SABOR = 'Uva';
````
![](https://cdn3.gnarususercontent.com.br/1221-mysqlconsultasavancadas/02/8.png)
````sql
SELECT * FROM tabela_de_produtos WHERE SABOR = 'Laranja';
````
![](https://cdn3.gnarususercontent.com.br/1221-mysqlconsultasavancadas/02/9.png)
````sql
SELECT * FROM tabela_de_produtos WHERE EMBALAGEM = 'PET';
````
![](https://cdn3.gnarususercontent.com.br/1221-mysqlconsultasavancadas/02/10.png)
````sql
SELECT * FROM tabela_de_produtos WHERE EMBALAGEM = 'pet';
````
![](https://cdn3.gnarususercontent.com.br/1221-mysqlconsultasavancadas/02/11.png)

Os filtros usados acima retornam mais linhas. Podemos usar qualquer coluna como critério.

13 ) Existem comandos de filtro aplicados a valores:
````sql
SELECT * FROM tabela_de_produtos WHERE PRECO_DE_LISTA > 19.50;
````
![](https://cdn3.gnarususercontent.com.br/1221-mysqlconsultasavancadas/02/12.png)
````sql
SELECT * FROM tabela_de_produtos WHERE PRECO_DE_LISTA BETWEEN 19.50 AND 19.52;
````
![](https://cdn3.gnarususercontent.com.br/1221-mysqlconsultasavancadas/02/13.png)

Neste caso podemos usar >,>=, <, <=, =, <> e Between. Assim podemos aplicar filtros sobre os valores que retornem mais valores.

14 ) É possível aplicar consultas condicionais usando operadores AND e OR. O retorno vai depender do significado do AND e OR numa estrutura lógica. Digite:
````sql
SELECT * FROM tabela_de_produtos WHERE SABOR = 'Manga'
OR TAMANHO = '470 ml';
````
![](https://cdn3.gnarususercontent.com.br/1221-mysqlconsultasavancadas/02/14.png)

Aqui retornamos ou um filtro (Sabor = Manga) ou outro ( Tamanho = 470 ml). Isso porque usamos o operador OR.

15 ) Digite:
````sql
SELECT * FROM tabela_de_produtos WHERE SABOR = 'Manga'
AND TAMANHO = '470 ml';
````
![](https://cdn3.gnarususercontent.com.br/1221-mysqlconsultasavancadas/02/15.png)

Agora, por causa do operador AND, o retorno somente ocorrerá quando as duas condições ocorrerem na mesma linha da tabela.

16 ) Podemos usar parte de um texto para ser usado como critério de localização de registros da tabela. Digite abaixo:
````sql
SELECT * FROM tabela_de_produtos WHERE SABOR LIKE '%Maça%';
````
![](https://cdn3.gnarususercontent.com.br/1221-mysqlconsultasavancadas/02/16.png)

Aqui iremos buscar todos os registros cujo sabor possua a palavra Maça. Não importa se no início, no meio ou no final do texto.

17 ) Podemos mesclar condições LIKE com outras. Digite:
````sql
SELECT * FROM tabela_de_produtos WHERE SABOR LIKE '%Maça%'
AND EMBALAGEM = 'PET';
````
![](https://cdn3.gnarususercontent.com.br/1221-mysqlconsultasavancadas/02/17.png)

Por fim, faremos a consulta do texto “Maça” apenas para embalagens PET.


## O que aprendemos?

- A importância de conhecer a base de dados antes de fazer as consultas;
- O comando de consultas e como podemos filtrá-las;
- Como podemos mesclar filtros condicionais com AND e OR;
- A usar >, >=, <, <=, = ou <> nos filtros que envolvem valores;
- Como funciona o comando LIKE;