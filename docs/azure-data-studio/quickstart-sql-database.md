---
title: 快速入门：连接和查询 Azure SQL 数据库
titleSuffix: Azure Data Studio
description: 本快速入门介绍如何使用 Azure Data Studio 来连接到 SQL 数据库并运行查询
ms.custom: seodec18, sqlfreshmay19
ms.date: 05/14/2019
ms.prod: sql
ms.technology: azure-data-studio
ms.reviewer: alayu; sstein
ms.topic: quickstart
author: yualan
ms.author: alayu
manager: craigg
ms.openlocfilehash: a961cd08baab13b87241492df4adef52d5846daf
ms.sourcegitcommit: 553ecea0427e4d2118ea1ee810f4a73275b40741
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/14/2019
ms.locfileid: "65620352"
---
# <a name="quickstart-use-includename-sosincludesname-sos-shortmd-to-connect-and-query-azure-sql-database"></a>快速入门：使用[!INCLUDE[name-sos](../includes/name-sos-short.md)]进行连接和查询 Azure SQL 数据库

在此快速入门中，您将使用[!INCLUDE[name-sos](../includes/name-sos-short.md)]连接到 Azure SQL 数据库服务器。 然后，将运行 TRANSACT-SQL (T-SQL) 语句来创建和查询中其他使用的 TutorialDB 数据库[!INCLUDE[name-sos](../includes/name-sos-short.md)]教程。

## <a name="prerequisites"></a>先决条件

若要完成本快速入门教程，需要[!INCLUDE[name-sos](../includes/name-sos-short.md)]，和 Azure SQL 数据库服务器。

- [安装 [!INCLUDE[name-sos](../includes/name-sos-short.md)]](download.md)

如果没有 Azure SQL 服务器，完成以下 Azure SQL 数据库快速入门之一。 请记住的完全限定的服务器名称和登录凭据的后续步骤：

- [创建数据库-门户](https://docs.microsoft.com/azure/sql-database/sql-database-get-started-portal)
- [创建数据库-CLI](https://docs.microsoft.com/azure/sql-database/sql-database-get-started-cli)
- [创建 DB-PowerShell](https://docs.microsoft.com/azure/sql-database/sql-database-get-started-powershell)


## <a name="connect-to-your-azure-sql-database-server"></a>连接到 Azure SQL 数据库服务器

使用[!INCLUDE[name-sos](../includes/name-sos-short.md)]建立到 Azure SQL 数据库服务器的连接。

1. 首次运行[!INCLUDE[name-sos](../includes/name-sos-short.md)]**欢迎**应打开页面。 如果没有看到**欢迎**页上，选择**帮助** > **欢迎**。 选择**新的连接**以打开**连接**窗格：
   
   ![新的连接图标](media/quickstart-sql-database/new-connection-icon.png)

2. 本文使用 SQL 登录，但还支持 Windows 身份验证。 填写以下字段用于 Azure SQL server 的服务器名称、 用户名和密码：

   | 设置       | 建议的值 | Description |
   | ------------ | ------------------ | ------------------------------------------------- | 
   | **服务器名称** | 完全限定的服务器名称 | 如下所示： **servername.database.windows.net**。 |
   | **身份验证** | SQL 登录名| 本教程使用 SQL 身份验证。 |
   | **用户名** | 服务器管理员帐户用户名 | 从用来创建服务器的帐户用户名。 |
   | **密码（SQL 登录名）** | 服务器管理员帐户密码 | 从用来创建服务器的帐户密码。 |
   | **是否保存密码？** |  是或否 | 选择**是**如果不想每次都输入密码。 |
   | **数据库名称** | *将保留为空* | 仅连接到这里的服务器。 |
   | **服务器组** | 选择<Default> | 可以将此字段设置为你创建的特定服务器组。 | 

   ![新的连接图标](media/quickstart-sql-database/new-connection-screen.png)  

3. 选择“连接”。

4. 如果你的服务器的防火墙规则允许 Azure Data Studio，若要连接，没有**创建新的防火墙规则**窗体将打开。 完成窗体以创建新的防火墙规则。 有关详细信息，请参阅[防火墙规则](https://docs.microsoft.com/azure/sql-database/sql-database-firewall-configure)。

   ![新的防火墙规则](media/quickstart-sql-database/firewall.png)  

在中打开你的服务器成功连接后，**服务器**侧栏。

## <a name="create-the-tutorial-database"></a>创建教程数据库

接下来的部分创建使用的 TutorialDB 数据库中其他[!INCLUDE[name-sos](../includes/name-sos-short.md)]教程。

1. 在 Azure SQL 服务器上右键单击**服务器**侧栏，然后选择**新查询**。

1. 将此 SQL 粘贴到查询编辑器。

   ```sql
   IF NOT EXISTS (
      SELECT name
      FROM sys.databases
      WHERE name = N'TutorialDB'
   )
   CREATE DATABASE [TutorialDB]
   GO

   ALTER DATABASE [TutorialDB] SET QUERY_STORE=ON
   GO
   ```

1. 从工具栏中，选择**运行**。 通知出现在**消息**窗格，其中显示查询进度。

## <a name="create-a-table"></a>创建表

查询编辑器连接到**主**数据库中，但我们想要创建的表中**TutorialDB**数据库。 

1. 连接到**TutorialDB**数据库。

   ![更改上下文](media/quickstart-sql-database/change-context2.png)



1. 创建`Customers`表。 

   使用此替换上一个查询在查询编辑器中的，然后选择**运行**。

   ```sql
   -- Create a new table called 'Customers' in schema 'dbo'
   -- Drop the table if it already exists
   IF OBJECT_ID('dbo.Customers', 'U') IS NOT NULL
   DROP TABLE dbo.Customers
   GO
   -- Create the table in the specified schema
   CREATE TABLE dbo.Customers
   (
      CustomerId        INT    NOT NULL   PRIMARY KEY, -- primary key column
      Name      [NVARCHAR](50)  NOT NULL,
      Location  [NVARCHAR](50)  NOT NULL,
      Email     [NVARCHAR](50)  NOT NULL
   );
   GO
   ```


## <a name="insert-rows-into-the-table"></a>向表中插入行

使用此替换上一个查询，然后选择**运行**。

   ```sql
   -- Insert rows into table 'Customers'
   INSERT INTO dbo.Customers
      ([CustomerId],[Name],[Location],[Email])
   VALUES
      ( 1, N'Orlando', N'Australia', N''),
      ( 2, N'Keith', N'India', N'keith0@adventure-works.com'),
      ( 3, N'Donna', N'Germany', N'donna0@adventure-works.com'),
      ( 4, N'Janet', N'United States', N'janet1@adventure-works.com')
   GO
   ```

## <a name="view-the-result"></a>查看结果

使用此替换上一个查询，然后选择**运行**。

   ```sql
   -- Select rows from table 'Customers'
   SELECT * FROM dbo.Customers;
   ```

显示查询结果：

   ![选择结果](media/quickstart-sql-database/select-results2.png)


## <a name="clean-up-resources"></a>清理资源

在此处创建的资源时生成更高版本的快速入门文章。 如果你打算通过这些文章，是确保不要删除这些资源。 否则，在 Azure 门户中，删除不再需要的资源。 有关详细信息，请参阅[清理资源](https://docs.microsoft.com/azure/sql-database/sql-database-get-started-portal#clean-up-resources)。

## <a name="next-steps"></a>后续步骤

现在，你已成功连接到 Azure SQL 数据库和运行查询，请尝试[代码编辑器教程](tutorial-sql-editor.md)。
