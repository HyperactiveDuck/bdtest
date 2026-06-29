# Log Temizleme Betigi

Sunuculardaki disk alanını optimize etmek amacıyla `/var/log` altındaki eski veya aşırı büyüyen günlük (log) dosyalarını güvenli bir şekilde temizleyen/arşivleyen yardımcı betik.

## Kullanım

Root yetkisiyle veya cron job ile her gece çalıştırılması tavsiye edilir.

```bash
sudo ./cleanup.sh
```

## Betik İçeriği

```bash
#!/bin/bash
# cleanup.sh - Disk Log Temizleme

LOG_DIR="/var/log/my-app"
MAX_SIZE="500M"

echo "Log temizleme işlemi başlatıldı..."

if [ -d "$LOG_DIR" ]; then
  # 14 günden eski .log dosyalarını sıkıştır
  find "$LOG_DIR" -name "*.log" -mtime +14 -exec gzip {} \;
  
  # 30 günden eski arşivlenmiş (.gz) logları sil
  find "$LOG_DIR" -name "*.gz" -mtime +30 -delete
  
  echo "Temizlik tamamlandı."
else
  echo "Log dizini bulunamadı: $LOG_DIR"
fi
```
