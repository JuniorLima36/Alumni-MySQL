1 ) Quando o resultado de um SELECT possui mais de uma linha não podemos atribuí-lo a uma variável usando o SELECT INTO. Para isso temos que usar o Cursor para receber valores vindos de uma tabela, com uma ou mais colunas.

2 ) Vamos criar uma SP que utilize Cursor. Digite e execute:
````sql
USE sucos_vendas;

DROP procedure IF EXISTS cursor_primeiro_contato;

DELIMITER $$

USE sucos_vendas$$

CREATE PROCEDURE `cursor_primeiro_contato` ()

BEGIN
  DECLARE vNome VARCHAR(50);
  DECLARE c CURSOR FOR SELECT NOME FROM tabela_de_clientes limit 4;
  OPEN c;
  FETCH c INTO vNome;
  SELECT vNome;
  FETCH c INTO vNome;
  SELECT vNome;
  FETCH c INTO vNome;
  SELECT vNome;
  FETCH c INTO vNome;
  SELECT vNome;
  CLOSE c;
END$$
DELIMITER ;
````

3 ) Note que cada linha da seleção é atribuída a variável vNome, uma de cada vez. Execute:
````sql
call cursor_primeiro_contato;
````
![](https://cdn3.gnarususercontent.com.br/1223-mysqlproceduresefuncions/05/1.png)

![](https://cdn3.gnarususercontent.com.br/1223-mysqlproceduresefuncions/05/2.png)

![](https://cdn3.gnarususercontent.com.br/1223-mysqlproceduresefuncions/05/3.png)

![](https://cdn3.gnarususercontent.com.br/1223-mysqlproceduresefuncions/05/4.png)

4 ) Na SP acima executamos um Cursos controlado onde sabíamos quantos elementos o mesmo tinha. Mas, normalmente, não sabemos esta informação. Por isso usamos sempre o Cursos combinados com um Looping. Digite e execute a criação da SP abaixo:
````sql
USE sucos_vendas;

DROP procedure IF EXISTS cursor_looping;


DELIMITER $$

USE `sucos_vendas`$$

CREATE PROCEDURE `cursor_looping` ()

BEGIN
  DECLARE fim_do_cursor INT DEFAULT 0;

  DECLARE vNome VARCHAR(50);

  DECLARE c CURSOR FOR SELECT NOME FROM tabela_de_clientes;

  DECLARE CONTINUE HANDLER FOR NOT FOUND SET fim_do_cursor = 1;

  OPEN c;

  WHILE fim_do_cursor = 0
  DO
    FETCH c INTO vNome;
    IF fim_do_cursor = 0 THEN
      SELECT vNome;
    END IF;
  END WHILE;
  CLOSE c;
END$$

DELIMITER ;
````

5 ) Executando a SP:
````sql
call cursor_looping;
````

Teremos diversos resultados em diferentes consultas.

![](https://cdn3.gnarususercontent.com.br/1223-mysqlproceduresefuncions/05/5.png)

6 ) O Cursor pode suportar mais de uma coluna. Crie a SP abaixo:
````sql
USE sucos_vendas;

DROP procedure IF EXISTS looping_cursor_multiplas_colunas;


DELIMITER $$

USE sucos_vendas$$

CREATE PROCEDURE `looping_cursor_multiplas_colunas` ()

BEGIN
  DECLARE fim_do_cursor INT DEFAULT 0;

  DECLARE vCidade, vEstado, vCep VARCHAR(50);

  DECLARE vNome, vEndereco VARCHAR(150);

  DECLARE c CURSOR FOR

  SELECT nome, endereco_1, cidade, estado, cep FROM tabela_de_clientes;

  DECLARE CONTINUE HANDLER FOR NOT FOUND SET fim_do_cursor = 1;

  OPEN c;

  WHILE fim_do_cursor = 0

  DO
    FETCH c INTO vNome, vEndereco, vCidade, vEstado, vCep;

    IF fim_do_cursor = 0 THEN
      SELECT CONCAT(vNome, ' Endereço: ',

      vEndereco, ', ', vCidade , ' - ', vEstado, ' CEP: ' , vCep);
    END IF;
  END WHILE;
  CLOSE c;
END$$

DELIMITER ;
````

7 ) Execute-a:
````sql
call looping_cursor_multiplas_colunas;
````

Esta SP também retorna múltiplas consultas.

![](https://cdn3.gnarususercontent.com.br/1223-mysqlproceduresefuncions/05/6.png)

8 ) Também podemos criar uma função. A diferença de uma função e uma SP é que a função retorna um valor e pode ser usada dentro de um comando <code>SELECT</code>, <code>INSERT</code>, <code>UPDATE</code> e condições de <code>DELETE</code>.

9 ) Para criar uma função vá com o botão da direita do mouse sobre Function e selecione Create Function:

![](https://cdn3.gnarususercontent.com.br/1223-mysqlproceduresefuncions/05/7.png)

10 ) Acrescente o código abaixo:
````sql
CREATE FUNCTION `f_acha_tipo_sabor`(vSabor VARCHAR(50)) RETURNS varchar(20) CHARSET utf8mb4

BEGIN
  DECLARE vRetorno VARCHAR(20) default "";

  CASE vSabor

  WHEN 'Lima/Limão' THEN SET vRetorno = 'Cítrico';

  WHEN 'Laranja' THEN SET vRetorno = 'Cítrico';

  WHEN 'Morango/Limão' THEN SET vRetorno = 'Cítrico';

  WHEN 'Uva' THEN SET vRetorno = 'Neutro';

  WHEN 'Morango' THEN SET vRetorno = 'Neutro';

  ELSE SET vRetorno = 'Ácidos';

  END CASE;

  RETURN vRetorno;
END
````

11 ) Clique em Apply. Teremos o código que poderá ser eecutado diretamente do script MYSQL.
````sql
USE sucos_vendas;

DROP function IF EXISTS f_acha_tipo_sabor;


DELIMITER $$

USE `sucos_vendas`$$

CREATE FUNCTION `f_acha_tipo_sabor`(vSabor VARCHAR(50)) RETURNS varchar(20) CHARSET utf8mb4

BEGIN
  DECLARE vRetorno VARCHAR(20) default "";

  CASE vSabor

  WHEN 'Lima/Limão' THEN SET vRetorno = 'Cítrico';

  WHEN 'Laranja' THEN SET vRetorno = 'Cítrico';

  WHEN 'Morango/Limão' THEN SET vRetorno = 'Cítrico';

  WHEN 'Uva' THEN SET vRetorno = 'Neutro';

  WHEN 'Morango' THEN SET vRetorno = 'Neutro';

  ELSE SET vRetorno = 'Ácidos';

  END CASE;

  RETURN vRetorno;
END$$


DELIMITER ;
````

12 ) Clique em Apply. Teremos o código que poderá ser executado diretamente do script MYSQL.

Observação: Se você verificar um erro como mostrado abaixo:

![](https://cdn3.gnarususercontent.com.br/1223-mysqlproceduresefuncions/05/8.png)

É porque o MYSQL não permite a construção de Funções. Para permitir, execute o comando:
````sql
SET GLOBAL log_bin_trust_function_creators = 1;
````

E crie a função novamente.

13 ) Execute a função:
````sql
SELECT f_acha_tipo_sabor ("Laranja");
````
![](https://cdn3.gnarususercontent.com.br/1223-mysqlproceduresefuncions/05/9.png)

14 ) Podemos usar a função num comando SELECT. Digite e execute:
````sql
SELECT NOME_DO_PRODUTO, SABOR, f_acha_tipo_sabor (SABOR) as TIPO

 FROM tabela_de_produtos;
````
![](https://cdn3.gnarususercontent.com.br/1223-mysqlproceduresefuncions/05/10.png)


## O que aprendemos?

- Conhecemos a estrutura de Cursor onde podemos atribuir valores resultados de um SELECT com múltiplas linhas.
- Vimos que podemos atribuir ao Cursor mais de uma coluna.
- Aprendemos como usar o Cursor em conjunto com um Looping.
- Foi mostrado como criamos e usamos uma função.