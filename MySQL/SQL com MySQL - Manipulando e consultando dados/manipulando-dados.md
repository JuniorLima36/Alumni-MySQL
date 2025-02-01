1 ) Acesse o Workbench.

2 ) No canto esquerdo temos uma estrutura em forma de árvore onde vemos o banco de dados, ou esquemas.

![](https://cdn3.gnarususercontent.com.br/1220-mysqlintroducaoaosql/02/1.png)

3 ) Abrindo um dos banco de dados podemos ver alguns dos seus componentes.

![](https://cdn3.gnarususercontent.com.br/1220-mysqlintroducaoaosql/02/2.png)

4 ) No menu do Workbench, temos o botão "+ SQL" onde uma área de edição será criada para que possamos incluir os comandos de SQL para gerenciar nossos bancos de dados.

5 ) Efetue um duplo clique no banco de dados World. Depois, execute o seguinte comando na área de edição:
````sql
SELECT * FROM CITY;
````

6 ) Clique em:

![](https://cdn3.gnarususercontent.com.br/1220-mysqlintroducaoaosql/02/3.png)

E a consulta é executada.

![](https://cdn3.gnarususercontent.com.br/1220-mysqlintroducaoaosql/02/4.png)

7 ) Digite, abaixo, um novo comando:
````sql
SELECT * FROM COUNTRY;
````

8 ) Clique em:

![](https://cdn3.gnarususercontent.com.br/1220-mysqlintroducaoaosql/02/3.png)

E as duas consultas serão executadas.

9 ) Se você selecionar uma área com alguns comandos e clicar em:

![](https://cdn3.gnarususercontent.com.br/1220-mysqlintroducaoaosql/02/3.png)

Somente aquele comando selecionado é que será executado.

10 ) Caso o comando esteja errado, abaixo você verá o resultado de cada execução.

11 ) Vamos criar um banco de dados. Para isso, crie um novo script no Workbench e digite:
````sql
CREATE DATABASE SUCOS;
````

12 ) Execute o comando. Note que o banco de dados é criado.

![](https://cdn3.gnarususercontent.com.br/1220-mysqlintroducaoaosql/02/7.png)

13 ) Podemos criar o banco de dados através de um assistente. Para isso, clique com o botão da direita do mouse sobre uma área qualquer onde fica a lista dos bancos de dados.

![](https://cdn3.gnarususercontent.com.br/1220-mysqlintroducaoaosql/02/8.png)

E selecione Create Schema.

14 ) Inclua o nome do banco de dados (ex: Sucos2).

15 ) Clique em Apply.

16 ) O comando SQL é exibido. Clique novamente em Apply e o novo banco é criado.

17 ) Podemos apagar o banco de dados. Execute o comando:
````sql
DROP DATABASE SUCOS;
````

18 ) Note que o banco não mais aparece na lista de bancos de dados.

![](https://cdn3.gnarususercontent.com.br/1220-mysqlintroducaoaosql/02/9.png)

19 ) Se escolhermos a base sucos2, com o botão da direita do mouse, podemos também apagar o banco clicando em Drop Schema.

![](https://cdn3.gnarususercontent.com.br/1220-mysqlintroducaoaosql/02/10.png)

20 ) É possível acessar o MySQL por linha de comando. Vá para o subdiretório c:\Program Files\MySQL\MySQL Server 8.0\bin

21 ) Digite o comando:
````sql
mysql -h localhost -u root -p
````

Tecle enter e depois inclua a senha.

22 ) Digite o comando:
````sql
CREATE DATABASE sucos;
````

Se você for conferir no Workbench veja que o banco de dados sucos foi acrescido à lista de bancos disponíveis.

23 ) Para executar uma consulta no banco exemplo world digite:
````sql
USE world; <ENTER>
SELECT * FROM city; <ENTER>
````

Onde <code>ENTER</code> significa teclar a tecla Enter.

24 ) Verá que a lista de cidades são listadas.

25 ) Para sair digite:
````sql
exit
````

## O que aprendemos?

- A acessar e navegar pelo Workbench;
- A criar um banco de dados por linha de SQL ou pelo assistente;
- Como apagar um banco de dados por linha de SQL ou pelo assistente;
- Como acessar uma tabela por linha de comando ou pelo assistente;