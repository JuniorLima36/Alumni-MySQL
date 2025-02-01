# Mudando o acesso

Com o mesmo usuário do exercício anterior, agora queremos que ele passe a ter apenas privilégio de exclusão na `TABELA1`.

Sabendo que os outros privilégios permanecem iguais, quais serão os comandos necessários para isso?

Os comandos podem ser os seguintes:
````sql
REVOKE ALL PRIVILEGES, GRANT OPTION FROM 'user'@'%';

GRANT SELECT, INSERT, UPDATE, DELETE, CREATE TEMPORARY TABLES, LOCK TABLES, EXECUTE 
ON BANCODB .TABELA3 TO 'user'@'%';

GRANT SELECT, DELETE, EXECUTE 
ON BANCODB .TABELA1 TO 'user'@'%';

GRANT SELECT, EXECUTE 
ON BANCODB .TABELA2 TO 'user'@'%';
````