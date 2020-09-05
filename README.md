# atividade-BDORv1
```sql
-- Database: atividade_bdor

CREATE TYPE tpproduto AS(
	produto TEXT,
	quantidade INT,
	peso NUMERIC(10,2)
);
```
```SQL
CREATE TYPE tppagamento AS (
	it_parcelas INT,
	ft_valor NUMERIC(10,2)
);
```
```sql
CREATE TYPE tpend AS(
	rua VARCHAR(100),
	numero INT,
	complemento VARCHAR(50),
	bairro VARCHAR(50),
	cidade VARCHAR(50),
	estado VARCHAR(2)
);
```
```SQL
CREATE TABLE IF NOT EXISTS pessoa (
	datacadastro DATE,
	endereco tpend,
	telefone TEXT[],
	email VARCHAR(50),
	referencia TEXT
);
```
```SQL
CREATE TABLE IF NOT EXISTS pessoafisica (
	num_pessoafisica SERIAL NOT NULL PRIMARY KEY,
	it_cpf VARCHAR(9),
	dt_nascimento DATE
) INHERITS (pessoa);
```
```sql
CREATE TABLE IF NOT EXISTS pessoajuridica (
	num_pessoajuridica SERIAL NOT NULL PRIMARY KEY,
	it_cgc VARCHAR(14),
	it_inscrestadual VARCHAR(14)
) INHERITS (pessoa);
```
```SQL
CREATE TABLE IF NOT EXISTS pedido_key (
	num_pedido INT PRIMARY KEY,
	dataapanha DATE,
	localapanha tpend,
	responsavel VARCHAR(255),
	dataentrega DATE,
	localentrega tpend,
	valortransporte NUMERIC(10,2),
	valorassegurado NUMERIC(10,2),
	formapagamento tppagamento,
	situacaopagamento BOOL,
	observacao TEXT
);
```
```SQL
CREATE TABLE IF NOT EXISTS pedidomudanca_KEY (
	listamoveis TEXT[]
) INHERITS (pedido_KEY);
```
```SQL
CREATE TABLE IF NOT EXISTS pedidoTRANSCARGA_KEY (
		listaPRODUTO tpproduto
) INHERITS (pedido_KEY);
```
```SQL
CREATE TABLE IF NOT EXISTS pessoajuridica_pedido(
	pessoa_juridica_fkey INT REFERENCES pessoajuridica (num_pessoajuridica),
	pedido_mudanca_fkey INT REFERENCES pedido_KEY (num_pedido)
);
```
```SQL
CREATE TABLE IF NOT EXISTS pessoafisica_pedido(
	pessoa_fisica_fkey INT REFERENCES pessoafisica (num_pessoafisica),
	pedido_mudanca_fkey INT REFERENCES pedido_KEY (num_pedido)
);
```
