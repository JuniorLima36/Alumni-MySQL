#  Acesso a uma base

Tenho um banco chamado `BANCODB`, com as seguintes tabelas:

- `TABELA1`
- `TABELA2`
- `TABELA3`

Queremos dar acesso apenas à leitura das tabelas `TABELA1` e `TABELA2`, e acesso completo à `TABELA3`. Sabendo que já temos um usuário `user@%` criado, como devem ser os comandos SQL para configurar este acesso?

Os comandos SQL devem ser os seguintes:
````sql
GRANT ALL PRIVILEGES
ON BANCODB.TABELA3 TO 'user'@'%';
````

````sql
GRANT SELECT
ON BANCODB.TABELA1 TO 'user'@'%';
````

````sql
GRANT SELECT
ON BANCODB.TABELA2 TO 'user'@'%';
````