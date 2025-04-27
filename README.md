# Процесс развертывания приложения

```mermaid
%%{init: {'theme': 'neutral', 'themeVariables': { 'primaryColor': '#e0e0e0'}}}%%
flowchart TD
    A[["Git Commit/Push 
    (ветка develop)"]] --> B[GitHub Actions]
    B --> C1["1. Сборка (Build)
    - .NET 8 self-contained
    - PublishSingleFile=true"]
    B --> C2["2. Тестирование
    - Unit-тесты (если есть)"]
    B --> C3["3. Деплой (Deploy)
    - SCP: app.tar.gz → сервер
    - Распаковка в /home/deploy
    - Systemd: запуск сервиса"]
    C3 --> D[[Сервер]]
    D --> E["Проверка:
    - Порт 5251
    - GET /ping → 'pong'"]
    E --> F{Релиз успешен?}
    F -->|Да| G[["🚀 Версия в продакшене"]]
    F -->|Нет| H[["❌ Автооткат
    (systemctl restart)"]]

    style A fill:#2e7d32,color:white,stroke:#1b5e20
    style B fill:#1565c0,color:white
    style C1 fill:#ff8f00,color:black
    style C2 fill:#ff8f00,color:black
    style C3 fill:#ff8f00,color:black
    style D fill:#6a1b9a,color:white
    style E fill:#2e7d32,color:white
    style G fill:#388e3c,color:white
    style H fill:#c62828,color:white

    classDef tool fill:#546e7a,color:white,stroke:#37474f;
    class B,tool
```
**Используемые инструменты:**
- 🛠️ **GitHub Actions** - CI/CD пайплайн  
- 📦 **SCP** - копирование артефактов  
- 🔄 **Systemd** - управление сервисом  
- ⚡ **Self-contained .NET** - автономная сборка  

**Директории сервера:**
- `/home/deploy/publish` - основная папка приложения  
- `/etc/systemd/system/setools-dz.service` - конфиг сервиса  