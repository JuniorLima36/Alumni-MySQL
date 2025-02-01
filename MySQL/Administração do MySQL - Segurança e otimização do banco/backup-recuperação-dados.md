1 ) Os componentes de uma base ficam armazenados em um banco de dados. Você pode criar um banco de dados novo com o seguinte comando (no caso, será criado com nome o library):
````sql
CREATE DATABASE LIBRARY;
````

2 ) A base de dados pode ser criada, também, pelo assistente do Workbench. Para isso, clique com o botão direito do mouse sobre a área vazia da lista de componentes, à esquerda do Workbench, e escolha a opção Create Schema:

![](https://cdn3.gnarususercontent.com.br/1224-mysql-adminstracao/03/image27.png)

3 ) Crie uma nova base chamada library2, mas utilizando o assistente. Para isso, digite o seu nome na opção Name:

![](https://cdn3.gnarususercontent.com.br/1224-mysql-adminstracao/03/image14.png)

4 ) Quando você criou estas bases, o MySQL escreveu no seu disco rígido os arquivos físicos que as representam. Para saber em que diretório estes arquivos foram criados, você pode ver o valor da variável de ambiente Variable_Name:
````sql
SHOW VARIABLES WHERE Variable_Name LIKE '%dir';
````

![](https://cdn3.gnarususercontent.com.br/1224-mysql-adminstracao/03/image2.png)

Você verá todas as variáveis que possuem <code>dir</code> no nome. A variável que com o diretório dos arquivos é a <code>datadir</code>.

5 ) Indo no diretório mencionado acima, você verá:

![](https://cdn3.gnarususercontent.com.br/1224-mysql-adminstracao/03/image37.png)

Há um subdiretório para cada base.

6 ) A inicialização desta variável <code>datadir</code> está no my.ini:

![](https://cdn3.gnarususercontent.com.br/1224-mysql-adminstracao/03/image46.png)

7 ) Para apagar uma base, basta executar o comando:
````sql
DROP DATABASE library2;
````

8 ) Ou pelo assistente do Workbench. Para isso, clique com o botão direito do mouse sobre a base de dados a ser excluída e escolha a opção Drop Schema:

![](https://cdn3.gnarususercontent.com.br/1224-mysql-adminstracao/03/image28.png)

9 ) Crie um diretório chamado mysqladmin, na raiz do drive C:\.

10 ) Na linha de comando do Windows, digite os seguintes comandos:
````
cd\
cd "Program Files"
cd "MySQL"
cd "MySQL 8.0"
cd Bin
````

11 ) Para realizar um backup da base sucos_vendas, digite:
````
mysqldump -uroot -p --databases sucos_vendas > c:\mysqladmin\sucos_vendas_full.sql
````

A senha do usuário root será necessária para a execução do comando.

12 ) Dentro do arquivo C:\mysqladmin\sucos_vendas_full.sql, você terá os comandos para recuperar a base sucos_vendas.

13 ) Para realizar um backup somente da tabela notas_fiscais, da base sucos_vendas, execute o seguinte comando:
````
mysqldump -uroot -p --databases sucos_vendas --tables notas_fiscais > c:\mysqladmin\sucos_vendas_tab_notas_fiscais.sql
````

14 ) Para realizar um backup de todas as tabelas da base sucos_vendas, exceto a tabela notas_vendas, execute o seguinte comando:
````
mysqldump -uroot -p --databases sucos_vendas --ignore-table sucos_vendas.notas_fiscais > c:\mysqladmin\sucos_vendas_ig_tab_notas_fiscias.sql
````

15 ) Para realizar um backup somente dos comandos de INSERT de todas as tabelas da base sucos_vendas, execute o seguinte comando:
````
mysqldump -uroot -p --databases sucos_vendas --no-create-db --no-create-info --complete-insert > c:\mysqladmin\sucos_vendas_somente_inserts.sql
````

16 ) Na página https://dev.mysql.com/doc/refman/8.0/en/mysqldump.html, você pode ver todas as propriedades suportadas pelo mysqldump.

17 ) Você pode realizar um backup através do Workbench. Para isso, abra-o.

18 ) Antes do processo, você precisa "desligar" o banco, para fazer o processo de criação do backup. Para isso, dê um duplo clique sobre o banco sucos_vendas, digite e execute:
````
LOCK INSTANCE FOR BACKUP;
````

19 ) Clique na aba Administration:

![](https://cdn3.gnarususercontent.com.br/1224-mysql-adminstracao/03/image31.png)

20 ) E depois em Data Export.

21 ) Selecione a base sucos_vendas.

22 ) Marque a opção Export to Self-Contained File.

23 ) Ao lado, inclua o nome do arquivo a ser salvo (C:\mysqladmin\sucos_vendas_full_work.sql).

24 ) Clique em Start Export.

25 ) Veja que, no diretório de saída (C:\mysqladmin\), um arquivo novo foi criado, com o mesmo conteúdo do arquivo criado pelo mysqldump.

26 ) Você pode exportar cada componente do banco (no caso, as tabelas) em um arquivo, separadamente. Para isso, novamente clique em Data Export.

27 ) Selecione a base sucos_vendas.

28 ) Escolha a opção Export to Dump Project Folder.

29 ) Ao lado, inclua o nome do diretório onde os arquivos serão salvos (C:\mysqladmin\bkp_sucos_vendas).

30 ) Clique em Start Export.

31 ) Veja que, no diretório de saída (C:\mysqladmin\), haverá uma pasta e dentro dela haverá diversos arquivos representando as diferentes tabelas.

32 ) Outra forma de fazer o backup é copiando toda a estrutura do banco. Mas antes, no diretório C:\mysqladmin\bkp_sucos_vendas\, crie um diretório chamado Dados.

33 ) Vá em C:\ProgramData\MySQL\MySQL Server 8.0 e copie o arquivo my.ini para o diretório C:\mysqladmin\bkp_sucos_vendas\Dados\.

34 ) Depois, copie o diretório (e também o seu conteúdo) C:\ProgramData\MySQL\MySQL Server 8.0\Data para dentro de C:\mysqladmin\bkp_sucos_vendas\Dados\.

35 ) O que você tem salvo em C:\mysqladmin\bkp_sucos_vendas\Dados é todo o ambiente de dados, preservado em um outro disco.

36 ) Após o fim do processo, libere a instância do banco de dados, digitando o seguinte comando:
````sql
UNLOCK INSTANCE
````

37 ) Para recuperar o backup, primeiramente, no Workbench, apague a base sucos_vendas, digitando:
````sql
drop database sucos_vendas;
````

38 ) O backup desta base está salvo em C:\mysqladmin\sucos_vendas_full.sql. Então, abra uma janela de linha de comando do Windows e digite:
````
cd\
cd "Program Files"
cd "MySQL"
cd "MySQL 8.0"
cd Bin
````

39 ) E execute:
````
mysql -uroot -p < c:\mysqladmin\sucos_vendas_full.sql
````

40 ) A base será criada e seus dados incluídos novamente.

41 ) Você também pode recuperar a base através do arquivo físico. Para isso, no Workbench, apague novamente a base:
````sql
drop database sucos_vendas;
````

42 ) Saia do Workbench e pare o serviço do MySQL.

43 ) Vá em C:\mysqladmin\bkp_sucos_vendas\Dados\ e copie o arquivo my.ini para dentro de C:\ProgramData\MySQL\MySQL Server 8.0\.

44 ) Copie o diretório (e também o seu conteúdo) C:\mysqladmin\bkp_sucos_vendas\Dados\Data para C:\ProgramData\MySQL\MySQL Server 8.0\Data.

45 ) Suba o serviço do MySQL.

46 ) Entre no Workbench e veja que a base sucos_vendas voltou a estar disponível.

## O que aprendemos?

- A criar e apagar bases de dados
- Como realizar o backup através do mysqldump
- A fazer o backup copiando toda a estrutura de dados para outro diretório
- A recuperar o backup usando o a linha de comando do MySQL ou copiando de volta a estrutura de arquivos