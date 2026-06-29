# Yedeklilik ve Felaket Senaryosu (Disaster Recovery)

Veri merkezinde oluşabilecek fiziksel kesintilerde veya büyük veri kayıplarında sistemin yedek bölgeden ayağa kaldırılması planıdır.

## Hedef Kriterler (RPO & RTO)

*   **RPO (Recovery Point Objective)**: Maksimum 1 saat (En fazla 1 saatlik veri kaybı tolere edilebilir).
*   **RTO (Recovery Time Objective)**: Maksimum 4 saat (Sistem en geç 4 saat içinde çalışır hale getirilmelidir).

## Kurtarma Adımları

1.  **Felaket İlanı**: Kesintinin 30 dakikayı aşacağı anlaşıldığında, CTO onayıyla DR planı resmi olarak başlatılır.
2.  **Yedek Sunucu Hazırlığı**: AWS Dublin (eu-west-1) birincil bölgemiz çöktüğünde AWS Frankfurt (eu-central-1) yedek bölgemizdeki CloudFormation şablonları çalıştırılır.
3.  **Veritabanı Geri Yükleme**: En son alınan S3 yedeği Frankfurt veritabanı kümesine restore edilir:
    ```bash
    pg_restore -h dr-db.internal -U postgres -d production_db latest_backup.dump
    ```
4.  **DNS Yönlendirme**: Cloudflare DNS ayarlarından trafik ana sunuculardan DR sunucularına yönlendirilir.
5.  **Test ve Doğrulama**: Temel kullanıcı giriş ve veri yazma testleri yapılarak sistem halka açılır.
