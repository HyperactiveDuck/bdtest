# Veritabani Performans Analizi

Bu betik, PostgreSQL `pg_stat_statements` görünümünü sorgulayarak en çok kaynak tüketen (CPU, bellek, disk okuma) ve yavaş çalışan ilk 10 SQL sorgusunu raporlar.

## Gereksinimler

Veritabanında `pg_stat_statements` eklentisinin aktif olması gerekir:

```sql
CREATE EXTENSION IF NOT EXISTS pg_stat_statements;
```

## Analiz Sorgusu

```sql
SELECT 
  query AS "Sorgu", 
  calls AS "Çağrı Adedi", 
  round(total_exec_time::numeric, 2) AS "Toplam Süre (ms)", 
  round(mean_exec_time::numeric, 2) AS "Ortalama Süre (ms)",
  round((100 * total_exec_time / sum(total_exec_time) OVER ())::numeric, 2) AS "Yük Yüzdesi (%)"
FROM pg_stat_statements
ORDER BY total_exec_time DESC
LIMIT 10;
```
