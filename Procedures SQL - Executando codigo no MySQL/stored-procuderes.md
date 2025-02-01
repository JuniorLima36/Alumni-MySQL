1 ) Abra o MYSQL Workbench e crie um novo script de comandos sql.

2 ) Vamos iniciar criando algumas Stored Procedures. Clique com o botão da direita do mouse sobre Stored Procedure, abaixo do banco sucos_vendas.

![](https://cdn3.gnarususercontent.com.br/1223-mysqlproceduresefuncions/02/0.png)

3 ) Digite, após o comando <code>CREATE PROCEDURE</code>, entre as aspas, o nome da Stored Procedure (alo_mundo).

4 ) Entre o BEGIN END digite:
````sql
select 'Alô Mundo !!!!';
````

5 ) Clique em Apply. Iremos ver o comando abaixo:
````sql
USE `sucos_vendas`;
DROP procedure IF EXISTS `alo_mundo`;
DELIMITER $$
USE `sucos_vendas`$$
CREATE PROCEDURE `alo_mundo` ()
BEGIN
select 'Alô Mundo !!!!';
END$$
DELIMITER ;
````

6 ) Os comandos acima representam os comandos MYSQL para a criação da Stored Procedure. Se executarmos estes comandos direto no script MYSQL a SP (Stored Procedure) será criada.

7 ) Clique em Apply e depois Finish.

8 ) Podemos ver, abaixo do nó Stored Procedure, a mesma criada.

![](https://cdn3.gnarususercontent.com.br/1223-mysqlproceduresefuncions/02/1.png)

9 ) No Script digite e execute:
````sql
Call alo_mundo;
````

10 ) Temos o resultado:
![](https://cdn3.gnarususercontent.com.br/1223-mysqlproceduresefuncions/02/2.png)

11 ) Digite, no script SQL:
````sql
USE `sucos_vendas`;
DROP procedure IF EXISTS `mostra_numero`;
DELIMITER $$
USE `sucos_vendas`$$
CREATE PROCEDURE `mostra_numero` ()
BEGIN
select (1 + 9) - 5;
END$$
DELIMITER ;
````

Observação: Diferente um pouco dos vídeos onde as SPs foram criadas pelo assistente, aqui, no passo a passo, iremos apresentar o código MYSQL para cria a SP.

12 ) No Script digite e execute:
````sql
Call mostra_numero;
````
![](https://cdn3.gnarususercontent.com.br/1223-mysqlproceduresefuncions/02/3.png)

13 ) Vimos, aqui, uma SP que retorna uma expressão numérica.

14 ) Digite e execute:
````sql
USE `sucos_vendas`;
DROP procedure IF EXISTS `mostra_numero_alias`;
DELIMITER $$
USE `sucos_vendas`$$
CREATE PROCEDURE `mostra_numero_alias` ()
BEGIN
select (1 + 9) - 5 as RESULTADO;
END$$
DELIMITER ;
````

15 ) No Script digite e execute:
````sql
Call mostra_numero_alias;
````

![](https://cdn3.gnarususercontent.com.br/1223-mysqlproceduresefuncions/02/4.png)

Você pode ver que o resultado da SP trouxe o nome da coluna como um Alias.

16 ) Digite e execute:
````sql
USE `sucos_vendas`;
DROP procedure IF EXISTS `sp_com_funcoes`;
DELIMITER $$
USE `sucos_vendas`$$
CREATE PROCEDURE `sp_com_funcoes` ()
BEGIN
SELECT CONCAT('Alô Mundo !!!!', '.....', (1 + 9) - 5) as ITENS_COMBINADOS;
END$$
DELIMITER ;
````

17 ) No Script digite e execute:
````sql
Call sp_com_funcoes;
````
![](https://cdn3.gnarususercontent.com.br/1223-mysqlproceduresefuncions/02/5.png)

Vimos como podemos usar funções MYSQL dentro das SPs.

18 ) Digite e execute:
````sql
USE `sucos_vendas`;
DROP procedure IF EXISTS `sp_com_funcoes`;
DELIMITER $$

USE `sucos_vendas`$$
CREATE PROCEDURE `sp_com_funcoes` ()
BEGIN
SELECT CONCAT('Alô Mundo !!!!', '.....', (1 + 9) - 5) as ITENS_COMBINADOS;
END$$
DELIMITER ;
````

19 ) No Script digite e execute:
````sql
Call sp_com_funcoes;
````
![](https://cdn3.gnarususercontent.com.br/1223-mysqlproceduresefuncions/02/6.png)

Vimos como podemos usar funções MYSQL dentro das SPs.

20 ) Digite e execute:
````sql
USE `sucos_vendas`;
DROP procedure IF EXISTS `sp_com_comentarios`;
DELIMITER $$

USE `sucos_vendas`$$
CREATE PROCEDURE `sp_com_comentarios` ()
BEGIN

/* Vamos exibir itens combinados
entre textos e números */

-- Usando a função CONCAT

SELECT CONCAT('Alô Mundo !!!!', '.....', (1 + 9) - 5) as ITENS_COMBINADOS;
END$$
DELIMITER ;
````

21 ) No Script digite e execute:
````sql
Call sp_com_comentarios;
````
![](https://cdn3.gnarususercontent.com.br/1223-mysqlproceduresefuncions/02/7.png)

No exemplo acima vimos como usamos comentários dentro do código da SP.

22 ) Digite e execute:
````sql
USE `sucos_vendas`;
DROP procedure IF EXISTS `alo_mundo_2`;
DELIMITER $$

USE `sucos_vendas`$$
CREATE PROCEDURE `alo_mundo_2` ()
BEGIN
SELECT 'Alô Mundo !!!!, tudo bem?' as RESULTADO;
END$$
DELIMITER ;
````

23 ) Vamos alterar uma SP existente. Para isso digite o comando abaixo:
````sql
USE `sucos_vendas`;
DROP procedure IF EXISTS `alo_mundo_3`;
DELIMITER $$

USE `sucos_vendas`$$
CREATE PROCEDURE `alo_mundo_3`()
BEGIN
SELECT 'Alô Mundo !!!!, tudo bem? Versão 3' as RESULTADO;
END$$
DELIMITER ;
````

Note que o comando apaga a SP através de um DROP e a cria novamente com o novo código. É desta maneira que podemos alterar um SP já existente.

24 ) Como já mencionado no comando de alteração de uma SP, se quer apenas apagá-la, digite.
````sql
USE `sucos_vendas`;
DROP procedure IF EXISTS `alo_mundo_2`;
````

25 ) Podemos usar variáveis para atribuir valores e usar as mesmas nos comandos da SP. Digite e execute o comando abaixo:
````sql
USE `sucos_vendas`;
DROP procedure IF EXISTS `exibe_variavel`;
DELIMITER $$

USE `sucos_vendas`$$
CREATE PROCEDURE `exibe_variavel` ()
BEGIN
declare texto char(20) default 'Alô Mundo !!!!';
SELECT texto;
END$$
DELIMITER ;
````

Nesta SP declaramos uma variável (texto), atribuímos um valor inicial padrão e exibimos na saída.

26 ) Digite e execute:
````sql
call exibe_variavel;
````
![](https://cdn3.gnarususercontent.com.br/1223-mysqlproceduresefuncions/02/8.png)


## O que aprendemos?

- A criar uma Stored Procedure (SP) que retorna um texto;
- Como a SP retorna um valor em sua saída;
- A usar funções do MYSQL e comentários na SP;
- Como alterar uma SP já existente;
- Como excluir uma SP.