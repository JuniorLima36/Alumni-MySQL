# Sobre os Cursos de MySQL - Alumini
O curso de MySQL oferecido pela Alura como parte do programa ONE (Oracle Next Education) é uma excelente oportunidade para quem deseja dominar uma das ferramentas de banco de dados mais utilizadas no mercado de tecnologia. Voltado para iniciantes e também para quem já possui conhecimentos básicos, o curso oferece uma abordagem prática e orientada para o desenvolvimento de habilidades que são altamente demandadas no mercado de trabalho.
O que você aprenderá no curso:

- **Modelagem de Banco de Dados**: Aprenda a planejar e estruturar bancos de dados relacionais para armazenar informações de forma eficiente e organizada.
- **Comandos SQL Essenciais**: Domine os comandos básicos e avançados, como criação de tabelas, inserção de dados, consultas e atualizações.
- **Relacionamentos e Normalização**: Entenda como relacionar tabelas e garantir a integridade dos dados, utilizando boas práticas de normalização.
- **Consultas Avançadas**: Explore técnicas como JOINs, subconsultas e funções agregadas para criar relatórios e análises mais complexas.
- **Gerenciamento de Dados**: Aprenda a manipular grandes volumes de informações e a realizar backups e restaurações do banco de dados.

Além de ensinar as bases do MySQL, o curso também prepara você para entender conceitos fundamentais de bancos de dados, que podem ser aplicados em diferentes áreas, como desenvolvimento web, análise de dados e sistemas empresariais.

# MySQL Comandos 

### MySQL SELECT
**Descrição:** Recupera dados de uma tabela.
````sql
SELECT nome, idade FROM usuarios;
````

---

### MySQL WHERE
Filtra os dados com base em uma condição.
````sql
SELECT * FROM usuarios WHERE idade > 18;
````

---

### MySQL AND, OR, NOT
**Descrição:** Usados para combinar condições.
````sql
SELECT * FROM usuarios WHERE idade > 18 AND cidade = 'São Paulo';
````

---

### MySQL ORDER BY
**Descrição:** Ordena os resultados.
````sql
SELECT * FROM usuarios ORDER BY idade DESC;
````

---

### MySQL INSERT INTO
**Descrição:** Insere dados em uma tabela.
````sql
INSERT INTO usuarios (nome, idade) VALUES ('Junior', 25);
````

---

### MySQL NULL Values
**Descrição:** Trabalha com valores nulos.
````sql
SELECT * FROM usuarios WHERE nome IS NULL;
````

---

### MySQL UPDATE
**Descrição:** Atualiza registros existentes.
````sql
UPDATE usuarios SET idade = 26 WHERE nome = 'Junior';
````

---

### MySQL DELETE
**Descrição:** Exclui registros de uma tabela.
````sql
DELETE FROM usuarios WHERE nome = 'Junior';
````

---

### MySQL LIMIT
**Descrição:** Limita o número de resultados retornados.
````sql
SELECT * FROM usuarios LIMIT 5;
````

---

### MySQL MIN and MAX
**Descrição:** Retorna o valor mínimo ou máximo de uma coluna.
````sql
SELECT MIN(idade), MAX(idade) FROM usuarios;
````

---

### MySQL COUNT, AVG, SUM
**Descrição:** Conta, calcula a média ou soma os valores.
````sql
SELECT COUNT(*), AVG(idade), SUM(idade) FROM usuarios;
````

---

### MySQL LIKE
**Descrição:** Filtra registros com base em padrões.
````sql
SELECT * FROM usuarios WHERE nome LIKE 'J%';
````

---

### MySQL Wildcards
**Descrição:** Utiliza caracteres especiais no padrão de busca.
````sql
SELECT * FROM usuarios WHERE nome LIKE 'J__son';  -- Dois caracteres antes de 'son'
````

---

### MySQL IN
**Descrição:** Filtra valores dentro de um conjunto.
````sql
SELECT * FROM usuarios WHERE cidade IN ('São Paulo', 'Rio de Janeiro');
````

---

### MySQL BETWEEN
**Descrição:** Filtra valores dentro de um intervalo.
````sql
SELECT * FROM usuarios WHERE idade BETWEEN 20 AND 30;
````

---

### MySQL Aliases
**Descrição:** Cria um apelido para tabelas ou colunas.
````sql
SELECT nome AS nome_usuario FROM usuarios;
````

---

### MySQL Joins
**Descrição:** Combina dados de múltiplas tabelas.
````sql
SELECT * FROM usuarios u INNER JOIN pedidos p ON u.id = p.usuario_id;
````

---

### MySQL INNER JOIN
**Descrição:** Retorna registros que têm correspondência em ambas as tabelas.
````sql
SELECT * FROM usuarios u INNER JOIN pedidos p ON u.id = p.usuario_id;
````

---

### MySQL LEFT JOIN
**Descrição:** Retorna todos os registros da tabela da esquerda e os correspondentes da tabela da direita.
````sql
SELECT * FROM usuarios u LEFT JOIN pedidos p ON u.id = p.usuario_id;
````

---

### MySQL RIGHT JOIN
**Descrição:** Retorna todos os registros da tabela da direita e os correspondentes da tabela da esquerda.
````sql
SELECT * FROM usuarios u RIGHT JOIN pedidos p ON u.id = p.usuario_id;
````

---

### MySQL CROSS JOIN
**Descrição:** Retorna o produto cartesiano de ambas as tabelas.
````sql
SELECT * FROM usuarios u CROSS JOIN pedidos p;
````

---

### MySQL Self Join
**Descrição:** Junta uma tabela consigo mesma.
````sql
SELECT a.nome, b.nome FROM usuarios a, usuarios b WHERE a.id = b.referente_id;
````

---

### MySQL UNION
**Descrição:** Combina os resultados de duas ou mais consultas SELECT.
````sql
SELECT nome FROM usuarios WHERE cidade = 'São Paulo'
UNION
SELECT nome FROM usuarios WHERE cidade = 'Rio de Janeiro';
````

---

### MySQL GROUP BY
**Descrição:** Agrupa os resultados com base em uma coluna.
````sql
SELECT cidade, COUNT(*) FROM usuarios GROUP BY cidade;
````

---

### MySQL HAVING
**Descrição:** Filtra os resultados após o GROUP BY.
````sql
SELECT cidade, COUNT(*) FROM usuarios GROUP BY cidade HAVING COUNT(*) > 5;
````

---

### MySQL EXISTS
**Descrição:** Verifica a existência de um conjunto de resultados.
````sql
SELECT nome FROM usuarios WHERE EXISTS (SELECT 1 FROM pedidos WHERE usuario_id = usuarios.id);
````

---

### MySQL ANY, ALL
**Descrição:** Compara valores com qualquer ou todos os valores de um conjunto.
````sql
SELECT nome FROM usuarios WHERE idade > ALL (SELECT idade FROM usuarios WHERE cidade = 'São Paulo');
````

---

### MySQL INSERT SELECT
**Descrição:** Insere dados selecionados de uma tabela em outra.
````sql
INSERT INTO backup_usuarios (nome, idade)
SELECT nome, idade FROM usuarios WHERE cidade = 'São Paulo';
````

---

### MySQL CASE
**Descrição:** Condiciona valores em uma consulta.
````sql
SELECT nome, 
  CASE 
    WHEN idade >= 18 THEN 'Adulto'
    ELSE 'Menor de Idade'
  END AS categoria
FROM usuarios;
````

---

### MySQL Null Functions
**Descrição:** Lida com valores nulos.
````sql
SELECT COALESCE(nome, 'Desconhecido') FROM usuarios;
````

---

### MySQL Comments
**Descrição:** Comenta uma linha ou bloco de código.
````sql
-- Este é um comentário de linha
SELECT * FROM usuarios; /* Este é um comentário em bloco */
````

---

### MySQL Operators
**Descrição:** Operadores como =, !=, <, >, <=, >=.
````sql
SELECT * FROM usuarios WHERE idade >= 18 AND idade <= 30;
````


### MySQL Database
**Descrição:** Representa um banco de dados no MySQL.
````sql
CREATE DATABASE minha_loja;
````

---

### MySQL Create DB
**Descrição:** Cria um novo banco de dados.
````sql
CREATE DATABASE nome_do_banco;
````

---

### MySQL Drop DB
**Descrição:** Exclui um banco de dados existente.
````sql
DROP DATABASE nome_do_banco;
````

---

### MySQL Create Table
**Descrição:** Cria uma nova tabela dentro de um banco de dados.
````sql
CREATE TABLE usuarios (
  id INT AUTO_INCREMENT,
  nome VARCHAR(100),
  idade INT,
  PRIMARY KEY(id)
);
````

---

### MySQL Drop Table
**Descrição:** Exclui uma tabela existente de um banco de dados.
````sql
DROP TABLE usuarios;
````

---

### MySQL Alter Table
**Descrição:** Modifica uma tabela existente (por exemplo, adicionar ou excluir colunas).
````sql
ALTER TABLE usuarios ADD email VARCHAR(100);
````

---

### MySQL Constraints
**Descrição:** Define restrições em colunas para garantir integridade dos dados (ex: NOT NULL, UNIQUE, etc).
````sql
CREATE TABLE usuarios (
  id INT AUTO_INCREMENT PRIMARY KEY,
  nome VARCHAR(100) NOT NULL,
  email VARCHAR(100) UNIQUE
);
````

---

### MySQL Not Null
**Descrição:** Define que uma coluna não pode ter valores nulos.
````sql
CREATE TABLE produtos (
  id INT AUTO_INCREMENT PRIMARY KEY,
  nome VARCHAR(100) NOT NULL
);
````

---

### MySQL Unique
**Descrição:** Garante que os valores em uma coluna sejam exclusivos.
````sql
CREATE TABLE usuarios (
  id INT AUTO_INCREMENT PRIMARY KEY,
  email VARCHAR(100) UNIQUE
);
````

---

### MySQL Primary Key
**Descrição:** Define uma chave primária para identificar de forma única os registros.
````sql
CREATE TABLE usuarios (
  id INT AUTO_INCREMENT PRIMARY KEY,
  nome VARCHAR(100)
);
````

---

### MySQL Foreign Key
**Descrição:** Define uma chave estrangeira para criar um relacionamento entre tabelas.
````sql
CREATE TABLE pedidos (
  id INT AUTO_INCREMENT PRIMARY KEY,
  usuario_id INT,
  FOREIGN KEY (usuario_id) REFERENCES usuarios(id)
);
````

---

### MySQL Check
**Descrição:** Define uma condição para garantir que os dados atendam a uma restrição específica.
````sql
CREATE TABLE produtos (
  id INT AUTO_INCREMENT PRIMARY KEY,
  preco DECIMAL(10, 2),
  CHECK (preco >= 0)
);
````

---

### MySQL Default
**Descrição:** Define um valor padrão para uma coluna, caso não seja fornecido.
````sql
CREATE TABLE usuarios (
  id INT AUTO_INCREMENT PRIMARY KEY,
  nome VARCHAR(100) NOT NULL,
  status VARCHAR(20) DEFAULT 'ativo'
);
````

---

### MySQL Create Index
**Descrição:** Cria um índice para melhorar a performance de consultas.
````sql
CREATE INDEX idx_nome ON usuarios (nome);
````

---

### MySQL Auto Increment
**Descrição:** Define uma coluna para incrementar automaticamente o valor (geralmente usada para chaves primárias).
````sql
CREATE TABLE usuarios (
  id INT AUTO_INCREMENT PRIMARY KEY,
  nome VARCHAR(100)
);
````

---

### MySQL Dates
**Descrição:** Trabalha com tipos de dados de data e hora, como DATE, DATETIME, TIMESTAMP, etc.
````sql
CREATE TABLE eventos (
  id INT AUTO_INCREMENT PRIMARY KEY,
  nome VARCHAR(100),
  data_evento DATE
);
````

---

### MySQL Views
**Descrição:** Cria uma visão (view), que é uma consulta armazenada como se fosse uma tabela.
````sql
CREATE VIEW usuarios_ativos AS
SELECT * FROM usuarios WHERE status = 'ativo';
````

---


## MySQL References
**Descrição:** Usado para criar uma referência de chave estrangeira entre tabelas.
````sql
CREATE TABLE pedidos (
  id INT AUTO_INCREMENT PRIMARY KEY,
  usuario_id INT,
  FOREIGN KEY (usuario_id) REFERENCES usuarios(id)
);
````

---

## **MySQL Data Types**
**Descrição:** Define os tipos de dados das colunas em uma tabela. Alguns tipos comuns incluem:
- INT para números inteiros.
- VARCHAR para strings de comprimento variável.
- DATE para datas.
- DECIMAL para números decimais.
- TEXT para textos longos.

````sql
CREATE TABLE produtos (
  id INT AUTO_INCREMENT PRIMARY KEY,
  nome VARCHAR(100),
  preco DECIMAL(10, 2),
  descricao TEXT,
  data_lancamento DATE
);
````

---

## **MySQL Functions**
Funções incorporadas para manipulação de dados. Alguns exemplos:
**Descrição:** COUNT(): Conta o número de registros.
````sql
SELECT COUNT(*) FROM usuarios;
````

---

**Descrição:** AVG(): Calcula a média de uma coluna numérica.
````sql
SELECT AVG(idade) FROM usuarios;
````

---

**Descrição:** CONCAT(): Concatena duas ou mais strings.
````sql
SELECT CONCAT(nome, ' ', sobrenome) AS nome_completo FROM usuarios;
````

---

**Descrição:** NOW(): Retorna a data e hora atuais.
````sql
SELECT NOW();
````

---

**Descrição:** UPPER(): Converte uma string para maiúsculas.
````sql
SELECT UPPER(nome) FROM usuarios;
````

---

**Descrição:** LOWER(): Converte uma string para minúsculas.
````sql
SELECT LOWER(nome) FROM usuarios;
````

---

**Descrição:** ROUND(): Arredonda um valor numérico para um número especificado de casas decimais.
````sql
SELECT ROUND(preco, 2) FROM produtos;
````

---

## MySQL Numeric Functions
**Descrição:** ABS() Retorna o valor absoluto de um número.
````sql
SELECT ABS(-10);  -- Retorna 10
````

---

**Descrição:** CEIL() ou CEILING() Retorna o menor inteiro maior ou igual ao número.
````sql
SELECT CEIL(4.2);  -- Retorna 5
````

---
 
**Descrição:** FLOOR() Retorna o maior inteiro menor ou igual ao número.
````sql
SELECT FLOOR(4.7);  -- Retorna 4
````

---

**Descrição:** ROUND() Arredonda um número para o número de casas decimais especificado.
````sql
SELECT ROUND(3.14159, 2);  -- Retorna 3.14
````

---

**Descrição:** MOD() Retorna o resto de uma divisão.
````sql
SELECT MOD(10, 3);  -- Retorna 1
````

---

**Descrição:** RAND() Retorna um número aleatório entre 0 e 1.
````sql
SELECT RAND();  -- Retorna um número aleatório, por exemplo, 0.9576
````

---

**Descrição:** SIGN() Retorna o sinal de um número: 1 para positivo, 0 para zero e -1 para negativo.
````sql
SELECT SIGN(-5);  -- Retorna -1
````

---

**Descrição:** PI() Retorna o valor de π (pi).
````sql
SELECT PI();  -- Retorna 3.14159265358979
````

---

**Descrição:** POWER() ou POW() Retorna o valor de um número elevado a uma potência.
````sql
SELECT POW(2, 3);  -- Retorna 8
````

---

**Descrição:** SQRT() Retorna a raiz quadrada de um número.
````sql
SELECT SQRT(16);  -- Retorna 4
````

---

**Descrição:** EXP() Retorna o valor de e (base dos logaritmos naturais) elevado à potência fornecida.
````sql
SELECT EXP(1);  -- Retorna 2.71828182845905
````

---

**Descrição:** LOG() Retorna o logaritmo natural de um número.
````sql
SELECT LOG(10);  -- Retorna 2.30258509299405
````

---

**Descrição:** LOG10() Retorna o logaritmo de base 10 de um número.
````sql
SELECT LOG10(100);  -- Retorna 2
````

---

**Descrição:** DEGREES() Converte um valor de radianos para graus.
````sql
SELECT DEGREES(PI());  -- Retorna 180
````

---

**Descrição:** RADIANS() Converte um valor de graus para radianos.
````sql
SELECT RADIANS(180);  -- Retorna 3.14159265358979
````

---


## **MySQL Date Functions**

**Descrição:** CURDATE() Retorna a data atual no formato YYYY-MM-DD.
````sql
SELECT CURDATE();  -- Exemplo: '2025-01-30'
````

---

**Descrição:** CURRENT_DATE() Funciona como CURDATE(), retornando a data atual.
````sql
SELECT CURRENT_DATE();  -- Exemplo: '2025-01-30'
````

---

**Descrição:** NOW() Retorna a data e a hora atuais no formato YYYY-MM-DD HH:MM:SS.
````sql
SELECT NOW();  -- Exemplo: '2025-01-30 12:34:56'
````

---

**Descrição:** CURRENT_TIMESTAMP() Retorna a data e a hora atuais, similar ao NOW().
````sql
SELECT CURRENT_TIMESTAMP();  -- Exemplo: '2025-01-30 12:34:56'
````

---

**Descrição:** DATE() Extrai a parte da data de um valor DATETIME ou TIMESTAMP.
````sql
SELECT DATE('2025-01-30 12:34:56');  -- Retorna '2025-01-30'
````

---

**Descrição:** TIME() Extrai a parte de tempo de um valor DATETIME ou TIMESTAMP.
````sql
SELECT TIME('2025-01-30 12:34:56');  -- Retorna '12:34:56'
````

---

**Descrição:** YEAR() Retorna o ano de uma data.
````sql
SELECT YEAR('2025-01-30');  -- Retorna 2025
````

---

**Descrição:** MONTH() Retorna o mês de uma data.
````sql
SELECT MONTH('2025-01-30');  -- Retorna 1
````

---

**Descrição:** DAY() Retorna o dia do mês de uma data.
````sql
SELECT DAY('2025-01-30');  -- Retorna 30
````

---

**Descrição:** DAYOFMONTH() Retorna o dia do mês (semelhante a DAY()).
````sql
SELECT DAYOFMONTH('2025-01-30');  -- Retorna 30
````

---

**Descrição:** DAYOFWEEK() Retorna o número do dia da semana (1 para domingo, 7 para sábado).
````sql
SELECT DAYOFWEEK('2025-01-30');  -- Retorna 5 (quinta-feira)
````

---

**Descrição:** DAYOFYEAR() Retorna o número do dia do ano (1 a 366).
````sql
SELECT DAYOFYEAR('2025-01-30');  -- Retorna 30
````

---

**Descrição:** MONTHNAME() Retorna o nome completo do mês.
````sql
SELECT MONTHNAME('2025-01-30');  -- Retorna 'January'
````

---

**Descrição:** DAYNAME() Retorna o nome completo do dia da semana.
````sql
SELECT DAYNAME('2025-01-30');  -- Retorna 'Thursday'
````

---

**Descrição:** ADDDATE() ou DATE_ADD() Adiciona um intervalo de tempo a uma data.
````sql
SELECT ADDDATE('2025-01-30', INTERVAL 10 DAY);  -- Retorna '2025-02-09'
````

---

**Descrição:** SUBDATE() ou DATE_SUB() Subtrai um intervalo de tempo de uma data.
````sql
SELECT SUBDATE('2025-01-30', INTERVAL 10 DAY);  -- Retorna '2025-01-20'
````

---

**Descrição:** DATEDIFF() Retorna a diferença em dias entre duas datas.
````sql
SELECT DATEDIFF('2025-01-30', '2025-01-20');  -- Retorna 10
````

---

**Descrição:** TIMESTAMP() Retorna um valor DATETIME para um valor de data e hora especificado.
````sql
SELECT TIMESTAMP('2025-01-30', '12:34:56');  -- Retorna '2025-01-30 12:34:56'
````

---

**Descrição:** UNIX_TIMESTAMP() Retorna o timestamp UNIX (número de segundos desde 1970-01-01 00:00:00 UTC) de uma data.
````sql
SELECT UNIX_TIMESTAMP('2025-01-30 12:34:56');  -- Retorna 1735626896
````

---

**Descrição:** FROM_UNIXTIME() Converte um timestamp UNIX para uma data.
````sql
SELECT FROM_UNIXTIME(1735626896);  -- Retorna '2025-01-30 12:34:56'
````

---

**Descrição:** STR_TO_DATE() Converte uma string para um valor de data baseado em um formato específico.
````sql
SELECT STR_TO_DATE('30-01-2025', '%d-%m-%Y');  -- Retorna '2025-01-30'
````

---

**Descrição:** DATE_FORMAT() Formata uma data de acordo com um formato especificado.
````sql
SELECT DATE_FORMAT('2025-01-30', '%W, %M %d, %Y');  -- Retorna 'Thursday, January 30, 2025'
````

---



## **MySQL Advanced Functions**
**Descrição:** COALESCE() Retorna o primeiro valor não nulo em uma lista de valores.
````sql
SELECT COALESCE(NULL, NULL, 'primeiro_valor', 'segundo_valor');  -- Retorna 'primeiro_valor'
````

---

**Descrição:** IFNULL() Retorna um valor substituto se o valor fornecido for NULL.
````sql
SELECT IFNULL(nome, 'Desconhecido') FROM usuarios;  -- Se nome for NULL, retorna 'Desconhecido'
````

---

**Descrição:** NULLIF() Retorna NULL se os dois valores fornecidos forem iguais, caso contrário, retorna o primeiro valor.
````sql
SELECT NULLIF(10, 10);  -- Retorna NULL
SELECT NULLIF(10, 20);  -- Retorna 10
````

---

**Descrição:** CASE Executa expressões condicionais, funcionando como um if dentro de uma consulta.
````sql
SELECT nome, 
  CASE
    WHEN idade >= 18 THEN 'Adulto'
    ELSE 'Menor'
  END AS categoria
FROM usuarios;
````

---

**Descrição:** GREATEST() Retorna o maior valor entre os argumentos fornecidos.
````sql
SELECT GREATEST(10, 20, 5);  -- Retorna 20
````

---

**Descrição:** LEAST() Retorna o menor valor entre os argumentos fornecidos.
````sql
SELECT LEAST(10, 20, 5);  -- Retorna 5
````

---

**Descrição:** CONVERT() Converte um valor de um tipo de dados para outro.
````sql
SELECT CONVERT('2025-01-30', DATE);  -- Converte string para tipo de dados DATE
````

---

**Descrição:** CAST() Similar ao CONVERT(), converte um valor de um tipo de dados para outro, mas com sintaxe diferente.
````sql
SELECT CAST('2025-01-30' AS DATE);  -- Converte string para tipo de dados DATE
````

---

**Descrição:**  BIN() Converte um valor para uma string binária (base 2).
````sql
SELECT BIN(10);  -- Retorna '1010'
````

---

**Descrição:** HEX() Converte um valor para uma string hexadecimal.
````sql
SELECT HEX(255);  -- Retorna 'FF'
````

---

**Descrição:** OCT() Converte um valor para uma string octal.
````sql
SELECT OCT(8);  -- Retorna '10'
````

---

**Descrição:** UNHEX() Converte uma string hexadecimal de volta para o valor original.
````sql
SELECT UNHEX('FF');  -- Retorna 255
````

---

**Descrição:** LAST_INSERT_ID() Retorna o último valor gerado automaticamente para uma coluna AUTO_INCREMENT.
````sql
INSERT INTO usuarios (nome) VALUES ('João');
SELECT LAST_INSERT_ID();  -- Retorna o id gerado para o último usuário inserido
````

---

**Descrição:** GROUP_CONCAT() Concatena os valores de uma coluna em um único valor.
````sql
SELECT GROUP_CONCAT(nome) FROM usuarios;  -- Retorna os nomes concatenados
````

---

**Descrição:** FIND_IN_SET() Retorna a posição de uma string em uma lista separada por vírgulas.
````sql
SELECT FIND_IN_SET('João', 'Maria,João,José');  -- Retorna 2
````

---

**Descrição:** MD5() Retorna o valor MD5 (hash) de uma string.
````sql
SELECT MD5('senha');  -- Retorna o hash MD5 de 'senha'
````

---

**Descrição:** SHA1() Retorna o valor SHA-1 (hash) de uma string.
````sql
SELECT SHA1('senha');  -- Retorna o hash SHA-1 de 'senha'
````

---

**Descrição:** UUID() Gera um identificador único universal (UUID).
````sql
SELECT UUID();  -- Exemplo de retorno: 'a2e6d2f2-8c62-11eb-9f1d-8a2a0d6b9444'
````

---

**Descrição:** RAND() Retorna um número aleatório entre 0 e 1.
````sql
SELECT RAND();  -- Exemplo de retorno: 0.637
````

---

**Descrição:** SHA2() Retorna o valor SHA-2 (hash) de uma string, com a opção de definir o número de bits (256 ou 512).
````sql
SELECT SHA2('senha', 256);  -- Retorna o hash SHA-256 de 'senha'
````

---