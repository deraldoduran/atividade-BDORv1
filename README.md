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
