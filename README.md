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
```sql
insert into pessoafisica  (it_cpf, dt_nascimento, datacadastro, endereco, telefone, email, referencia) values ('010358-25', '1987-01-18', '2014-05-11',ROW( 'Orin', '5232', 'CA', '2nd', 'Santa Barbara', 'Yg'), '{(805) 6598392}', 'dlegge0@domainmarket.com', 'Quebec  Mike');
insert into pessoafisica  (it_cpf, dt_nascimento, datacadastro, endereco, telefone, email, referencia) values ('465767-02', '1977-01-10', '2017-01-04',ROW( 'Autumn Leaf', '69', 'TX', 'Larry', 'San Antonio', 'Vg'), '{(210) 4911413}', 'ddmitrievski1@ucoz.ru', 'Papa Whiskey Oscar');
insert into pessoafisica  (it_cpf, dt_nascimento, datacadastro, endereco, telefone, email, referencia) values ('956190-88', '1938-09-26', '2016-04-17',ROW( 'Oak', '447', 'TX', 'Declaration', 'Lubbock', 'Wq'),'{(806) 4115001}', 'mpashba2@multiply.com', 'Yankee Golf');
insert into pessoafisica  (it_cpf, dt_nascimento, datacadastro, endereco, telefone, email, referencia) values ('444930-12', '1977-01-09', '2013-03-27',ROW( 'Springview', '8188', 'AZ', 'Hooker', 'Mesa', 'Fa'), '{(480) 1579571}', 'vakker3@live.com', 'Tango Hotel Mike');
insert into pessoafisica  (it_cpf, dt_nascimento, datacadastro, endereco, telefone, email, referencia) values ('294390-42', '2015-03-08', '2013-08-22',ROW( 'Hovde', '8', 'MD', 'Bayside', 'Bethesda', 'Cs'), '{(202) 1864756}', 'cdemalchar4@europa.eu', 'Golf Echo Lima');
insert into pessoafisica  (it_cpf, dt_nascimento, datacadastro, endereco, telefone, email, referencia) values ('457316-85', '1941-09-01', '2017-09-12', ROW('Bayside', '14', 'NC', 'Golf View', 'Charlotte', 'Gb'), '{(704) 4713991}', 'bheers5@technorati.com', 'Delta Uniform');
insert into pessoafisica  (it_cpf, dt_nascimento, datacadastro, endereco, telefone, email, referencia) values ('175292-15', '1991-09-05', '2013-10-03',ROW('Rieder', '48', 'DC', 'Declaration', 'Washington', 'Iq'), '{(202) 4427648}', 'sduberry6@wunderground.com', 'Charlie Delta Romeo');
insert into pessoafisica  (it_cpf, dt_nascimento, datacadastro, endereco, telefone, email, referencia) values ('873486-30', '1983-09-03', '2015-01-08', ROW('Sauthoff', '2321', 'CA', 'Mcbride', 'Riverside', 'Mc'), '{(951) 1060158}', 'athurbon7@cocolog-nifty.com', 'Golf Zulu Charlie');
```
```SQL
insert into pessoajuridica (it_cgc, it_inscrestadual, datacadastro, endereco, telefone, email, referencia) values ('57984680300149', '52059733100987', '2019-01-15', ROW('Sherman', '48', 'Drive', 'Cynictis penicillata', 'Borovskoy', 'Ml'), '{{4281638747},{555555555}}', 'giddons0@discuz.net', 'Glennie');
insert into pessoajuridica (it_cgc, it_inscrestadual, datacadastro, endereco, telefone, email, referencia) values ('28024302939371', '38706958406975', '2020-05-15', ROW('Monterey', '0172', 'Terrace', 'Ctenophorus ornatus', 'Shaogongzhuang', 'Ji'), '{4053941578}', 'acathrall1@mapquest.com', 'Anestassia');
insert into pessoajuridica (it_cgc, it_inscrestadual, datacadastro, endereco, telefone, email, referencia) values ('25266406596881', '17628311459993', '2019-02-26', ROW('Swallow', '0', 'Crossing', 'Sterna paradisaea', 'Balagui', 'Wy'), '{6038908352}', 'cmclaughlan2@java.com', 'Catlaina');
insert into pessoajuridica (it_cgc, it_inscrestadual, datacadastro, endereco, telefone, email, referencia) values ('74816626138555', '47844661462010', '2018-10-16', ROW('Swallow', '89373', 'Court', 'Macropus rufus', 'Idi Rayeuk', 'Gz'), '{5999342982}', 'earpin3@dion.ne.jp', 'Ermina');
insert into pessoajuridica (it_cgc, it_inscrestadual, datacadastro, endereco, telefone, email, referencia) values ('85612268511379', '26597718915403', '2019-03-04', ROW('Bay', '0', 'Place', 'Ursus americanus', 'Cintawana', 'Kf'), '{{7228341468},{8899955444}}', 'fruoss4@google.com.br', 'Fayette');
insert into pessoajuridica (it_cgc, it_inscrestadual, datacadastro, endereco, telefone, email, referencia) values ('11161205263925', '97227872944736', '2018-10-10', ROW('Summer Ridge', '626', 'Way', 'Carduelis uropygialis', 'Zharkent', 'Gz'), '{9008296927}', 'sglendenning5@answers.com', 'Samara');
insert into pessoajuridica (it_cgc, it_inscrestadual, datacadastro, endereco, telefone, email, referencia) values ('93350863125807', '71437781903646', '2018-11-01', ROW('Holy Cross', '241', 'Trail', 'Tursiops truncatus', 'Pailou', 'Ia'), '{7738328249}', 'iishaki6@walmart.com', 'Imojean');
insert into pessoajuridica (it_cgc, it_inscrestadual, datacadastro, endereco, telefone, email, referencia) values ('06192169972476', '69500412996249', '2019-12-31', ROW('Orin', '98977', 'Point', 'Laniarius ferrugineus', 'Huangqiang', 'Ak'), '{7615810289}', 'kbaiyle7@kickstarter.com', 'Kathie');
insert into pessoajuridica (it_cgc, it_inscrestadual, datacadastro, endereco, telefone, email, referencia) values ('60128643657184', '88850546161474', '2019-06-15', ROW('Jackson', '143', 'Center', 'Pelecans onocratalus', 'Shanxi', 'We'), '{3586489681}', 'cboutton8@so-net.ne.jp', 'Cherish');
insert into pessoajuridica (it_cgc, it_inscrestadual, datacadastro, endereco, telefone, email, referencia) values ('83973285821068', '49511404190218', '2018-12-30', ROW('Saint Paul', '7', 'Park', 'Nucifraga columbiana', 'Buguruslan', 'Ie'), '{7061257778}', 'kovitz9@wordpress.org', 'Kelila');
```
