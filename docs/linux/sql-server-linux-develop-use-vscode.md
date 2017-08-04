---
title: "SQL Server 使用的 Visual Studio Code mssql 扩展 |Microsoft 文档"
description: "本教程演示如何使用 VS Code 的 mssql 扩展。 此扩展，可编辑和运行在 VS Code 的 TRANSACT-SQL 脚本。"
author: erickangMSFT
ms.author: erickang
manager: jhubbard
ms.date: 03/17/2017
ms.topic: article
ms.prod: sql-linux
ms.technology: database-engine
ms.assetid: 9766ee75-32d3-4045-82a6-4c7968bdbaa6
ms.custom: H1Hack27Feb2017
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: a4b2f82ac904d58604b0c27d46624995878e8a35
ms.contentlocale: zh-cn
ms.lasthandoff: 08/02/2017

---
# <a name="use-visual-studio-code-to-create-and-run-transact-sql-scripts-for-sql-server"></a>使用 Visual Studio Code 创建和运行 SQL Server 的 TRANSACT-SQL 脚本

本主题演示如何使用**mssql** Visual Studio Code (VS Code) 要开发 SQL Server 数据库的扩展。

Visual Studio Code 是一款适用于 Linux、macOS 和 Windows 的图形代码编辑器，支持扩展。 [ **Mssql** VS Code 的扩展]使您能够连接到 SQL Server，使用 TRANSACT-SQL (T-SQL)，查询并查看结果。

## <a name="install-vs-code"></a>安装 VS Code
1. 如果尚未安装 VS Code 中，[下载并安装 VS Code]在您的计算机上。

2. 启动 VS Code。

## <a name="install-the-mssql-extension"></a>安装 mssql 扩展
以下步骤说明了如何安装 mssql 扩展。 

1. 按**CTRL + SHIFT + P** (或**F1**) 以打开在 VS Code 的命令控制板。 

2. 选择**安装扩展**和类型**mssql**。
   > [!TIP] 
   > 有关 macOS， **CMD**密钥相当于**CTRL** Linux 和 Windows 上的密钥。

2. 单击安装**mssql**。 
   
   <img src="./media/sql-server-linux-develop-use-vscode/vscode-extension.png" alt="Install the extension" style="width: 600px;"/>

3. **Mssql**扩展采用一分钟的时间安装。 请等待通知安装成功的提示。

   <img src="./media/sql-server-linux-develop-use-vscode/vscode-install-success-notification.png" alt="Installation success notification" style="width: 600px;"/>

   > [!NOTE]
   > 对于 macOS，则必须安装 OpenSSL。 这是 mssql 扩展使用 .Net Core 的先决条件。 请按照**安装必备**中的步骤[.Net 核心说明]。 也可在 macOS 终端运行以下命令。
   >
   >   ```bash
   >   brew update
   >   brew install openssl
   >   ln -s /usr/local/opt/openssl/lib/libcrypto.1.0.0.dylib /usr/local/lib/
   >   ln -s /usr/local/opt/openssl/lib/libssl.1.0.0.dylib /usr/local/lib/
   >   ```
   
   > [!NOTE]
   > 对于 Windows 8.1、 Windows Server 2012 或更低版本，你必须下载并安装[Windows 10 通用 C 运行时]。 下载并打开 zip 文件。 然后根据当前 OS 配置运行安装程序（.msu 文件）。

## <a name="create-or-open-a-sql-file"></a>创建或打开 SQL 文件

**Mssql**扩展使 mssql 命令和 T-SQL 的 intellisense 功能在编辑器中的语言模式设置为时**SQL**。

1. 按**CTRL + N**。 默认情况下，Visual Studio Code 将打开一个新的“纯文本”文件。 

2. 按**CTRL + K、 M**并更改到语言模式**SQL**。 

   <img src="./media/sql-server-linux-develop-use-vscode/vscode-language-mode.png" alt="SQL language mode" style="width: 500px;" />

3. 也可使用 .sql 文件扩展打开现有文件。 语言模式，则自动**SQL**扩展名为.sql 的文件。  

## <a name="connect-to-sql-server"></a>连接到 SQL Server

以下步骤演示了如何使用 VS Code 连接到 SQL Server。

1. 在 VS Code 中，按**CTRL + SHIFT + P** (或**F1**) 以打开命令控制板。

2. 类型**sql**以显示 mssql 命令。

   <img src="./media/sql-server-linux-develop-use-vscode/vscode-commands.png" alt="mssql commands" style="width: 500px;" />
   

3. 选择**MS SQL： 连接**命令。 你可以只需键入**sqlcon**按**ENTER**。

4. 选择**创建连接配置文件**。 这将为 SQL Server 实例创建连接配置文件。

5. 按照提示为新连接配置文件指定连接属性。 指定每个值后, 按**ENTER**以继续。 

   下表描述了连接配置文件的属性。

   | 设置 | Description |
   |-----|-----|
   | **服务器名称** | SQL Server 实例名称。 对于本教程中，使用**localhost**连接到您的计算机上的本地 SQL Server 实例。 如果要连接到远程 SQL Server，请输入目标 SQL Server 计算机的名称，或它的 IP 地址。 |
   | **[可选]数据库名称** | 要使用的数据库。 对于此教程的目的，不指定数据库和按**ENTER**以继续。 |
   | **用户名** | 输入拥有访问服务器上数据库权限的用户名。 对于本教程中，使用默认**SA** SQL Server 安装过程中创建的帐户。 |
   | **密码 （SQL 登录名）** | 输入指定用户的密码。 | 
   | **保存的密码？** | 类型**是**保存密码。 否则，请键入**否**，在每次使用时连接配置文件的密码会提示您。 |
   | **[可选]输入此配置文件的名称** | 连接配置文件名称。 例如，无法将该配置文件**localhost 配置文件**。 

   > [!Tip] 
   > 可在用户设置文件 (settings.json) 中创建和编辑连接配置文件。 通过选择打开设置文件**首选项**然后**用户设置**VS Code 菜单中。 有关更多详细信息，请参阅[管理连接配置文件]。

6. 按**ESC**键关闭通知你，该配置文件已创建并已连接的信息消息。

   > [!TIP]
   > 如果你获取连接失败，请首先尝试诊断中的错误消息从问题**输出**在 VS Code 的面板 (选择**输出**上**视图**菜单)。 然后查看[连接故障排除建议]。

7. 在状态栏中验证连接。

   <img src="./media/sql-server-linux-develop-use-vscode/vscode-connection-status.png" alt="Connection status" style="width: 500px;" />

## <a name="create-a-database"></a>创建数据库

1. 在编辑器中，键入**sql**弹出的可编辑的代码段的列表。 

   <img src="./media/sql-server-linux-develop-use-vscode/vscode-sql-snippets.png" alt="SQL snippets" style="width: 500px;" />

2. 选择**sqlCreateDatabase**。

3. 在代码段中，键入**TutorialDB**数据库名称。

   ```sql
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
   
4. 按**CTRL + SHIFT + E**执行 TRANSACT-SQL 命令。 在查询窗口中查看结果。

   <img src="./media/sql-server-linux-develop-use-vscode/vscode-create-database-messages.png" alt="create database messages" style="width: 500px;" />

   > [!TIP]
   > 可以自定义为 mssql 扩展命令绑定的快捷键。 请参阅[自定义快捷键]。

## <a name="create-a-table"></a>创建表

1. 删除编辑器窗口中的内容。

2. 按**F1**以显示命令控制板。

3. 类型**sql**中要显示的 SQL 命令或类型的命令调色板**sqluse**为**MS SQL:Use 数据库**命令。

4. 单击**MS SQL:Use 数据库**，然后选择**TutorialDB**数据库。 此操作会将上下文更改为上一节中创建的新数据库。

   <img src="./media/sql-server-linux-develop-use-vscode/vscode-use-database.png" alt="use database" style="width: 500px;" />

3. 在编辑器中，键入**sql**以显示这些代码段，然后选择**sqlCreateTable**按**输入**。

4. 在代码段中，键入**员工**为表名。

5. 按**选项卡**，然后键入**dbo**架构名称。

   > [!NOTE]
   > 添加片段之后，必须键入表名和架构名，而无效从 VS Code 编辑器中更改焦点。

6. 更改的列名称**Column1**到**名称**和**Column2**到**位置**。

   ```sql
   -- Create a new table called 'Employees' in schema 'dbo'
   -- Drop the table if it already exists
   IF OBJECT_ID('dbo.Employees', 'U') IS NOT NULL
   DROP TABLE dbo.Employees
   GO
   -- Create the table in the specified schema
   CREATE TABLE dbo.Employees
   (
      EmployeesId        INT    NOT NULL   PRIMARY KEY, -- primary key column
      Name      [NVARCHAR](50)  NOT NULL,
      Location   [NVARCHAR](50)  NOT NULL
   );
   GO
   ```

7. 按**CTRL + SHIFT + E**以创建的表。

## <a name="insert-and-query"></a>插入和查询

1. 添加以下语句插入到四个行**员工**表。 然后选择所有行。

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

   > [!TIP]
   > 键入时，可使用 T-SQL IntelliSense 协助。
   >   <img src="./media/sql-server-linux-develop-use-vscode/vscode-intellisense.png" alt="TSQL IntelliSense" style="width: 500px;" />

2. 按**CTRL + SHIFT + E**执行命令。 这两个结果集显示在**结果**窗口。 

   <img src="./media/sql-server-linux-develop-use-vscode/vscode-result-grid.png" alt="Results" style="width: 300px;" />

## <a name="view-and-save-the-result"></a>查看并保存结果

1. 上**视图**菜单上，选择**切换编辑器组布局**以切换到垂直或水平拆分布局。

   <img src="./media/sql-server-linux-develop-use-vscode/vscode-toggle-split.png" alt="Vertical split" style="width: 500px;" />

2. 单击**结果**和**消息**面板标头以折叠和展开面板。

   <img src="./media/sql-server-linux-develop-use-vscode/vscode-toggle-messages-pannel.png" alt="Toggle Messages" style="width: 500px;" />

   > [!TIP]
   > 可以自定义 mssql 扩展的默认行为。 请参阅[自定义扩展选项]。

2. 单击第二个结果网格上的最大化网格图标放大网格。

   <img src="./media/sql-server-linux-develop-use-vscode/vscode-maximize-grid.png" alt="Maximize grid" style="width: 500px;" />

   > [!NOTE]
   > T-SQL 脚本具有两个或多个结果网格时，会显示最大化图标。

3. 使用网格上的鼠标右键打开网格上下文菜单。 

   <img src="./media/sql-server-linux-develop-use-vscode/vscode-grid-context-menu.png" alt="Context menu" style="width: 500px;" />

4. 选择**选择所有**。

5. 打开网格上下文菜单，然后选择**将另存为 JSON**将结果保存到的.json 文件。

6. 为 JSON 文件指定文件名。 对于本教程中，键入**employees.json**。

7. 验证 JSON 文件是否已保存，是否已在 VS Code 中打开。

   <img src="./media/sql-server-linux-develop-use-vscode/vscode-save-as-json.png" alt="Save as Json" style="width: 500px;" />

## <a name="next-steps"></a>后续步骤

在实际情况中，你可能会创建一个稍后要保存和运行的脚本（用于管理或作为大型开发项目的一部分）。 在这种情况下，你可以将使用脚本保存**.sql**扩展。

如果你不熟悉 T-SQL 的请参阅[教程： 编写 TRANSACT-SQL 语句]和[TRANSACT-SQL 参考 （数据库引擎）]。

使用或导致 mssql 扩展的详细信息，请参阅[mssql 扩展项目 wiki]。

使用 VS Code 的详细信息，请参阅[Visual Studio Code 文档](https://code.visualstudio.com/docs)。

[* * 有关 VS Code 扩展 mssql * *]:https://aka.ms/mssql-marketplace
[下载并安装 VS Code]:https://code.visualstudio.com/Download
[.Net 核心说明]:https://www.microsoft.com/net/core
[管理连接配置文件]:https://github.com/Microsoft/vscode-mssql/wiki/manage-connection-profiles
[连接故障排除建议]:./sql-server-linux-troubleshooting-guide.md#connection
[自定义快捷键]:https://github.com/Microsoft/vscode-mssql/wiki/customize-shortcuts
[教程： 编写 TRANSACT-SQL 语句]:https://msdn.microsoft.com/library/ms365303.aspx
[TRANSACT-SQL 参考 （数据库引擎）]:https://msdn.microsoft.com/library/bb510741.aspx
[Visual Studio Code documentation]:https://code.visualstudio.com/docs
[Windows 10 通用 C 运行时]:https://github.com/Microsoft/vscode-mssql/wiki/windows10-universal-c-runtime-requirement
[自定义扩展选项]: https://github.com/Microsoft/vscode-mssql/wiki/customize-options
[mssql 扩展项目 wiki]: https://github.com/Microsoft/vscode-mssql/wiki

