---
title: 使用 Visual Studio Code 的 mssql 扩展适用于 SQL Server
titleSuffix: SQL Server
description: 使用适用于 Visual Studio Code 的 mssql 扩展编辑和 Linux 上运行 SQL Server Transact SQL 脚本。
author: VanMSFT
ms.author: vanto
manager: jroth
ms.date: 12/18/2018
ms.topic: conceptual
ms.prod: sql
ms.technology: linux
ms.assetid: 9766ee75-32d3-4045-82a6-4c7968bdbaa6
ms.openlocfilehash: fcda7a310e7a9dc77ea9464dd82dbed7260b0b39
ms.sourcegitcommit: 93d1566b9fe0c092c9f0f8c84435b0eede07019f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/11/2019
ms.locfileid: "67833792"
---
# <a name="use-visual-studio-code-to-create-and-run-transact-sql-scripts"></a>使用 Visual Studio Code 创建和运行 TRANSACT-SQL 脚本

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

本文介绍如何使用**mssql**适用于 Visual Studio Code 开发 SQL Server 数据库扩展。 由于 Visual Studio Code 是跨平台，您可以使用**mssql** Linux、 macOS 和 Windows 上的扩展。

## <a name="install-and-start-visual-studio-code"></a>安装并启动 Visual Studio Code

Visual Studio Code 是支持扩展的跨平台的图形代码编辑器。

1. [下载并安装 Visual Studio Code](https://code.visualstudio.com/)在计算机上。

1. 启动 Visual Studio Code。

   >[!NOTE]
   >如果通过 xrdp 远程桌面会话连接时，Visual Studio Code 未启动，请参阅[不工作时使用 XRDP 连接在 Ubuntu 上的 VS Code](https://github.com/Microsoft/vscode/issues/3451)。

## <a name="install-the-mssql-extension"></a>安装 mssql 扩展

[适用于 Visual Studio Code 的 mssql 扩展](https://aka.ms/mssql-marketplace)可让你连接到 SQL Server，使用 TRANSACT-SQL (T-SQL) 查询并查看结果。

1. 在 Visual Studio Code 中，选择**视图** > **命令面板**，或按**Ctrl**+**Shift** +**P**，或按**F1**以打开**命令面板**。

1. 在中**命令面板**，选择**扩展：安装扩展**从下拉列表。 

1. 在中**扩展**窗格中，键入*mssql*。

1. 选择**SQL Server (mssql)** 扩展，并选择**安装**。

   ![安装 mssql 扩展](./media/sql-server-linux-develop-use-vscode/vscode-extension.png)

1. 安装完成后，选择**重新加载**启用扩展。

## <a name="create-or-open-a-sql-file"></a>创建或打开 SQL 文件

Mssql 扩展启用 mssql 命令和 T-SQL IntelliSense 在代码编辑器中将语言模式设置为时**SQL**。

1. 选择**文件** > **新文件**或按**Ctrl**+**N**。 默认情况下，visual Studio Code 打开新的纯文本文件。 

1. 选择**纯文本**上的较低的状态栏或按**Ctrl**+**K** > **M**，并选择**SQL**从语言下拉列表。 

   ![SQL 语言模式](./media/sql-server-linux-develop-use-vscode/vscode-language-mode.png)

   > [!NOTE]
   > 如果这是首次使用该扩展，该扩展将安装支持 SQL Server 工具。

如果打开现有的文件具有 *.sql*文件扩展名，将语言模式将自动设置为 SQL。  

## <a name="connect-to-sql-server"></a>连接到 SQL Server

请按照下列步骤创建连接配置文件和连接到 SQL Server。

1. 按**Ctrl**+**Shift**+**P**或**F1**打开**命令面板**. 

1. 类型*sql*以显示 mssql 命令或键入*sqlcon*，然后选择**MS SQL:连接**从下拉列表。

   ![mssql 命令](./media/sql-server-linux-develop-use-vscode/vscode-commands.png)

   >[!NOTE]
   >SQL 文件，如空的 SQL 文件创建时，必须具有焦点在代码编辑器中的才可以执行 mssql 命令。

1. 选择**MS SQL:管理连接配置文件**命令。

1. 然后选择**创建**为您的 SQL Server 中创建新的连接配置文件。

1. 按照提示指定为新的连接配置文件的属性。 指定每个值后，按**Enter**以继续。

   | 连接属性 | 描述 |
   |---|---|
   | **服务器名称或 ADO 连接字符串** | 指定 SQL Server 实例名称。 使用*localhost*连接到本地计算机上的 SQL Server 实例。 若要连接到远程 SQL Server，请输入目标 SQL Server 的名称或其 IP 地址。 若要连接到 SQL Server 容器，请指定容器的主机计算机的 IP 地址。 如果您需要指定端口，使用逗号分隔的名称。 例如，对于端口 1401年上侦听的服务器，输入`<servername or IP>,1401`。<br/><br/>或者，可以为您在本文中的数据库输入在 ADO 连接字符串。 |
   | **数据库名称**（可选） | 要使用的数据库。 若要连接到的默认数据库，不指定数据库名称。 |
   | **身份验证类型** | 请执行以下某**集成**或**SQL 登录名**。 |
   | **用户名** | 如果所选**SQL 登录名**，输入数据库服务器上具有访问权限的用户的名称。 |
   | **密码** | 输入指定用户的密码。 |
   | **保存密码** | 按**Enter**以选择**是**和保存密码。 选择**否**每次使用的连接配置文件时提示输入密码。 |
   | **配置文件名称**（可选） | 键入一个名称为连接配置文件，如*localhost 配置文件*。 |

   在输入所有值，并选择后**都 Enter**，Visual Studio Code 创建连接配置文件，并连接到 SQL Server。

   > [!TIP]
   > 如果连接失败，请尝试以诊断问题中的错误消息**输出**Visual Studio Code 中的面板。 若要打开**输出**面板中，选择**视图** > **输出**。 此外查看[连接故障排除建议](./sql-server-linux-troubleshooting-guide.md#connection)。

1. 验证您在较低的状态栏中的连接。

   ![连接状态](./media/sql-server-linux-develop-use-vscode/vscode-connection-status.png)

作为上一步骤的替代方法，您可以还创建和编辑连接配置文件中的用户设置文件 (*settings.json*)。 若要打开设置文件，请选择**文件** > **首选项** > **设置**。 有关详细信息，请参阅[管理连接配置文件](https://github.com/Microsoft/vscode-mssql/wiki/manage-connection-profiles)。

## <a name="create-a-sql-database"></a>创建 SQL 数据库

1. 在前面启动新的 SQL 文件中键入*sql*以显示可编辑的代码片段的列表。 

   ![SQL 代码段](./media/sql-server-linux-develop-use-vscode/vscode-sql-snippets.png)

1. 选择**sqlCreateDatabase**。

1. 在段中，键入`TutorialDB`替换 DatabaseName:

   ```sql
   -- Create a new database called 'TutorialDB'
   -- Connect to the 'master' database to run this snippet
   USE master
   GO
   IF NOT EXISTS (
      SELECT name
      FROM sys.databases
      WHERE name = N'TutorialDB'
   )
   CREATE DATABASE [TutorialDB]
   GO
   ```

1. 按**Ctrl**+**Shift**+**E**执行 Transact-SQL 命令。 在查询窗口中查看结果。

   ![创建数据库邮件](./media/sql-server-linux-develop-use-vscode/vscode-create-database-messages.png)

   > [!TIP]
   > 您可以自定义 mssql 命令的快捷键。 请参阅[自定义快捷键](https://github.com/Microsoft/vscode-mssql/wiki/customize-shortcuts)。

## <a name="create-a-table"></a>创建表

1. 删除代码编辑器窗口的内容。

1. 按**Ctrl**+**Shift**+**P**或**F1**打开**命令面板**. 

1. 类型*sql*以显示 mssql 命令或键入*sqluse*，然后选择**MS SQL:使用数据库**命令。

1. 选择新**TutorialDB**数据库。 

   ![使用数据库](./media/sql-server-linux-develop-use-vscode/vscode-use-database.png)

1. 在代码编辑器中，键入*sql*若要显示这些代码片段，请选择**sqlCreateTable**，然后按**Enter**。

1. 在段中，键入`Employees`表名称。

1. 按**选项卡**以转到下一个字段，然后键入`dbo`架构名称。

1. 将列定义为包含以下列：

   ```sql
   EmployeesId INT NOT NULL PRIMARY KEY,
   Name [NVARCHAR](50)  NOT NULL,
   Location [NVARCHAR](50)  NOT NULL
   ```

1. 按**Ctrl**+**Shift**+**E**创建表。

## <a name="insert-and-query"></a>插入和查询

1. 添加以下语句将四个行插入**员工**表。

   ```sql
   -- Insert rows into table 'Employees'
   INSERT INTO Employees
      ([EmployeesId],[Name],[Location])
   VALUES
      ( 1, N'Jared', N'Australia'),
      ( 2, N'Nikita', N'India'),
      ( 3, N'Tom', N'Germany'),
      ( 4, N'Jake', N'United States')
   GO
   -- Query the total count of employees
   SELECT COUNT(*) as EmployeeCount FROM dbo.Employees;
   -- Query all employee information
   SELECT e.EmployeesId, e.Name, e.Location 
   FROM dbo.Employees as e
   GO
   ```

   键入时，T-SQL IntelliSense 可帮助完成该语句：

   ![T-SQL 的 IntelliSense](./media/sql-server-linux-develop-use-vscode/vscode-intellisense.png)

   > [!TIP]
   > Mssql 扩展还提供了命令来帮助创建 INSERT 和 SELECT 语句。 上一示例中，不使用它们。

1. 按**Ctrl**+**Shift**+**E**执行命令。 两个结果集显示在**结果**窗口。 

   ![结果](./media/sql-server-linux-develop-use-vscode/vscode-result-grid.png)

## <a name="view-and-save-the-result"></a>查看并保存结果

1. 选择**视图** > **编辑器布局** > **翻转布局**以切换到垂直或水平拆分布局。

1. 选择**结果**并**消息**面板标头来折叠和展开面板。

   ![切换标头](./media/sql-server-linux-develop-use-vscode/vscode-toggle-messages-pannel.png)

   > [!TIP]
   > 可以自定义 mssql 扩展的默认行为。 请参阅[自定义扩展选项](https://github.com/Microsoft/vscode-mssql/wiki/customize-options)。

1. 选择要放大这些结果的第二个结果网格上的最大化网格图标。

   ![最大化网格](./media/sql-server-linux-develop-use-vscode/vscode-maximize-grid.png)

   > [!NOTE]
   > T-SQL 脚本生成两个或多个结果网格时，将显示最大化图标。

1. 通过右键单击网格中打开网格上下文菜单。 

   ![上下文菜单](./media/sql-server-linux-develop-use-vscode/vscode-grid-context-menu.png)

1. 选择**全**。

1. 再次打开网格上下文菜单，然后选择**另存为 JSON**保存到结果 *.json*文件。

1. 为 JSON 文件指定文件名。 

1. 验证 JSON 文件保存，并在 Visual Studio Code 中打开。

   ![将另存为 JSON](./media/sql-server-linux-develop-use-vscode/vscode-save-as-json.png)

如果需要保存和运行 SQL 脚本更高版本，为管理或更大的开发项目中，将使用脚本另存 *.sql*扩展。

## <a name="next-steps"></a>后续步骤

如果您熟悉 T-SQL，请参阅[教程：编写 TRANSACT-SQL 语句](https://docs.microsoft.com/sql/t-sql/tutorial-writing-transact-sql-statements)并[TRANSACT-SQL 参考 （数据库引擎）](https://docs.microsoft.com/sql/t-sql/language-reference)。

有关使用或提供 mssql 扩展的详细信息，请参阅[mssql 扩展项目 wiki](https://github.com/Microsoft/vscode-mssql/wiki)。

使用 Visual Studio Code 的详细信息，请参阅[Visual Studio Code 文档](https://code.visualstudio.com/docs)。