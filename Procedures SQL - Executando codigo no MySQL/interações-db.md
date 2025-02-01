1 ) Abra um novo script MYSQL.

2 ) Digite e execute:
````sql
USE `sucos_vendas`;
DROP procedure IF EXISTS `manipulacao_dados`;
DELIMITER $$

USE `sucos_vendas`$$
CREATE PROCEDURE `manipulacao_dados` ()
BEGIN
INSERT INTO tabela_de_produtos (CODIGO_DO_PRODUTO,NOME_DO_PRODUTO,SABOR,TAMANHO,EMBALAGEM,PRECO_DE_LISTA)
     VALUES ('2001001','Sabor da Serra 700 ml - Manga','Manga','700 ml','Garrafa',7.50),
         ('2001000','Sabor da Serra  700 ml - Melão','Melão','700 ml','Garrafa',7.50),
         ('2001002','Sabor da Serra  700 ml - Graviola','Graviola','700 ml','Garrafa',7.50),
         ('2001003','Sabor da Serra  700 ml - Tangerina','Tangerina','700 ml','Garrafa',7.50),
         ('2001004','Sabor da Serra  700 ml - Abacate','Abacate','700 ml','Garrafa',7.50),
         ('2001005','Sabor da Serra  700 ml - Açai','Açai','700 ml','Garrafa',7.50),
         ('2001006','Sabor da Serra  1 Litro - Manga','Manga','1 Litro','Garrafa',7.50),
         ('2001007','Sabor da Serra  1 Litro - Melão','Melão','1 Litro','Garrafa',7.50),
         ('2001008','Sabor da Serra  1 Litro - Graviola','Graviola','1 Litro','Garrafa',7.50),
         ('2001009','Sabor da Serra  1 Litro - Tangerina','Tangerina','1 Litro','Garrafa',7.50),
         ('2001010','Sabor da Serra  1 Litro - Abacate','Abacate','1 Litro','Garrafa',7.50),
         ('2001011','Sabor da Serra  1 Litro - Açai','Açai','1 Litro','Garrafa',7.50);

         SELECT * FROM tabela_de_produtos WHERE NOME_DO_PRODUTO LIKE 'Sabor da Serra%';
         UPDATE tabela_de_produtos SET PRECO_DE_LISTA = 8 WHERE NOME_DO_PRODUTO LIKE 'Sabor da Serra%';

         SELECT * FROM tabela_de_produtos WHERE NOME_DO_PRODUTO LIKE 'Sabor da Serra%';
         DELETE FROM tabela_de_produtos WHERE NOME_DO_PRODUTO LIKE 'Sabor da Serra%';

         SELECT * FROM tabela_de_produtos WHERE NOME_DO_PRODUTO LIKE 'Sabor da Serra%';
END$$
DELIMITER ;
````

3 ) Execute:
````sql
Call manipulacao_dados;
````

4 ) A SP acima manipula uma série de comandos no banco de dados MYSQL.

Observação: Se você observar o seguinte erro:

![](https://cdn3.gnarususercontent.com.br/1223-mysqlproceduresefuncions/03/0.png)

É porque você deve efetuar uma modificação na configuração do seu MYSQL.

Vá, no menu, em Edit / Preference e na seção SQL EDITOR vá até o final do formulário e desmarque a opção Safe Updates (Reject UPDATEs and DELETEs with no restrictions).

![](https://cdn3.gnarususercontent.com.br/1223-mysqlproceduresefuncions/03/1.png)

5 ) Podemos também usar a SP para inserir dados na tabela usando variáveis. Digite e execute:
````sql
USE `sucos_vendas`;
DROP procedure IF EXISTS `inclui_novo_produto`;
DELIMITER $$

USE `sucos_vendas`$$
CREATE PROCEDURE `inclui_novo_produto` ()
BEGIN
DECLARE vCodigo varchar(50) DEFAULT '3000001';
DECLARE vNome varchar(50) DEFAULT 'Sabor do Mar 700 ml - Manga';
DECLARE vSabor varchar(50) DEFAULT 'Manga';
DECLARE vTamanho varchar(50) DEFAULT '700 ml';
DECLARE vEmbalagem varchar(50) DEFAULT 'Garrafa';
DECLARE vPreco DECIMAL(10,2) DEFAULT 9.25;
INSERT INTO tabela_de_produtos
(CODIGO_DO_PRODUTO,NOME_DO_PRODUTO,SABOR,TAMANHO,EMBALAGEM,PRECO_DE_LISTA)
     VALUES (vCodigo,
     vNome,
     vSabor,
     vTamanho,
     vEmbalagem,
     vPreco);
END$$
DELIMITER ;
````

6 ) Execute:
````sql
Call inclui_novo_produto;
````

7 ) Veja que usamos referência direta as variáveis no comando INSERT, dentro da SP.

8 ) Podemos usar parâmetros para passar para a SP os dados que serão usados no comando de INSERT. Para isso digite e execute:
````sql
USE `sucos_vendas`;
DROP procedure IF EXISTS `inclui_novo_produto_parametro`;
DELIMITER $$

USE `sucos_vendas`$$
CREATE PROCEDURE `inclui_novo_produto_parametro`(vCodigo varchar(50),
vNome varchar(50), vSabor varchar(50), vTamanho varchar(50),
vEmbalagem varchar(50), vPreco DECIMAL(10,2))
BEGIN
INSERT INTO tabela_de_produtos
(CODIGO_DO_PRODUTO,NOME_DO_PRODUTO,SABOR,TAMANHO,EMBALAGEM,PRECO_DE_LISTA)
     VALUES (vCodigo,
     vNome,
     vSabor,
     vTamanho,
     vEmbalagem,
     vPreco);
END$$
DELIMITER ;
````

9 ) Execute a SP:
````sql
Call inclui_novo_produto_parametro('4000001', 'Sabor do Pantanal 1 Litro - Melancia',
'Melancia', '1 Litro', 'PET', 4.76);
````

10 ) Veja que o comando acima passa os dados que serão incluídos dentro da tabela através dos parâmetros.

11 ) Repita a execução do comando novamente:
````sql
Call inclui_novo_produto_parametro('4000004', 'Sabor do Pantanal 1 Litro - Melancia',
'Melancia', '1 Litro', 'PET', 4.76);
````

12 ) Note que houve um erro de chave primária porque o produto 4000004 já existe na tabela:

![](https://cdn3.gnarususercontent.com.br/1223-mysqlproceduresefuncions/03/2.png)

13 ) Podemos tratar este erro para que ele apresente uma mensagem amigável quando ocorrer. Execute e digite:
````sql
USE `sucos_vendas`;
DROP procedure IF EXISTS `inclui_novo_produto_parametro_2`;
DELIMITER $$

USE `sucos_vendas`$$
CREATE PROCEDURE `inclui_novo_produto_parametro_2`(vCodigo varchar(50),
vNome varchar(50), vSabor varchar(50), vTamanho varchar(50),
vEmbalagem varchar(50), vPreco DECIMAL(10,2))
BEGIN
DECLARE mensagem VARCHAR(40);
DECLARE EXIT HANDLER FOR 1062
BEGIN
   SET mensagem = 'Problema de Chave Primária !!!';
   SELECT mensagem;
END;

INSERT INTO tabela_de_produtos
(CODIGO_DO_PRODUTO,NOME_DO_PRODUTO,SABOR,TAMANHO,EMBALAGEM,PRECO_DE_LISTA)
     VALUES (vCodigo,
     vNome,
     vSabor,
     vTamanho,
     vEmbalagem,
     vPreco);
SET mensagem = 'Produto incluido com sucesso !!!';
SELECT mensagem;
END$$
DELIMITER ;
````

14 ) Execute e digite:
````sql
Call inclui_novo_produto_parametro_2('4000004', 'Sabor do Pantanal 1 Litro - Melancia',
'Melancia', '1 Litro', 'PET', 4.76);
````
![](https://cdn3.gnarususercontent.com.br/1223-mysqlproceduresefuncions/03/3.png)

15 ) Repita o comando. Teremos:

![](https://cdn3.gnarususercontent.com.br/1223-mysqlproceduresefuncions/03/4.png)

16 ) Vimos que o comando <code>SET</code> é usado para atribuir valores as variáveis. Más podemos atribuir valores a ela usando comandos <code>SELECT</code> através do <code>SELECT INFO</code>. Execute e digite:
````sql
USE `sucos_vendas`;
DROP procedure IF EXISTS `acha_sabor_produto`;
DELIMITER $$

USE `sucos_vendas`$$
CREATE PROCEDURE `acha_sabor_produto`(vProduto VARCHAR(50))
BEGIN
   DECLARE vSabor VARCHAR(50);
   SELECT SABOR INTO vSabor FROM tabela_de_produtos WHERE codigo_do_produto = vProduto;
   SELECT vSabor;
END$$
DELIMITER ;
````

17 ) Execute:
````sql
Call acha_sabor_produto('1013793');
````

18 ) Teremos como resposta o sabor do produto passado como parâmetro.

![](https://cdn3.gnarususercontent.com.br/1223-mysqlproceduresefuncions/03/5.png)


## O que aprendemos?

- Como manipular comandos SQL dentro da SP;
- Como passar parâmetros para uma SP;
- Como tratamos erros;
- A atribuição de variáveis através de um comando SELECT.