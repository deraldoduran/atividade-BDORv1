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
