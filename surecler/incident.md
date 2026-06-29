# Hata Yonetimi (Incident Management)

Sistemde beklenmeyen bir kesinti, performans kaybı veya güvenlik ihlali durumunda izlenecek acil durum prosedürü.

## Acil Durum Seviyeleri

| Seviye | Tanım | Aksiyon Süresi |
| :--- | :--- | :--- |
| **P1** | Sistem tamamen kapalı, tüm kullanıcılar etkileniyor | Derhal müdahale (15 dk içinde) |
| **P2** | Kritik bir servis çalışmıyor, kullanıcıların bir kısmı etkileniyor | 1 saat içinde müdahale |
| **P3** | Minör hata, alternatif geçici çözümler mevcut | 24 saat içinde çözüm |

## Adım Adım Müdahale Süreci

1.  **Tespit ve Alarm**: Datadog veya Sentry üzerinden gelen P1/P2 alarmları nöbetçi mühendise (on-call) ulaşır.
2.  **İletişim Kanalı**: Slack üzerinde anlık bir `#incident-YYYY-MM-DD` kanalı açılır. Tüm paydaşlar buraya davet edilir.
3.  **Hata Giderme (Mitigation)**:
    *   Eğer son sürüm dağıtımı sonrası olduysa **Rollback** işlemi yapılır.
    *   Veritabanı yükü yüksekse geçici olarak ek okuyucu (replica) sunucular devreye alınır.
4.  **Kök Neden Analizi (Post-Mortem)**: Hata çözüldükten sonra 48 saat içinde hatanın kök nedeni analiz edilerek bir rapor hazırlanır ve tekrarlanmaması için önlemler listelenir.
