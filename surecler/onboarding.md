# Yeni Personel Kurulumu (Onboarding)

Ekibe yeni katılan bir geliştiricinin sistemlerimize erişebilmesi ve lokal ortamını hazırlayabilmesi için takip etmesi gereken adımlar.

## İlk Gün Hazırlıkları

1.  **Kurumsal Hesaplar**: Active Directory (AD) hesabı oluşturulması ve e-posta adresinin aktif edilmesi.
2.  **VPN Erişimi**: Şirket içi ağa bağlanmak için Cisco AnyConnect VPN istemcisinin kurulması ve 2FA (MFA) kaydı.
3.  **Haberleşme Kanalları**: Slack ve Jira/Confluence davetlerinin onaylanması.

## Geliştirici Ortamı Kurulumu

Lokalinizde projeleri çalıştırabilmek için aşağıdaki bağımlılıkları kurun:

*   **Docker**: Servisleri ayağa kaldırmak için en güncel Docker Desktop veya Docker Engine sürümü.
*   **Node.js**: LTS sürümü (v20 veya üzeri).
*   **Git**: Sürüm kontrol sistemi.

Lokal depoyu klonlayıp Docker ortamını başlatın:

```bash
git clone git@github.com:my-org/my-project.git
cd my-project
npm install
docker-compose up -d
```
