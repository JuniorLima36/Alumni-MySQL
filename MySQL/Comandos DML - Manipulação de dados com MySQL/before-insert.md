O `BEFORE INSERT` é responsável por disparar a `TRIGGER` antes que um evento de inserção ocorra na tabela. Sua sintaxe é demonstrada abaixo:
````sql
DELIMITER//
CREATE TRIGGER nome_do_trigger
  BEFORE INSERT
  ON nome_da_tabela FOR EACH ROW
BEGIN
-- codigo_a_ser_executado
END//
````

Seguindo o exemplo da aula, é demonstrado um SQL que calcula a idade em anos baseado na data atual:
````sql
SELECT CPF, IDADE, DATA_NASCIMENTO, timestampdiff(YEAR, DATA_NASCIMENTO, NOW()) AS ANOS FROM
CLIENTES
````

Caso seja necessário calcular a idade de um(a) novo(a) cliente, que será inserido(a) na tabela CLIENTES, podemos utilizar o `BEFORE INSERT`. Antes do registro ir para a tabela, o cálculo da idade será realizado como é demonstrado abaixo:

````sql
DELIMITER//

CREATE TRIGGER TG_CLIENTES_IDADE_INSERT BEFORE INSERT ON CLIENTES

FOR EACH ROW

BEGIN

SET NEW.IDADE = timestampdiff(YEAR, NEW.DATA_NASCIMENTO, NOW());

END//
````

Vale ressaltar que o código acima é válido para novos(as) clientes. Em caso de registros já existentes no banco de dados, a idade não se altera. Observe que não utilizamos o `UPDATE`, mas sim a cláusula `SET` diretamente. Uma vez que não podemos utilizar um comando `UPDATE` em uma trigger, na qual a tabela a ser atualizada é a mesma que sofrerá a ação para acionar a trigger (neste caso, a tabela "clientes"), utilizamos o comando `SET` atualizando apenas os novos registros a serem inseridos na tabela. O operador `NEW` representa o novo registro que será incluído.
Dis