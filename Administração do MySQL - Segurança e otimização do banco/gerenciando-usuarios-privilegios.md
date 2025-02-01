1 ) Quando você instalou MySQL, foi criado um usuário root, com privilégios de administrador. Mas, normalmente, este usuário é apagado e substituído por um administrador real.

2 ) No Workbench, clique na aba Administration.

3 ) Clique em Users and Privileges.

4 ) Você terá, do lado esquerdo, a lista de usuários do ambiente, na qual você pode ver o usuário root:

![](https://cdn3.gnarususercontent.com.br/1224-mysql-adminstracao/05/image13.png)

5 ) Clique no botão Add Account.

6 ) Na caixa de diálogo, aba Login, preencha os campos Login Name, Limit to Hosts Matching, Password e confirme a senha:

![](https://cdn3.gnarususercontent.com.br/1224-mysql-adminstracao/05/image6.png)

7 ) Na aba Administrative Roles, escolha o que este usuário pode fazer no MySQL. Selecione DBA, assim tudo será marcado:

![](https://cdn3.gnarususercontent.com.br/1224-mysql-adminstracao/05/image41.png)

8 ) Clique em Apply, assim o usuário será criado.

9 ) Feche a aba da conexão do Workbench:

![](https://cdn3.gnarususercontent.com.br/1224-mysql-adminstracao/05/image4.png)

10 ) Você pode, na tela de conexões, criar uma nova, com o usuário criado nos passos anteriores:

![](https://cdn3.gnarususercontent.com.br/1224-mysql-adminstracao/05/image21.png)

![](https://cdn3.gnarususercontent.com.br/1224-mysql-adminstracao/05/image23.png)

11 ) Clique em Test e salve a conexão.

12 ) Entre no Workbench com o usuário criado nos passos anteriores.

13 ) O usuário poderia ter sido criado via SQL. Crie um outro usuário administrador (admin02). Digite:
````sql
CREATE USER 'admin02'@'localhost' identified BY 'admin02';
GRANT ALL PRIVILEGES ON *.* TO 'admin02'@'localhost' WITH GRANT OPTION;
````

14 ) Se você voltar à tela de Users and Privileges e executar um Refresh, você irá ver este novo usuário, com seus privilégios:

![](https://cdn3.gnarususercontent.com.br/1224-mysql-adminstracao/05/image29.png)

![](https://cdn3.gnarususercontent.com.br/1224-mysql-adminstracao/05/image39.png)

15 ) Para apagar o usuário root original, digite:
````sql
DROP USER 'root'@'localhost';
````

16 ) Se você tentar se conectar com usuário root, não irá mais conseguir, porque este usuário não existe mais.

17 ) O que vai determinar o que um usuário poderá fazer ou não, são seus parâmetros, tanto na caixa de diálogo do Workbench quanto via SQL.

18 ) Crie um usuário user01, usando a aba Administration e a opção Users and Privileges. Este usuário terá os privilégios: CREATE TEMPORARY TABLES, DELETE, EXECUTE, INSERT, LOCK TABLES, SELECT e UPDATE:

![](https://cdn3.gnarususercontent.com.br/1224-mysql-adminstracao/05/image30.png)

19 ) Clique em Apply.

20 ) Crie um outro usuário normal, mas agora via SQL. Digite:
````sql
CREATE USER 'user02'@'localhost' identified BY 'user02';
GRANT SELECT, INSERT, UPDATE, DELETE, CREATE TEMPORARY TABLES,
LOCK TABLES, EXECUTE ON *.* TO 'user02'@'localhost';
````

21 ) Crie um usuário somente leitura, com login read01, através da caixa de diálogo e o read02, via SQL. Para estes usuários, os privilégios serão SELECT e EXECUTE:

![](https://cdn3.gnarususercontent.com.br/1224-mysql-adminstracao/05/image12.png)

:

````sql
CREATE USER 'read02'@'localhost' identified BY 'read02';
GRANT SELECT, EXECUTE ON *.* TO 'read02'@'localhost';
````

22 ) Vá para mais dois usuários, com os logins back01 e back02. Aqui, estes usuários somente podem criar backups:
````sql
CREATE USER 'back02'@'localhost' identified BY 'back02';
GRANT SELECT, RELOAD, LOCK TABLES, REPLICATION CLIENT ON *.* TO 'back02'@'localhost';
````

23 ) Todos os usuários criados até aqui só podem acessar o banco de dados através da máquina localhost. Quando você cria um usuário,se você manter % ou _** no campo **Limit to Hosts Matching, você irá determinar que outros IPs possam ser utilizados para acessar o banco. Estes caracteres funcionam como curinga:
````sql
CREATE USER 'admingeneric02'@'%' identified BY 'admingeneric02';
GRANT ALL PRIVILEGES ON *.* TO 'admingeneric02'@'%' WITH GRANT OPTION;
````

24 ) Você também pode limitar o acesso às bases e tabelas. Crie o usuário user03, mas, em vez de adicionar privilégios globais na aba Administrative Roles, acesse a aba Schema Privileges e adicione o esquema a ser acessado:

![](https://cdn3.gnarususercontent.com.br/1224-mysql-adminstracao/05/image24.png)

25 ) O mesmo comando pode ser digitado por SQL. Inclusive, abaixo, você pode criar o usuário simplesmente e depois adicionar, em outro comando, os privilégios:
````sql
CREATE USER 'user04'@'%' IDENTIFIED BY 'user04';
GRANT SELECT, INSERT, UPDATE, DELETE, CREATE TEMPORARY TABLES, LOCK TABLES, EXECUTE
ON sucos_vendas.* TO 'user04'@'%';
````

O usuário criado acima somente pode ver a base sucos_vendas.

26 ) Crie uma conexão para o usuário user04:

![](https://cdn3.gnarususercontent.com.br/1224-mysql-adminstracao/05/image47.png)

27 ) Se conecte e note que somente a base sucos_vendas é disponibilizada para acesso:

![](https://cdn3.gnarususercontent.com.br/1224-mysql-adminstracao/05/image10.png)

28 ) Você pode limitar o acesso às tabelas, dando permissões do que pode ser feito nelas:
````sql
CREATE USER 'user05'@'%' IDENTIFIED BY 'user05';
GRANT SELECT, INSERT, UPDATE, DELETE
ON sucos_vendas.tabela_de_clientes TO 'user05'@'%';
GRANT SELECT
ON sucos_vendas.tabela_de_produtos TO 'user05'@'%';
````

Estes comandos estão dando privilégios para inclusão, alteração, exclusão e consulta para o user05 na tabela_de_clientes, mas somente leitura na tabela_de_produtos.

29 ) Crie uma conexão para o usuário user05 e entre no Workbench.

30 ) Execute o comando:
````sql
INSERT INTO `sucos_vendas`.`tabela_de_produtos` (
    `CODIGO_DO_PRODUTO`,
    `NOME_DO_PRODUTO`,
    `EMBALAGEM`,
    `TAMANHO`,
    `SABOR`,
    `PRECO_DE_LISTA`
) VALUES (
    '999999',
    'BNBNBNBNB',
    'HJHJHJHJ',
    'FGFGFGF',
    'GHGHGH',
    10
);
````

Você verá erros ao tentar incluir um registro na tabela:

![](https://cdn3.gnarususercontent.com.br/1224-mysql-adminstracao/05/image18.png)

31 ) Existe um comando para verificar os usuários existentes:
````sql
SELECT * FROM mysql.user;
````

32 ) Há também um comando que mostra os acessos de um usuário, por exemplo:
````sql
SHOW GRANTS FOR 'user02'@'localhost';
````

33 ) O comando REVOKE ALL retira os privilégios de acesso dos usuários:
````sql
REVOKE ALL PRIVILEGES, GRANT OPTION FROM 'user02'@'localhost';
````

## O que aprendemos?

- A criar usuários administradores e a remover o usuário root
- Como criar um usuário com privilégios para acesso normal (sem ser administrador)
- Como criar um usuário que só pode ler os dados
- Como criar um usuário que somente executa backups
- A fazer a criação dos usuários pela caixa de diálogo do Workbench e via SQL
- Como limitar o acesso do usuário pelo IP
- A limitar o acesso por banco e por tabela
- Como revogar os privilégios