# DotNet7API

This is a .NET 7 Web API project primarily for **learning purposes**.

This project was created using **Visual Studio 2022 for Mac**.

## How to Start the Project

### Method 1: Using Visual Studio 2022 for Mac (Recommended)

Since the project was created with Visual Studio 2022 for Mac, the most straightforward way is to open it using the IDE:

1. Open Visual Studio 2022 for Mac.
2. Click on "Open a project or solution".
3. Navigate to this project's directory and select the `DotNet7API.sln` solution file.
4. On the top toolbar of the IDE, click the "Run (Play)" button, or press `Cmd + Enter` to build and start the project.

### Method 2: Using the .NET CLI (Terminal)

If you prefer using a terminal or command-line tools, you can use the .NET CLI to start the project.

1. Open your Terminal.
2. Navigate to the project-level directory (the directory containing the `.csproj` file, typically a folder with the same name as the solution):
   ```bash
   cd DotNet7API/DotNet7API
   ```
3. Run the following command to start the application:
   ```bash
   dotnet run
   ```
   Once the application starts, the terminal will display the local server's listening URL (e.g., `http://localhost:5000` or `https://localhost:5001`).

### Testing the API

After starting the project, if it's a Web API template with Swagger included, you can open your browser and navigate to `https://localhost:<port>/swagger` to test the API endpoints.
