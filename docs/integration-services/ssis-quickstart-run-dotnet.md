---
title: "使用.NET 代码 (C#) 中运行的 SSIS 项目 |Microsoft 文档"
ms.date: 09/25/2017
ms.topic: article
ms.prod: sql-server-2017
ms.technology:
- integration-services
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.translationtype: MT
ms.sourcegitcommit: 656e62f36446db4ef5b232129130a0253d2aebdf
ms.openlocfilehash: 65a8db27af80e5cd7001e9a8777dde3c59e9c55e
ms.contentlocale: zh-cn
ms.lasthandoff: 09/22/2017

---
# <a name="run-an-ssis-package-with-c-code-in-a-net-app"></a>使用 C# 代码在.NET 应用程序中运行 SSIS 包
此快速入门教程演示如何编写 C# 代码来连接到数据库服务器和运行 SSIS 包。

可以使用 Visual Studio、 Visual Studio 代码或你选择的另一种工具来创建 C# 应用程序。

## <a name="prerequisites"></a>先决条件

在开始之前，请确保你有 Visual Studio 或 Visual Studio Code 安装。 从下载免费的社区版的 Visual Studio 中或免费的 Visual Studio Code， [Visual Studio 下载](https://www.visualstudio.com/downloads/)。

> [!NOTE]
> Azure SQL 数据库服务器在端口 1433年上侦听。 如果你正在尝试连接到 Azure SQL 数据库服务器从企业防火墙内，此端口必须为你成功连接到企业防火墙中打开。

## <a name="get-the-connection-info-if-deployed-to-sql-database"></a>获取连接信息，如果部署到 SQL 数据库

如果您的包部署到 Azure SQL 数据库，获取你需要连接到 SSIS 目录数据库 (SSISDB) 的连接信息。 你需要遵循的过程中的完全限定的服务器名称和登录信息。

1. 登录到 [Azure 门户](https://portal.azure.com/)。
2. 选择**SQL 数据库**从左侧的菜单，然后单击的 SSISDB 数据库**SQL 数据库**页。 
3. 上**概述**为您的数据库页上，查看的完全限定的服务器名称。 弹出**单击此项可复制**选项，将鼠标悬停在的服务器名称。 
4. 如果你忘记了您的 Azure SQL 数据库服务器登录信息，导航到 SQL 数据库服务器页以查看服务器管理员名称。 如有必要，可以重置密码。
5. 单击**显示数据库连接字符串**。
6. 查看完整**ADO.NET**连接字符串。 示例代码使用`SqlConnectionStringBuilder`重新创建你提供的单个参数值与此连接字符串。

## <a name="create-a-new-visual-studio-project"></a>创建新的 Visual Studio 项目

1. 在 Visual Studio 中，选择**文件**，**新建**，**项目**。 
2. 在**新项目**对话框中，展开**Visual C#**。
3. 选择**控制台应用程序**并输入*run_ssis_project*项目名称。
4. 单击**确定**创建并在 Visual Studio 中打开新项目。

## <a name="add-references"></a>添加引用
1. 在解决方案资源管理器，右键单击**引用**文件夹，然后选择**添加引用**。 **引用管理器**对话框随即打开。
2. 在**引用管理器**对话框框中，展开**程序集**和选择**扩展**。
3. 选择要添加的以下两个引用：
    -   Microsoft.SqlServer.Management.Sdk.Sfc
    -   Microsoft.SqlServer.Smo
4. 单击**浏览**按钮以添加对的引用**Microsoft.SqlServer.Management.IntegrationServices**。 （此程序集是只会安装在全局程序集缓存 (GAC)。）**选择要引用的文件**对话框随即打开。
5. 在**选择要引用的文件**对话框框中，导航到包含的程序集的 GAC 文件夹。 此文件夹通常是`C:\Windows\assembly\GAC_MSIL\Microsoft.SqlServer.Management.IntegrationServices\14.0.0.0__89845dcd8080cc91`。
6. 在文件夹，然后单击中选择程序集 （即，.dll 文件）**添加**。
7. 单击**确定**关闭**引用管理器**对话框框中，并添加三个引用。 若要确保引用是否存在，请检查**引用**在解决方案资源管理器的列表。

## <a name="add-the-c-code"></a>添加 C# 代码 
1. 打开**Program.cs**。

2. 内容替换**Program.cs**替换为以下代码。 添加你的服务器、 数据库、 用户和密码的相应值。

> [!NOTE]
> 下面的示例使用 Windows 身份验证。 若要使用 SQL Server 身份验证，请替换`Integrated Security=SSPI;`参数与`User ID=<user name>;Password=<password>;`。


```csharp
using Microsoft.SqlServer.Management.IntegrationServices;
using System.Data.SqlClient;

namespace run_ssis_package
{
    class Program
    {
        static void Main(string[] args)
        {
            // Variables
            string targetServerName = "localhost";
            string folderName = "Project1Folder";
            string projectName = "Integration Services Project1";
            string packageName = "Package.dtsx";

            // Create a connection to the server
            string sqlConnectionString = "Data Source=" + targetServerName +
                ";Initial Catalog=master;Integrated Security=SSPI;";
            SqlConnection sqlConnection = new SqlConnection(sqlConnectionString);

            // Create the Integration Services object
            IntegrationServices integrationServices = new IntegrationServices(sqlConnection);

            // Get the Integration Services catalog
            Catalog catalog = integrationServices.Catalogs["SSISDB"];

            // Get the folder
            CatalogFolder folder = catalog.Folders[folderName];

            // Get the project
            ProjectInfo project = folder.Projects[projectName];

            // Get the package
            PackageInfo package = project.Packages[packageName];

            // Run the package
            package.Execute(false, null);

        }
    }
}
```

## <a name="run-the-code"></a>运行代码

1. 若要运行该应用程序，请按**F5**。
2. 验证按预期方式运行包，然后关闭应用程序窗口。

## <a name="next-steps"></a>后续步骤
- 考虑运行包的其他方式。
    - [使用 SSMS 中运行 SSIS 包](./ssis-quickstart-run-ssms.md)
    - [运行 SSIS 包使用 TRANSACT-SQL (SSMS)](./ssis-quickstart-run-tsql-ssms.md)
    - [使用 TRANSACT-SQL (VS Code) 运行 SSIS 包](ssis-quickstart-run-tsql-vscode.md)
    - [在命令提示符下运行 SSIS 包](./ssis-quickstart-run-cmdline.md)
    - [使用 PowerShell 运行 SSIS 包](ssis-quickstart-run-powershell.md)

