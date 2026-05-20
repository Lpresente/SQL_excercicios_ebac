## Atividades

### **2. Selecionando dados**

```sql
CREATE EXTERNAL TABLE transacoes(
  id_cliente BIGINT, 
  id_transacao BIGINT,
  valor FLOAT,
  id_loja STRING) 
ROW FORMAT SERDE 'org.apache.hadoop.hive.serde2.OpenCSVSerde'
WITH SERDEPROPERTIES ('separatorChar' = ',', 'quoteChar' = '"', 'escapeChar' = '\\')
STORED AS TEXTFILE
LOCATION 's3://bucket-lucaspresente-transacoes/'
```
#### [**2.1. Query 1**](https://github.com/Lpresente/SQL_excercicios_ebac/blob/main/Mod3_tabelas/query_1.csv.csv)
```sql
SELECT *
FROM transacoes
```

#### [**2.2. Query 2**](https://github.com/Lpresente/SQL_excercicios_ebac/blob/main/Mod3_tabelas/query_2.csv.csv)
```sql
SELECT id_cliente,
	valor,
	id_loja AS nome_loja
FROM transacoes;
```

#### [**2.3. Query 3**](https://github.com/Lpresente/SQL_excercicios_ebac/blob/main/Mod3_tabelas/query_3.csv.csv)
```sql
SELECT DISTINCT id_loja AS nome_loja
FROM transacoes;
```

### **3. Ordenando e limitando dados**

#### [**3.1. Query 4**](https://github.com/Lpresente/SQL_excercicios_ebac/blob/main/Mod3_tabelas/query_4.csv.csv)
```sql
SELECT id_cliente,
	valor
FROM transacoes
ORDER BY valor DESC
LIMIT 2;
```
