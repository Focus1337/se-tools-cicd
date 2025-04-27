# Процесс развертывания приложения

![diagram](https://github.com/user-attachments/assets/4de04c50-3edb-4057-9563-7cedf0de6f3c)

**Используемые инструменты:**
- 🛠️ **GitHub Actions** - CI/CD пайплайн
- 📦 **SCP** - копирование артефактов
- 🔄 **Systemd** - управление сервисом
- ⚡ **Self-contained .NET** - автономная сборка

**Директории сервера:**
- `/home/deploy/publish` - основная папка приложения
- `/etc/systemd/system/setools-dz.service` - конфиг сервиса  
