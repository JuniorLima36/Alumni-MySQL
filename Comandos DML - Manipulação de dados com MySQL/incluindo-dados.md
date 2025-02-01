1 ) Vamos criar um novo script SQL no Workbench.

2 ) Iremos inserir um novo produto. Digite:
````sql
USE vendas_sucos;


INSERT INTO PRODUTOS (CODIGO, DESCRITOR, SABOR, TAMANHO, EMBALAGEM, PRECO_LISTA)

VALUES ('1040107', 'Light - 350 ml - Melância', 'Melância', '350 ml', 'Lata', 4.56);
````

3 ) Vamos conferir se o produto foi realmente incluido na tabela. Digite e execute:
````sql
SELECT * FROM PRODUTOS;
````
![](https://cdn3.gnarususercontent.com.br/1222-mysqlmanipulacaodedados/03/1.png)

4 ) No script podemos incluir mais de um comando. Digite e execute:
````sql
INSERT INTO PRODUTOS (CODIGO, DESCRITOR, SABOR, TAMANHO, EMBALAGEM, PRECO_LISTA)

VALUES ('1040108', 'Light - 350 ml - Graviola', 'Graviola', '350 ml', 'Lata', 4.00);

INSERT INTO PRODUTOS

VALUES ('1040109', 'Light - 350 ml - Açai', 'Açai', '350 ml', 'Lata', 5.60);
````

5 ) Também podemos incluir, num mesmo comando, a inclusão de mais de um registro. Digite e execute:
````sql
INSERT INTO PRODUTOS

VALUES ('1040110', 'Light - 350 ml - Jaca', 'Jaca', '350 ml', 'Lata', 6.00),

       ('1040111', 'Light - 350 ml - Manga', 'Manga', '350 ml', 'Lata', 3.50);
````

6 ) Faça Download do arquivo RecuperacaoAmbiente.zip.

7 ) Descompacte o arquivo.

8 ) Selecione, na área Navigator, em Administration.

9 ) Selecione o link Data Import/Restore.

10 ) Na opção Import From Dump Project Folder escolha o diretório DumpSucosVendas.

11 ) Selecione Start Import.

12 ) Verifique na base Sucos_Vendas se as tabelas foram criadas.

13 ) Podemos, da base Vendas_Sucos, acessar tabelas da base Sucos_Vendas.
````sql
USE vendas_sucos;

SELECT * FROM sucos_vendas.tabela_de_produtos;
````
![](https://cdn3.gnarususercontent.com.br/1222-mysqlmanipulacaodedados/03/2.png)

14 ) A consulta, a seguir, mostra a lista de produtos, na tabela tabela_de_produtos, da base sucos_vendas que ainda não foram incluídas na tabela produtos, da base vendas_sucos:
````sql
SELECT CODIGO_DO_PRODUTO AS CODIGO, NOME_DO_PRODUTO AS DESCRITOR,

EMBALAGEM, TAMANHO, SABOR, PRECO_DE_LISTA AS PRECO_LISTA

FROM sucos_vendas.tabela_de_produtos

WHERE CODIGO_DO_PRODUTO NOT IN (SELECT CODIGO FROM produtos);
````
![](https://cdn3.gnarususercontent.com.br/1222-mysqlmanipulacaodedados/03/3.png)

15 ) No comando INSERT podemos incluir os produtos na tabela sucos_vendas.tabela_de_produtos na tabela vendas_sucos.produtos. Digite e execute:
````sql
INSERT INTO produtos

SELECT CODIGO_DO_PRODUTO AS CODIGO, NOME_DO_PRODUTO AS DESCRITOR,

SABOR, TAMANHO, EMBALAGEM,  PRECO_DE_LISTA AS PRECO_LISTA

FROM sucos_vendas.tabela_de_produtos

WHERE CODIGO_DO_PRODUTO NOT IN (SELECT CODIGO FROM produtos);
````

16 ) Vamos conferir a tabela de produtos. Digite e execute:
````sql
SELECT * FROM produtos;
````
![](https://cdn3.gnarususercontent.com.br/1222-mysqlmanipulacaodedados/03/4.png)

17 ) Mostraremos como incluir dados na tabela de cliente. Digite e execute:
````sql
SELECT * FROM clientes;
````
![](https://cdn3.gnarususercontent.com.br/1222-mysqlmanipulacaodedados/03/5.png)

18 ) Ao lado temos o botão Form Editor:

![](https://cdn3.gnarususercontent.com.br/1222-mysqlmanipulacaodedados/03/6.png)

Teremos uma caixa de diálogo para editar a tabela de Clientes.

![](https://cdn3.gnarususercontent.com.br/1222-mysqlmanipulacaodedados/03/7.png)

19 ) Inclua um novo cliente:
- CPF: 1471156710;
- NOME: Érica Carvalho;
- ENDERECO: R. Iriquiti;
- BAIRRO: Jardins;
- CIDADE: São Paulo;
- ESTADO: SP;
- CEP: 80012212;
- DATA_NASCIMENTO: 1999-09-01;
- IDADE: 27;
- SEXO: F;
- LIMITE_CREDITO: 170000;
- VOLUME_COMPRA: 24500;
- PRIMEIRA_COMPRA: 0;

20 ) Confirme a inclusão. O comando será apresentado e confirme a execução.

21 ) Execute a consulta novamente. Digite e execute:
````sql
SELECT * FROM clientes;
````
![](https://cdn3.gnarususercontent.com.br/1222-mysqlmanipulacaodedados/03/8.png)

O cliente foi incluido.

22 ) Vamos incluir os clientes usando como fonte o outro banco de dados. Digite e execute:
````sql
INSERT INTO CLIENTES

SELECT CPF, NOME, ENDERECO_1 AS ENDERECO, BAIRRO, CIDADE, ESTADO, CEP,

DATA_DE_NASCIMENTO AS DATA_NASCIMENTO, IDADE, SEXO, LIMITE_DE_CREDITO AS LIMITE_CREDITO,

VOLUME_DE_COMPRA AS VOLUME_COMPRA, PRIMEIRA_COMPRA

FROM sucos_vendas.tabela_de_clientes WHERE CPF

NOT IN (SELECT CPF FROM CLIENTES);
````

23 ) Teste o conteúdo da tabela de clientes:
````sql
SELECT * FROM CLIENTES;
````
![](https://cdn3.gnarususercontent.com.br/1222-mysqlmanipulacaodedados/03/9.png)

24 ) Vamos mostrar agora como incluir dados na tabela de vendedores através de arquivos externos. Descompacte o arquivo contido no link desta aula e iremos usar a tabela Vendedores.csv. como fonte.

25 ) Botão da direita do mouse sobre a tabela Vendedores e escolha a opção Table Data Import Wizard.

![](https://cdn3.gnarususercontent.com.br/1222-mysqlmanipulacaodedados/03/10.png)

26 ) Em File Path selecione o arquivo Vendedores.csv.

27 ) Mantenha os dados padrões como mostrado abaixo:

![](https://cdn3.gnarususercontent.com.br/1222-mysqlmanipulacaodedados/03/11.png)

28 ) Observação: Se você visualizar um erro como mostrado abaixo:

![](https://cdn3.gnarususercontent.com.br/1222-mysqlmanipulacaodedados/03/12.png)

Há erro na interpretação da tabela através da lista de caracteres. Para isso faça:

- Abra o arquivo com Notepad clássico;
- Clique arquivo / Salvar como.
- Escolha o padrão ANSI:

![](https://cdn3.gnarususercontent.com.br/1222-mysqlmanipulacaodedados/03/13.png)

Volte a caixa de diálogo e escolha:

![](https://cdn3.gnarususercontent.com.br/1222-mysqlmanipulacaodedados/03/14.png)

Pode existir problemas entre computadores e entre os arquivos baixados. Você deve ver a combinação correta entre o formato do arquivo (Que pode ser modificado no NOTEPAD clássico) e na caixa de diálogo de importação de dados.

![](https://cdn3.gnarususercontent.com.br/1222-mysqlmanipulacaodedados/03/15.png)

29 ) Desmarque a opção FERIAS:

![](https://cdn3.gnarususercontent.com.br/1222-mysqlmanipulacaodedados/03/16.png)

30 ) Clique em Next várias vezes até os dados serem incluídos na tabela de vendedores.

31 ) Verifique o conteúdo da tabela de vendedores.
````sql
SELECT * FROM VENDEDORES;
````
![](https://cdn3.gnarususercontent.com.br/1222-mysqlmanipulacaodedados/03/17.png)


## O que aprendemos?

- Aprendemos a incluir dados em uma tabela, através de comando;
- Vimos a inclusão de vários registros em um único comando;
- Foi mostrado como incluir dados na tabela através de um assistente;
- Mostramos como incluir dados usando um arquivo externo.