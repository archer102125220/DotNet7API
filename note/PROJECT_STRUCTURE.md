# DotNet7API 專案結構與設定檔說明

這份筆記詳細說明了 `DotNet7API` 專案中的資料夾結構以及各個核心設定檔的用途。這對於新加入專案或是進行日常維護都非常有幫助。

---

## 📁 專案根目錄 (Root Directory)

專案根目錄 (`/DotNet7API`) 包含了整個方案 (Solution) 層級的設定與相關文件。

- **`global.json`**
  - **用途**: 指定該專案（或方案）應使用的 .NET SDK 版本。
  - **說明**: 確保所有開發者以及 CI/CD 流程都在相同版本的 .NET SDK 下建置專案，避免因為 SDK 版本差異導致的非預期錯誤。

- **`DotNet7API.sln`**
  - **用途**: Visual Studio 方案檔 (Solution File)。
  - **說明**: 負責組織與管理一個或多個關聯的專案（例如主程式、測試專案等）。若使用 Visual Studio 或 Rider，開啟此檔案即可載入整個方案的結構。

- **`.gitignore`**
  - **用途**: Git 版本控制忽略清單。
  - **說明**: 設定哪些檔案或資料夾不該被推送到 Git 儲存庫。通常包含編譯產生的 `bin/` 與 `obj/` 資料夾，以及編輯器的暫存設定（如 `.vs/` 或 `.idea/`）。

- **`README.md` / `README_en.md`**
  - **用途**: 專案介紹文件。
  - **說明**: 記錄如何啟動專案、開發環境需求以及其他開發者需要知道的基本資訊。

---

## 📁 主要專案資料夾 (`/DotNet7API/DotNet7API/`)

這個資料夾是實際的 .NET 7 Web API 應用程式原始碼所在位置。

- **`Program.cs`**
  - **用途**: 應用程式的進入點 (Entry Point)。
  - **說明**: 在 .NET 6/7 中，此檔案結合了傳統的 `Program.cs` 和 `Startup.cs` 功能。負責設定依賴注入 (DI) 容器、中介軟體 (Middleware) 管線以及路由註冊。

- **`DotNet7API.csproj`**
  - **用途**: C# 專案檔 (Project File)。
  - **說明**: 以 XML 格式定義專案的目標框架 (Target Framework)、NuGet 套件參考以及其他建置設定。

- **`appsettings.json` 與 `appsettings.Development.json`**
  - **用途**: 應用程式設定檔。
  - **說明**: 用來儲存資料庫連線字串、日誌等級設定、API 金鑰等組態資訊。`Development.json` 會在開發環境中覆蓋主設定檔的對應值，避免將測試設定外洩至正式環境。

### 核心資料夾

- **`Controllers/`**
  - **用途**: 放置 API 控制器 (Controllers)。
  - **說明**: 負責接收 HTTP 請求 (Request)、呼叫相關業務邏輯，並回傳 HTTP 回應 (Response)。例如預設的 `WeatherForecastController.cs`。

- **`Properties/`**
  - **用途**: 存放專案屬性與啟動設定。
  - **重點檔案**: `launchSettings.json`。定義了在開發環境中執行或除錯應用程式的設定，包含啟動 URL（例如 `http://localhost:5000`）、環境變數 (`ASPNETCORE_ENVIRONMENT`) 等。

- **`bin/` 與 `obj/` (隱藏或被忽略的資料夾)**
  - **用途**: 編譯過程中的產出物。
  - **說明**: `obj/` 用於存放中繼檔案與編譯暫存，`bin/` 用於存放最終編譯出來的執行檔 (DLL, EXE)。這些資料夾不應加入版本控制。

---

## 🎯 總結

理解上述的結構與設定檔，有助於快速釐清 .NET 7 API 專案的運作脈絡。
- 若需要**新增 API 端點**，請前往 `Controllers/`。
- 若需要**修改連線字串**，請前往 `appsettings.json`。
- 若需要**加入中介軟體 (Middleware) 或 DI 注入**，請修改 `Program.cs`。
- 若需要**更新套件**，請透過 NuGet 指令或修改 `.csproj`。
