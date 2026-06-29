# Migration Calistirici

CI/CD hattında (GitHub Actions veya GitLab CI) çalışan ve veritabanı şema güncellemelerini (migrations) otomatik uygulayan entegrasyon betiği.

## Kurulum ve Çalıştırma

Gereksinim: Projede Node.js ve Knex.js kurulu olmalıdır.

```bash
npm run db:migrate
```

## Entegrasyon Örneği (GitHub Actions)

```yaml
name: Database Migration

on:
  push:
    branches:
      - main

jobs:
  migrate:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v3
      - name: Setup Node
        uses: actions/setup-node@v3
        with:
          node-version: 18
      - run: npm ci
      - name: Run Migrations
        env:
          DATABASE_URL: ${{ secrets.PROD_DATABASE_URL }}
        run: npx knex migrate:latest
```
