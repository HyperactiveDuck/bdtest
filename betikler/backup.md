# Yedekleme Betigi

Bu betik, sunucu üzerindeki PostgreSQL veritabanını ve belirli dosya dizinlerini yedekleyip AWS S3 veya harici bir sunucuya yükler.

## Kullanım

Betik parametre almadan çalıştırılabilir. Ayarlar `.env` dosyasından okunur.

```bash
./backup.sh
```

## Betik İçeriği

```bash
#!/bin/bash
# backup.sh - Otomatik Veritabanı ve Dosya Yedekleyici

DB_NAME="production_db"
BACKUP_DIR="/var/backups/db"
DATE=$(date +%Y-%m-%d_%H%M%S)
FILENAME="${DB_NAME}_${DATE}.sql.gz"

echo "Yedekleme başlatılıyor: ${DB_NAME}..."

# Veritabanı dökümü al ve sıkıştır
pg_dump -h localhost -U postgres ${DB_NAME} | gzip > ${BACKUP_DIR}/${FILENAME}

if [ $? -eq 0 ]; then
  echo "Veritabanı yedeği alındı: ${BACKUP_DIR}/${FILENAME}"
  
  # AWS S3'e yükle (isteğe bağlı)
  # aws s3 cp ${BACKUP_DIR}/${FILENAME} s3://my-app-backups-bucket/db/${FILENAME}
  
  # 7 günden eski yedekleri temizle
  find ${BACKUP_DIR} -type f -mtime +7 -name "*.sql.gz" -exec rm {} \;
  echo "Eski yedekler temizlendi."
else
  echo "Hata: Yedek alınamadı!" >&2
  exit 1
fi
```
