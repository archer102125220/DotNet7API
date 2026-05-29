# DotNet7API 部署教學

本文件提供將 **DotNet7API** 專案部署到生產環境 (Production) 的標準步驟與建議。

## 1. 準備發布檔案 (Publish)

在部署應用程式之前，我們需要先編譯並打包專案為可用於正式環境的版本。

請在專案目錄下執行以下指令：

```bash
dotnet publish -c Release -o ./publish
```

**參數說明**：
- `-c Release`：使用 Release 模式編譯，這個模式會對程式碼進行最佳化，確保最佳執行效能。
- `-o ./publish`：指定發布檔案的輸出目錄，編譯完成後的執行檔及相關依賴都會存放在這個資料夾中。

## 2. 環境變數與組態設定 (Configuration)

在生產環境中，請確保應用程式讀取正確的設定檔。

### `appsettings.json` 管理
- 預設的 `appsettings.json` 包含共用設定。
- 您可以建立或修改 `appsettings.Production.json`，在裡面設定生產環境專屬的配置 (例如：正式資料庫連線字串、外部 API 的正式金鑰等)。
- 請確保**不要**將敏感的密碼或金鑰直接寫在組態檔並提交至版控系統，建議透過伺服器的環境變數或 Secret Manager 來管理。

### 設定環境變數
在執行應用程式前，請確保伺服器上的 `ASPNETCORE_ENVIRONMENT` 變數設為 `Production`。
這會讓 ASP.NET Core 自動讀取 `appsettings.Production.json` 的配置。

* Linux/macOS 範例：
  ```bash
  export ASPNETCORE_ENVIRONMENT=Production
  ```
* Windows (PowerShell) 範例：
  ```powershell
  $env:ASPNETCORE_ENVIRONMENT="Production"
  ```

## 3. 執行應用程式

將 `./publish` 資料夾內的檔案複製到您的伺服器後，進入該目錄並透過 `dotnet` 指令執行應用程式：

```bash
cd /path/to/your/publish/folder
dotnet DotNet7API.dll
```

> **注意**：預設情況下，應用程式可能會綁定到 `http://localhost:5000`。您可以在執行時透過環境變數 (例如 `ASPNETCORE_URLS="http://localhost:8080"`) 或在組態檔中修改綁定的連接埠。

## 4. 常見的部署策略

根據您的基礎設施，可以選擇以下常見的部署方式：

### A. 使用 Docker (容器化)
若您的環境支援 Docker，您可以撰寫 `Dockerfile`，將 `.NET SDK` 用於編譯階段，並使用輕量級的 `.NET Runtime` 映像檔作為執行環境。這能確保應用程式在任何支援 Docker 的環境中都能一致地執行，也是目前最主流的部署方式。

### B. Windows Server (搭配 IIS)
在 Windows Server 上，.NET 應用程式最標準的部署方式是搭配 IIS (Internet Information Services)：
- 必須先在伺服器安裝 **.NET 7 Hosting Bundle** (包含 .NET Runtime 與 IIS 整合模組 ASP.NET Core Module)。
- 在 IIS 管理員中建立新的網站，並將實體路徑指向發布的 `./publish` 資料夾。
- 請務必將該網站的「應用程式集區 (Application Pool)」設定為「**無受控碼 (No Managed Code)**」，因為 ASP.NET Core 是獨立執行程序，IIS 僅作為反向代理伺服器。

### C. Linux (Nginx / Apache 搭配 Kestrel)
在 Linux 伺服器上，通常會將 ASP.NET Core 內建的 Kestrel 伺服器放在反向代理 (Reverse Proxy) 伺服器 (如 Nginx 或 Apache) 後面。
- Nginx 負責處理 HTTPS 憑證、靜態檔案及請求轉發。
- 建議使用 `systemd` 建立服務 (Service) 來管理您的應用程式，確保它在伺服器重開機時能自動啟動，或在意外崩潰時自動重啟。

### D. 雲端平台 (Azure App Service / AWS / GCP)
- **Azure App Service**：對於 .NET 應用程式具有最佳支援，可以透過 Visual Studio 直接發布，或設定 CI/CD Pipeline (如 GitHub Actions) 進行自動部署。
- **AWS / GCP**：可透過各大平台的容器服務 (ECS / Cloud Run) 部署 Docker 映像檔，或直接架設在虛擬機器 (EC2 / GCE) 上。
