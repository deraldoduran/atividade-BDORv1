# atividade-BDORv2
```sql
-- Database: atividade bdorv2

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
CREATE TABLE IF NOT EXISTS pedido (
	num_pedido INT,
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
CREATE TABLE IF NOT EXISTS pedidomudanca (
	num_pedido_mudanca SERIAL NOT NULL PRIMARY KEY,
	listamoveis TEXT[]
) INHERITS (pedido);
```
```SQL
CREATE TABLE IF NOT EXISTS pedidotranscarga (
		num_pedido_transcarga SERIAL NOT NULL PRIMARY KEY,
		listaPRODUTO tpproduto
) INHERITS (pedido);
```
```SQL
CREATE TABLE IF NOT EXISTS pessoajuridica_pedidomudanca(
	pessoa_juridica_fkey INT REFERENCES pessoajuridica (num_pessoajuridica),
	pedido_mudanca_fkey INT REFERENCES pedidomudanca (num_pedido_mudanca)
);
```
```SQL
CREATE TABLE IF NOT EXISTS pessoafisica_pedidomudanca(
	pessoa_fisica_fkey INT REFERENCES pessoafisica (num_pessoafisica),
	pedido_mudanca_fkey INT REFERENCES pedidomudanca (num_pedido_mudanca)
);
```
```sql
CREATE TABLE IF NOT EXISTS pessoajuridica_pedidotranscarga(
	pessoa_juridica_fkey INT REFERENCES pessoajuridica (num_pessoajuridica),
	pedido_transcarga_fkey INT REFERENCES pedidotranscarga (num_pedido_transcarga)
);
```
```SQL
CREATE TABLE IF NOT EXISTS pessoafisica_pedidotranscarga(
	pessoa_fisica_fkey INT REFERENCES pessoafisica (num_pessoafisica),
	pedido_transcarga_fkey INT REFERENCES pedidotranscarga (num_pedido_transcarga)
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
```SQL
insert into pedidomudanca (num_pedido, listamoveis,  dataapanha, localapanha, responsavel, dataentrega, localentrega, valortransporte, valorassegurado, formapagamento, situacaopagamento , observacao) values (100, '{{Papaya}, {Papaya}}', '2019-09-06', ROW('Birchwood', '2', 'Avenue', 'Larus sp.', 'Hobscheid', 'Ij'), 'Marlowe', '2020-06-12', ROW('Derek', '3', 'Lane', 'Nelco Laboratories, Inc.', 'Bardo', 'Gw'), 358.76, 79.71, ROW(4, 698.17), true, 'Foxtrot');
insert into pedidomudanca (num_pedido,listamoveis,  dataapanha, localapanha, responsavel, dataentrega, localentrega, valortransporte, valorassegurado, formapagamento, situacaopagamento , observacao) values (110, '{{Lidocaine and Prilocaine}, {Lidocaine and Prilocaine}}', '2020-07-29', ROW('Eastlawn', '3029', 'Court', 'Francolinus swainsonii', 'Zhangjiafang', 'Mp'), 'Clemens', '2020-07-28', ROW('Kropf', '7711', 'Avenue', 'Hi-Tech Pharmacal Co., Inc.', 'Xiaochuan', 'Pt'), 550.08, 77.87, ROW(3, 978.60), false, 'Victor');
insert into pedidomudanca (num_pedido,listamoveis,  dataapanha, localapanha, responsavel, dataentrega, localentrega, valortransporte, valorassegurado, formapagamento, situacaopagamento , observacao) values (120, '{{Oxacillin}, {oxacillin sodium}}', '2019-01-24', ROW('Sunfield', '8', 'Circle', 'Varanus komodensis', 'Bočar', 'Du'), 'Vernon', '2019-10-20', ROW('Roth', '9', 'Parkway', 'Sagent Pharmaceuticals', 'El Bálsamo', 'Lg'), 866.84, 21.14, ROW(3, 468.95), false, 'Victor');
insert into pedidomudanca (num_pedido,listamoveis,  dataapanha, localapanha, responsavel, dataentrega, localentrega, valortransporte, valorassegurado, formapagamento, situacaopagamento , observacao) values (130, '{{Blues - Mood Support}, {Angelica sinensis radix}, {Aralia quinquefolia}, {Arg. nit.}, {Arsenicum alb.}, {Berber. aqui.}, {Capsicum} , {Cinchona}, {Digitalis}, {Gelsemium}, {Hypericum}, {Ignatia}, {Iodium}, {Kali brom.}, {Kali carb.}, {Mag. phos.}, {Nat. carb.}, {Nat. mur.}, {Phosphorus}, {Salix nigra}, {Sanguinaria}, {Sepia}, {Stramonium}, {Echinacea}, {Ginkgo}}', '2018-10-14', ROW('Express', '148', 'Street', 'Vulpes vulpes', 'Montgomery', 'Ww'), 'Ramsay', '2020-07-28', ROW('Miller', '5489', 'Way', 'Newton Laboratories, Inc.', 'Xuefeng', 'Sx'), 874.65, 31.09, ROW(3, 551.20), true, 'Mike Echo Hotel');
insert into pedidomudanca (num_pedido, listamoveis,  dataapanha, localapanha, responsavel, dataentrega, localentrega, valortransporte, valorassegurado, formapagamento, situacaopagamento , observacao) values (140, '{{Glyburide}, {Glyburide}}', '2019-07-10', ROW('Westport', '0326', 'Park', 'Graspus graspus', 'Opinogóra Górna', 'Bp'), 'Tommie', '2020-05-01', ROW('Oneill', '585', 'Trail', 'MedVantx, Inc.', 'Sakerta Timur', 'Ow'), 490.82, 61.33, ROW(2, 382.10), false, 'India Juliett Echo');
insert into pedidomudanca (num_pedido, listamoveis,  dataapanha, localapanha, responsavel, dataentrega, localentrega, valortransporte, valorassegurado, formapagamento, situacaopagamento , observacao) values (150, '{{Opalescence PF}, {Sodium Fluoride and Potassium Nitrate}}', '2018-11-16', ROW('Pennsylvania', '58014', 'Crossing', 'Vulpes vulpes', 'Pignon', 'Dy'), 'Iorgo', '2020-05-08', ROW('Derek', '75', 'Pass', 'Ultradent Products, Inc.', 'Widuchowa', 'Og'), 024.28, 69.70, ROW(5, 948.23), true, 'X-ray');
insert into pedidomudanca (num_pedido, listamoveis,  dataapanha, localapanha, responsavel, dataentrega, localentrega, valortransporte, valorassegurado, formapagamento, situacaopagamento , observacao) values (160, '{{ALLIUM SATIVUM}, {ALLIUM SATIVUM}}', '2020-03-17', ROW('Warner', '35957', 'Place', 'Otaria flavescens', 'Sangalhos', 'Gr'), 'Bern', '2020-07-30', ROW('Lotheville', '009', 'Place', 'HOMEOLAB USA INC.', 'Xibing', 'Fn'), 897.88, 75.73, ROW(2, 688.56), false, 'X-ray India Tango');
insert into pedidomudanca (num_pedido, listamoveis,  dataapanha, localapanha, responsavel, dataentrega, localentrega, valortransporte, valorassegurado, formapagamento, situacaopagamento , observacao) values (170, '{{Flurazepam}, {Flurazepam Hydrochloride}}', '2020-08-15', ROW('Kensington', '5', 'Point', 'Bettongia penicillata', 'Minshan', 'Bz'), 'Sim', '2020-02-29', ROW('Cody', '30', 'Alley', 'Golden State Medical Supply, Inc.', 'Xindong', 'Ns'), 756.13, 06.27, ROW(5, 820.61), false, 'Papa Echo');
insert into pedidomudanca (num_pedido, listamoveis,  dataapanha, localapanha, responsavel, dataentrega, localentrega, valortransporte, valorassegurado, formapagamento, situacaopagamento , observacao) values (180, '{{Compulsin}, {Arsenicum Album}, {Aresnicum Iodatum}, {Calcarea Carbonica}, {Coffea Cruda}, {Iodum}, {Mancinella}, {Physostigma}, {Silicea}}', '2020-08-22', ROW('Morningstar', '33', 'Plaza', 'Ursus americanus', 'Aleksandrovka', 'Dc'), 'Moises', '2019-12-09', ROW('Lukken', '9757', 'Park', 'Ionx Holdings d/b/a HelloLife Inc.', 'Jiuhe', 'Qp'), 383.94, 54.60, ROW(2, 155.61), false, 'Yankee Delta Kilo');
insert into pedidomudanca (num_pedido, listamoveis,  dataapanha, localapanha, responsavel, dataentrega, localentrega, valortransporte, valorassegurado, formapagamento, situacaopagamento , observacao) values (190, '{{Gamunex-C}, {Immune Globulin Intravenous (Human)}, {10% Caprylate Chromatography Purified}}', '2019-08-05', ROW('Kennedy', '5604', 'Junction', 'Canis lupus baileyi', 'San Diego', 'Hf'), 'Claybourne', '2020-09-04', ROW('Dottie', '9250', 'Crossing', 'GRIFOLS USA, LLC', 'Curry', 'Ko'), 956.68, 59.17, ROW(7, 956.95), true, 'Sierra Oscar X-ray');


```
```SQL
insert into pedidoTRANSCARGA (listaPRODUTO, num_pedido, dataapanha, localapanha, responsavel, dataentrega, localentrega, valortransporte, valorassegurado,formapagamento, situacaopagamento , observacao) values (ROW('MYTAB For GAS', 7, 475.41), 027, '2019-08-27', ROW('Parkside', '34', 'Pass', 'Ovis stonei', 'Votkinsk', 'Yq'), 'Josias', '2019-10-01', ROW('Debs', '6408', 'Hill', 'A-S Medication LLC', 'Staryy Krym', 'Sn'), 725.88, 90.05, ROW(0, 868.13), true, 'India Romeo');
insert into pedidoTRANSCARGA (listaPRODUTO, num_pedido, dataapanha, localapanha, responsavel, dataentrega, localentrega, valortransporte, valorassegurado,formapagamento, situacaopagamento , observacao) values (ROW('Oxygen', 4, 539.50), 547, '2019-04-24', ROW('Spohn', '3315', 'Avenue', 'Cereopsis', 'Cagmanaba', 'Od'), 'Friedrich', '2020-03-30', ROW('Maple', '8704', 'Pass', 'I.D.M.Supply Company', 'Anjiang', 'Ry'), 763.14, 04.41, ROW(8, 869.66), false, 'India Charlie');
insert into pedidoTRANSCARGA (listaPRODUTO, num_pedido, dataapanha, localapanha, responsavel, dataentrega, localentrega, valortransporte, valorassegurado,formapagamento, situacaopagamento , observacao) values (ROW('Vyvanse', 6, 438.39), 113, '2019-06-20', ROW('Corscot', '2068', 'Crossing', 'Iguana iguana', 'Betong', 'Ks'), 'Hazlett', '2020-05-14', ROW('Pepper Wood', '2', 'Pass', 'Lake Medical & Surgical Supply DBA', 'Altunemil', 'Ii'), 487.96, 45.31, ROW(1, 161.18), true, 'Delta');
insert into pedidoTRANSCARGA (listaPRODUTO, num_pedido, dataapanha, localapanha, responsavel, dataentrega, localentrega, valortransporte, valorassegurado,formapagamento, situacaopagamento , observacao) values (ROW('Vaseline', 7, 101.97), 882, '2019-07-23', ROW('Dakota', '3', 'Alley', 'Mazama americana', 'Bánov', 'Xy'), 'Piotr', '2020-02-15', ROW('Oxford', '0938', 'Circle', 'Conopco Inc. d/b/a Unilever', 'Taiping', 'Kc'), 847.96, 84.14, ROW(3, 345.25), false, 'Alfa X-ray');
insert into pedidoTRANSCARGA (listaPRODUTO, num_pedido, dataapanha, localapanha, responsavel, dataentrega, localentrega, valortransporte, valorassegurado,formapagamento, situacaopagamento , observacao) values (ROW('GODDESS GARDEN ORGANICS WATER RESISTANT', 6, 755.53), 601, '2019-05-18', ROW('Kings', '26', 'Lane', 'Pseudocheirus peregrinus', 'Casais de Revelhos', 'Ze'), 'Freddy', '2019-11-19', ROW('Walton', '5', 'Point', 'Crossing Garden', 'Delgado', 'Jz'), 611.89, 54.01, ROW(8, 419.66), true, 'Papa');
insert into pedidoTRANSCARGA (listaPRODUTO, num_pedido, dataapanha, localapanha, responsavel, dataentrega, localentrega, valortransporte, valorassegurado,formapagamento, situacaopagamento , observacao) values (ROW('good neighbor pharmacy nasal decongestant', 7, 184.14), 298, '2020-08-05', ROW('Dovetail', '9', 'Center', 'Plocepasser mahali', 'Värmdö', 'Fz'), 'Farlee', '2020-02-01', ROW('Tennessee', '0', 'Hill', 'Amerisource Bergen', 'Vondrozo', 'Jb'), 684.13, 65.35, ROW(1, 230.16), true, 'Echo Yankee Juliett');
insert into pedidoTRANSCARGA (listaPRODUTO, num_pedido, dataapanha, localapanha, responsavel, dataentrega, localentrega, valortransporte, valorassegurado,formapagamento, situacaopagamento , observacao) values (ROW('Adenosine', 9, 868.08), 798, '2019-02-08', ROW('Ilene', '5', 'Drive', 'Marmota caligata', 'Delgermörön', 'Kk'), 'Hy', '2019-12-16', ROW('Anzinger', '84777', 'Hill', 'Baxter Corporation', 'Mulchén', 'Ry'), 975.91, 65.77, ROW(4, 928.39), false, 'Yankee Alfa');
insert into pedidoTRANSCARGA (listaPRODUTO, num_pedido, dataapanha, localapanha, responsavel, dataentrega, localentrega, valortransporte, valorassegurado,formapagamento, situacaopagamento , observacao) values (ROW('DELFLEX', 1, 179.04), 801, '2020-01-21', ROW('International', '16', 'Terrace', 'Ramphastos tucanus', 'Yatsushiro', 'Ec'), 'Renato', '2019-10-01', ROW('Muir', '3', 'Pass', 'Fresenius America', 'Jinglongqiao', 'Io'), 365.74, 90.82, ROW(6, 236.37), false, 'Uniform X-ray');
insert into pedidoTRANSCARGA (listaPRODUTO, num_pedido, dataapanha, localapanha, responsavel, dataentrega, localentrega, valortransporte, valorassegurado,formapagamento, situacaopagamento , observacao) values (ROW('Triamterene and Hydrochlorothiazide', 2, 420.82), 910, '2020-03-07', ROW('Springview', '8819', 'Plaza', 'Neophoca cinerea', 'Chvaletice', 'Jq'), 'Irvine', '2020-05-03', ROW('Sherman', '3436', 'Place', 'Preferred Pharmaceuticals, Inc', 'Fantino', 'Rs'), 982.87, 60.31, ROW(4, 249.82), true, 'Hotel');
insert into pedidoTRANSCARGA (listaPRODUTO, num_pedido, dataapanha, localapanha, responsavel, dataentrega, localentrega, valortransporte, valorassegurado,formapagamento, situacaopagamento , observacao) values (ROW('Triazolam', 5, 172.32), 458, '2019-01-17', ROW('Anzinger', '280', 'Circle', 'Rana sp.', 'Awsīm', 'Rt'), 'Leland', '2019-10-12', ROW('Surrey', '305', 'Trail', 'Roxane Laboratories, Inc.', 'Calvário', 'Vw'), 844.50, 65.18, ROW(9, 543.71), false, 'Juliett Whiskey');
```
```sql
insert into pessoajuridica_pedidomudanca values (1,8),(2,10),(3,12),(4,14),(5,16);
```
```sql
insert into pessoafisica_pedidomudanca values (1,9),(2,11),(3,13),(4,15),(5,17);
```
```sql
insert into  pessoajuridica_pedidotranscarga values (1,1),(2,3),(3,5),(4,7),(5,9);
```
```sql
insert into  pessoafisica_pedidotranscarga values (1,2),(2,4),(3,6),(4,8),(5,10);
```
```SQL
CREATE TABLE IF NOT EXISTS auditoria (
	operacao VARCHAR(50) NOT NULL,
	usuario VARCHAR(50) NOT NULL,
	DATA TIMESTAMP NOT NULL,
	num_pedido_novo INT,
	num_pedido INT,
	valortransporte_NOVO NUMERIC(10,2),
	valortransporte NUMERIC(10,2),
	valorassegurado_NOVO NUMERIC(10,2),
	valorassegurado NUMERIC(10,2)
);

CREATE OR REPLACE FUNCTION processa_auditoria() RETURNS
TRIGGER AS $log$
BEGIN
  IF (TG_OP = 'DELETE') THEN
  INSERT INTO auditoria SELECT 'EXCLUSAO', USER, NOW(), NEW.*, OLD.*;
  RETURN OLD;
  ELSIF (TG_OP = 'UPDATE') THEN
  INSERT INTO auditoria SELECT 'ATUALIZACAO', USER, NOW(), NEW.*, OLD.*;
  RETURN NEW;
   ELSIF (TG_OP = 'INSERT') THEN
  INSERT INTO auditoria SELECT 'INSERCAO', USER, NOW(), NEW.*;
  RETURN NEW;
  END IF;
  RETURN NULL;
END;
$log$ LANGUAGE plpgsql;

CREATE TRIGGER gatilho_auditoria
AFTER INSERT OR UPDATE OR DELETE
ON pedido
FOR EACH ROW EXECUTE PROCEDURE processa_auditoria();
```
```sql
UPDATE pedidotranscarga SET valortransporte = 800.00 WHERE valortransporte = 725.88;
```
