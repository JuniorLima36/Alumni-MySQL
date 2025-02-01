1 ) Abra um novo script MYSQL.

2 ) Digite e execute:
````sql
USE `sucos_vendas`;
DROP procedure IF EXISTS `cliente_novo_velho`;
DELIMITER $$

USE `sucos_vendas`$$
CREATE PROCEDURE `cliente_novo_velho`(vCPF VARCHAR(20))
BEGIN
   DECLARE vResultado VARCHAR(20);
   DECLARE vDataNascimento DATE;
   SELECT DATA_DE_NASCIMENTO INTO vDataNascimento FROM
   tabela_de_clientes WHERE CPF = vCPF;
   IF vDataNascimento < '20000101' THEN
      SET vResultado = 'CLIENTE VELHO';
   ELSE
      SET vResultado = 'CLIENTE NOVO';
   END IF;
   SELECT vResultado;
END$$
DELIMITER ;
````

2 ) Execute a SP.
````sql
Call cliente_novo_velho ('19290992743');
````
![](https://cdn3.gnarususercontent.com.br/1223-mysqlproceduresefuncions/04/0.png)

3 ) Esta SP usa a estrutura IF-THEN-ELSE para classificar um cliente como sendo novo ou velho, baseado em sua idade.

4 ) Vamos ver outra estrutura de controle de fluxo. Digite e execute:
````sql
USE `sucos_vendas`;
DROP procedure IF EXISTS `acha_status_preco_2`;
DELIMITER $$

USE `sucos_vendas`$$
CREATE PROCEDURE `acha_status_preco_2` (vProduto VARCHAR(50))
BEGIN
   DECLARE vPreco FLOAT;
   DECLARE vMensagem VARCHAR(30);
   SELECT PRECO_DE_LISTA INTO vPreco FROM tabela_de_produtos
   WHERE codigo_do_produto = vProduto;
   IF vPreco >= 12 THEN
      SET vMensagem = 'PRODUTO CARO.';
   ELSEIF vPreco >= 7  AND vPreco < 12 THEN
      SET vMensagem = 'PRODUTO EM CONTA.';
   ELSE
      SET vMensagem = 'PRODUTO BARATO.';
   END IF;
   SELECT vMensagem;
END$$
DELIMITER ;
````

5 ) Digite e execute:
````sql
Call acha_status_preco_2 ('1000889');
````

6 ) Observe que a estrutura <code>IF-THEN-ELSEIF</code> permite encadear diversos testes.

7 ) O encadeamento de condições pode ser expresso, também, usando o comando CASE-END-CASE. Para isso digite e execute:
````sql
USE `sucos_vendas`;
DROP procedure IF EXISTS `acha_tipo_sabor`;
DELIMITER $$

USE `sucos_vendas`$$
CREATE PROCEDURE `acha_tipo_sabor`(vProduto VARCHAR(50))
BEGIN
  DECLARE vSabor VARCHAR(50);
  SELECT SABOR INTO vSabor FROM tabela_de_Produtos
  WHERE codigo_do_produto = vProduto;
  CASE vSabor
  WHEN 'Lima/Limão' THEN SELECT 'Cítrico';
  WHEN 'Laranja' THEN SELECT 'Cítrico';
  WHEN 'Morango/Limão' THEN SELECT 'Cítrico';
  WHEN 'Uva' THEN SELECT 'Neutro';
  WHEN 'Morango' THEN SELECT 'Neutro';
  ELSE SELECT 'Ácidos';
  END CASE;
END$$
DELIMITER ;
````

8 ) Digite e execute:
````sql
CALL acha_tipo_sabor('1000889');
````

9 ) Uma estrutura derivada da mostrada é o CASE-NOT-FOUND. Para isso vamos criar a SP Acha_Tipo_Sabor_Erro. Digite e execute:
````sql
USE `sucos_vendas`;
DROP procedure IF EXISTS `acha_tipo_sabor_erro`;
DELIMITER $$

USE `sucos_vendas`$$
CREATE  PROCEDURE `acha_tipo_sabor_erro`(vProduto VARCHAR(50))
BEGIN
  DECLARE vSabor VARCHAR(50);
  SELECT SABOR INTO vSabor FROM tabela_de_Produtos
  WHERE codigo_do_produto = vProduto;
  CASE vSabor
  WHEN 'Lima/Limão' THEN SELECT 'Cítrico';
  WHEN 'Laranja' THEN SELECT 'Cítrico';
  WHEN 'Morango/Limão' THEN SELECT 'Cítrico';
  WHEN 'Uva' THEN SELECT 'Neutro';
  WHEN 'Morango' THEN SELECT 'Neutro';
  END CASE;
END$$
DELIMITER ;
````

10 ) Esta SP difere da anterior apenas porque foi retirada a linha abaixo.
````sql
ELSE SELECT 'Ácidos';
````

Estamos criando uma situação onde nenhuma das condições podem ser satisfeitas.

11 ) Execute a SP:
````sql
CALL acha_tipo_sabor_erro('1004327');
````

12 ) Temos o erro:

![](https://cdn3.gnarususercontent.com.br/1223-mysqlproceduresefuncions/04/1.png)

13 ) Para evitar de não incluirmos opções no CASE que contemplem todas as situações podemos acrescentar o tratamento de erro. Altere a SP executando:
````sql
USE `sucos_vendas`;
DROP procedure IF EXISTS `acha_tipo_sabor_erro`;
DELIMITER $$

USE `sucos_vendas`$$
CREATE  PROCEDURE `acha_tipo_sabor_erro`(vProduto VARCHAR(50))
BEGIN
  DECLARE vSabor VARCHAR(50);
  DECLARE msgErro VARCHAR(30);
  DECLARE CONTINUE HANDLER FOR 1339 SET msgErro = 'O case não está completo';
  SELECT SABOR INTO vSabor FROM tabela_de_Produtos
  WHERE codigo_do_produto = vProduto;
  CASE vSabor
  WHEN 'Lima/Limão' THEN SELECT 'Cítrico';
  WHEN 'Laranja' THEN SELECT 'Cítrico';
  WHEN 'Morango/Limão' THEN SELECT 'Cítrico';
  WHEN 'Uva' THEN SELECT 'Neutro';
  WHEN 'Morango' THEN SELECT 'Neutro';
  END CASE;
  SELECT msgErro;
END$$
DELIMITER ;
````

14 ) Execute a SP:
````sql
CALL acha_tipo_sabor_erro('1004327');
````
Teremos o erro tratado.

![](https://cdn3.gnarususercontent.com.br/1223-mysqlproceduresefuncions/04/2.png)

15 ) O Case Condicional utiliza uma estrutura de Case semelhante a usada quando executamos um comando SELECT. Digite e execute:
````sql
USE `sucos_vendas`;
DROP procedure IF EXISTS `acha_status_preco_case`;
DELIMITER $$

USE `sucos_vendas`$$
CREATE PROCEDURE `acha_status_preco_case`(vProduto VARCHAR(50))
BEGIN
   DECLARE vPreco FLOAT;
   DECLARE vMensagem VARCHAR(30);
   SELECT PRECO_DE_LISTA INTO vPreco FROM tabela_de_produtos
   WHERE codigo_do_produto = vProduto;
   CASE
   WHEN vPreco >= 12 THEN SET vMensagem = 'PRODUTO CARO.';
   WHEN vPreco >= 7 AND vPreco < 12 THEN  SET vMensagem = 'PRODUTO EM CONTA.';
   WHEN vPreco < 7 THEN SET vMensagem = 'PRODUTO BARATO';
   END CASE;
   SELECT vMensagem;
END$$
DELIMITER ;
````

16 ) Digite e execute:
````sql
CALL acha_status_preco_case('1004327');
````

17 ) A estrutura de Loop permite repetir um conjunto de comandos até que determinada condição aconteça. Digite e execute:
````sql
CREATE TABLE TAB_LOOPING (ID INT);
````

18 ) Após a criação de uma tabela auxiliar digite e execute
````sql
USE `sucos_vendas`;
DROP procedure IF EXISTS `looping_while`;
DELIMITER $$

USE `sucos_vendas`$$
CREATE PROCEDURE `looping_while`(vNumInicial INT, vNumFinal INT)
BEGIN
   DECLARE vContador INT;
   DELETE FROM TAB_LOOPING;
   SET vContador = vNumInicial;
   WHILE vContador <= vNumFinal
   DO
      INSERT INTO TAB_LOOPING (ID) VALUES (vContador);
      SET vContador = vContador + 1;
   END WHILE;
   SELECT * FROM TAB_LOOPING;
END$$
DELIMITER ;
````

19 ) Vamos executar a SP passando como parâmetro um número inicial e um número final para criação de uma sequência numérica na tabela temporária. Digite e execute:
````sql
call looping_while (1, 1000);
````

![](https://cdn3.gnarususercontent.com.br/1223-mysqlproceduresefuncions/04/3.png)

Teremos uma sequência numérica que vai de 1 a 1000.


## O que aprendemos?

- O control de fluxo IF-THEN-ELSE.
- Uma variação do controle anterior chamado IF-THEN-ELSEIF.
- A estrutura <code>CASE</code>;
- Como tratar erros no <code>CASE</code> quando nem todas as opções são contempladas;
- o <code>CASE</code> condicional, semelhante ao usado nos comandos SQL;
- O uso de Loops para repetir um conjunto de comandos até uma condição ser satisfeita.