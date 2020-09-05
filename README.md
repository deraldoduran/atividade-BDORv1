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
