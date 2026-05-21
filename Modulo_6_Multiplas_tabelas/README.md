## Atividades

### **1. Criação da tabela**

```sql
CREATE EXTERNAL TABLE IF NOT EXISTS default.cliente (
	`id_cliente` int,
	`nome` string,
	`valor_compra` double,
	`loja_cadastro` string
)
ROW FORMAT SERDE 'org.apache.hadoop.hive.serde2.lazy.LazySimpleSerDe'
WITH SERDEPROPERTIES (
	'serialization.format' = ',',
	'field.delim' = ','
)
LOCATION 's3://modulo6-lucaspresente-ebac/cliente/'
TBLPROPERTIES ('has_encrypted_data' = 'false');
```

```sql
CREATE EXTERNAL TABLE IF NOT EXISTS default.transacoes (
	`id_cliente` int,
	`id_transacao` int,
	`valor_compra` double,
	`id_loja` string
)
ROW FORMAT SERDE 'org.apache.hadoop.hive.serde2.lazy.LazySimpleSerDe'
WITH SERDEPROPERTIES (
	'serialization.format' = ',',
	'field.delim' = ','
)
LOCATION 's3://modulo6-lucaspresente-ebac/transacoes/'
TBLPROPERTIES ('has_encrypted_data' = 'false');
```

### **2. Função UNION**

#### [**2.1. Query 1**](https://github.com/Lpresente/SQL_excercicios_ebac/blob/main/Modulo_6_Multiplas_tabelas/query_1.csv.csv)
```sql
SELECT id_cliente
FROM transacoes
UNION
SELECT id_cliente
FROM cliente;
```

### **3. Junções inner/cross**

#### [**3.1. Query 2**](https://github.com/Lpresente/SQL_excercicios_ebac/blob/main/Modulo_6_Multiplas_tabelas/query_2.csv.csv)
```sql
SELECT transacoes.id_cliente,
	cliente.nome
FROM transacoes
	INNER JOIN cliente ON transacoes.id_cliente = cliente.id_cliente;
```

#### [**3.2. Query 3**](https://github.com/Lpresente/SQL_excercicios_ebac/blob/main/Modulo_6_Multiplas_tabelas/query_3.csv.csv)
```sql
SELECT *
FROM cliente
	CROSS JOIN transacoes;
```

### **4. Junções: left / right**

#### [**4.1. Query 4**](https://github.com/Lpresente/SQL_excercicios_ebac/blob/main/Modulo_6_Multiplas_tabelas/query_4.csv.csv)
```sql
SELECT *
FROM transacoes
	LEFT JOIN cliente ON cliente.id_cliente = transacoes.id_cliente;
```

#### [**4.2. Query 5**](https://github.com/Lpresente/SQL_excercicios_ebac/blob/main/Modulo_6_Multiplas_tabelas/query_5.csv.csv)
```sql
SELECT *
FROM transacoes
	RIGHT JOIN cliente ON cliente.id_cliente = transacoes.id_cliente;
```
