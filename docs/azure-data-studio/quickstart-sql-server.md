---
title: 快速入门：连接并查询 SQL Server
titleSuffix: Azure Data Studio
description: 本快速入门介绍如何使用 Azure Data Studio 连接到 SQL Server 并运行查询
ms.prod: sql
ms.technology: azure-data-studio
ms.topic: quickstart
author: yualan
ms.author: alayu
ms.reviewer: alayu; sstein
ms.custom: seodec18, sqlfreshmay19
ms.date: 08/02/2019
ms.openlocfilehash: 7398d918a027b28513b3f12a5101628cf1158e49
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/01/2020
ms.locfileid: "75884052"
---
# <a name="quickstart-connect-and-query-sql-server-using-includename-sosincludesname-sos-shortmd"></a>快速入门：使用 [!INCLUDE[name-sos](../includes/name-sos-short.md)] 连接并查询 SQL Server

本快速入门介绍如何使用 [!INCLUDE[name-sos](../includes/name-sos-short.md)] 连接到 SQL Server，然后使用 Transact-SQL (T-SQL) 语句创建 [!INCLUDE[name-sos](../includes/name-sos-short.md)] 教程中使用的 TutorialDB  。

## <a name="prerequisites"></a>必备条件

要完成本快速入门，需要 [!INCLUDE[name-sos](../includes/name-sos-short.md)]，并访问 SQL Server。

- [安装 [!INCLUDE[name-sos](../includes/name-sos-short.md)]](download.md)。

如果没有 SQL Server 的访问权限，请从以下链接选择你的平台（请确保记住 SQL 登录名和密码！）：

- [Windows - 下载 SQL Server 2017 Developer Edition](https://www.microsoft.com/sql-server/sql-server-downloads)
- [macOS - 在 Docker 上下载 SQL Server 2017](https://docs.microsoft.com/sql/linux/quickstart-install-connect-docker)
- [Linux - 下载 SQL Server 2017 Developer 版本](https://docs.microsoft.com/sql/linux/sql-server-linux-overview#install) - 只需按照以下步骤操作即可创建和查询数据  。

## <a name="connect-to-a-sql-server"></a>连接到 SQL Server

1. 启动 [!INCLUDE[name-sos](../includes/name-sos-short.md)]  。

2. 首次运行 [!INCLUDE[name-sos](../includes/name-sos-short.md)] 时，应该会打开“欢迎”页  。 如果没有看到“欢迎”页，请选择“帮助” > “欢迎”    。 选择“新建连接”以打开“连接”窗格   ：

   ![“新建连接”图标](media/quickstart-sql-server/new-connection-icon.png)

3. 本文使用 SQL 登录名，但也支持 Windows 身份验证   。 按如下所示填写字段：

- **服务器名称：** 在此处输入服务器名。 例如，localhost。
- **身份验证类型:** SQL 登录名
- **用户名:** SQL Server 的用户名
- **密码:** SQL Server 的密码
- **数据库名称：** \<默认\>
- **服务器组:** \<默认\>

   ![新建连接屏幕](media/quickstart-sql-server/new-connection-screen.png)

## <a name="create-a-database"></a>创建数据库

以下步骤创建一个名为“TutorialDB”的数据库  ：

1. 右键单击服务器“localhost”，然后选择“新建查询”   。

2. 将以下代码片段粘贴到查询窗口，然后选择“运行”  。

 ```sql
 USE master
 GO
 IF NOT EXISTS (
  SELECT name
  FROM sys.databases
  WHERE name = N'TutorialDB'
 )
  CREATE DATABASE [TutorialDB];
 GO
 IF SERVERPROPERTY('ProductVersion') > '12'
  ALTER DATABASE [TutorialDB] SET QUERY_STORE=ON;
 GO
 ```

完成查询后，新的“TutorialDB”会显示在数据库列表中  。 如果未显示，请右键单击“数据库”节点，然后选择“刷新”   。

   ![创建数据库](media/quickstart-sql-server/create-database.png)

## <a name="create-a-table"></a>创建表

查询编辑器仍连接到 master 数据库，但需要在 TutorialDB 数据库中创建一个表   。

1. 将连接上下文更改为 TutorialDB  ：

   ![更改上下文](media/quickstart-sql-server/change-context.png)

2. 将以下代码片段粘贴到查询窗口，并单击“运行”  ：

   > [!NOTE]
   > 还可以在编辑器中追加此片段，或覆盖之前的查询。 请注意，单击“运行”仅执行选定的查询  。 如果未选择任何内容，单击“运行”将执行编辑器中所有的查询  。

 ```sql
 -- Create a new table called 'Customers' in schema 'dbo'
 -- Drop the table if it already exists
 IF OBJECT_ID('dbo.Customers', 'U') IS NOT NULL
  DROP TABLE dbo.Customers;
 GO
 -- Create the table in the specified schema
 CREATE TABLE dbo.Customers
 (
  CustomerId int NOT NULL PRIMARY KEY, -- primary key column
  Name nvarchar(50) NOT NULL,
  Location nvarchar(50) NOT NULL,
  Email nvarchar(50) NOT NULL
 );
 GO
 ```

完成查询后，新的“客户”表会显示在表列表中  。 可能需要右键单击“TutorialDB”>“表”节点，然后选择“刷新”   。

## <a name="insert-rows"></a>插入行

- 将以下代码片段粘贴到查询窗口，并单击“运行”  ：

 ```sql
 -- Insert rows into table 'Customers'
 INSERT INTO dbo.Customers
  ([CustomerId], [Name], [Location], [Email])
 VALUES
  ( 1, N'Orlando', N'Australia', N''),
  ( 2, N'Keith', N'India', N'keith0@adventure-works.com'),
  ( 3, N'Donna', N'Germany', N'donna0@adventure-works.com'),
  ( 4, N'Janet', N'United States', N'janet1@adventure-works.com')
 GO
 ```

## <a name="view-the-data-returned-by-a-query"></a>查看查询返回的数据

1. 将以下代码片段粘贴到查询窗口，并单击“运行”  ：

 ```sql
 -- Select rows from table 'Customers'
 SELECT * FROM dbo.Customers;
 ```

   ![选择结果](media/quickstart-sql-server/select-results.png)

## <a name="next-steps"></a>后续步骤

现在，已成功连接到 SQL Server 并运行查询，下面请尝试[代码编辑器教程](tutorial-sql-editor.md)。