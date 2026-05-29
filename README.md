# DotNet7API

這是一個主要用於**學習目的**的 .NET 7 Web API 專案。

本專案是透過 **Visual Studio 2022 for Mac** 建立的。

## 如何啟動專案

### 方法一：使用 Visual Studio 2022 for Mac (推薦)

由於專案是透過 Visual Studio 2022 for Mac 建立的，最直接的方式是使用 IDE 開啟：

1. 開啟 Visual Studio 2022 for Mac。
2. 點選「開啟或將焦點移至現有專案...」。
3. 導覽至本專案目錄，並選擇 `DotNet7API.sln` 方案檔。
4. 在 IDE 的頂部工具列，點選「執行 (Play)」按鈕，或是按下 `Cmd + Enter` 來建置並啟動專案。

### 方法二：使用 .NET CLI (終端機)

如果您偏好使用終端機或是命令列工具，可以使用 .NET CLI 來啟動專案。

1. 開啟您的終端機 (Terminal)。
2. 將路徑切換到專案層級的目錄 (包含 `.csproj` 檔案的目錄，通常是與方案檔同名的資料夾)：
   ```bash
   cd DotNet7API/DotNet7API
   ```
3. 執行以下指令啟動應用程式：
   ```bash
   dotnet run
   ```
   應用程式啟動後，終端機會顯示本機伺服器的監聽網址 (例如 `http://localhost:5000` 或 `https://localhost:5001`)。

### 測試 API

專案啟動後，如果是帶有 Swagger 的 Web API 範本，您可以打開瀏覽器並前往 `https://localhost:<port>/swagger` 來測試 API 端點。
