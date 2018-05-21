---
title: 快速入门： 连接和查询 Azure SQL 数据库使用 SQL 操作 Studio （预览版） |Microsoft 文档
description: 本快速入门演示如何使用 SQL 操作 Studio （预览版） 来连接到 SQL 数据库和运行查询
ms.custom: tools|sos
ms.date: 03/08/2018
ms.prod: sql
ms.reviewer: alayu; sstein
ms.suite: sql
ms.prod_service: sql-tools
ms.component: sos
ms.tgt_pltfrm: ''
ms.topic: quickstart
author: yualan
ms.author: alayu
manager: craigg
ms.openlocfilehash: c72e6d5b8e3e2770300e6b890b076bf77617849b
ms.sourcegitcommit: 6fd8a193728abc0a00075f3e4766a7e2e2859139
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/17/2018
---
# <a name="quickstart-use-includename-sosincludesname-sos-shortmd-to-connect-and-query-azure-sql-database"></a>快速入门： 使用[!INCLUDE[name-sos](../includes/name-sos-short.md)]来连接和查询 Azure SQL 数据库

本快速入门演示如何使用*[!INCLUDE[name-sos](../includes/name-sos-short.md)]* 以连接到 Azure SQL 数据库，然后使用 TRANSACT-SQL (T-SQL) 语句来创建*TutorialDB*中使用[!INCLUDE[name-sos](../includes/name-sos-short.md)]教程。

## <a name="prerequisites"></a>必要條件

若要完成本快速入门教程，你需要[!INCLUDE[name-sos](../includes/name-sos-short.md)]，和 Azure SQL 服务器。

- [安装[!INCLUDE[name-sos](../includes/name-sos-short.md)] ](download.md)。

如果你还没有 Azure SQL 服务器，完成以下 （请记住服务器名称和登录凭据 ！） 的 Azure SQL 数据库快速入门之一：

- [创建数据库-门户](https://docs.microsoft.com/azure/sql-database/sql-database-get-started-portal)
- [创建数据库-CLI](https://docs.microsoft.com/azure/sql-database/sql-database-get-started-cli)
- [创建数据库-PowerShell](https://docs.microsoft.com/azure/sql-database/sql-database-get-started-powershell)


## <a name="connect-to-your-azure-sql-database-server"></a>连接到你的 Azure SQL 数据库服务器

使用[!INCLUDE[name-sos](../includes/name-sos-short.md)]来建立与 Azure SQL 数据库服务器的连接。

1. 首次运行[!INCLUDE[name-sos](../includes/name-sos-short.md)]**连接**应打开页。 如果看不到**连接**页上，单击**添加连接**，或**新连接**图标**服务器**侧栏：
   
   ![新建连接图标](media/quickstart-sql-database/new-connection-icon.png)

2. 本文章将使用*SQL 登录名*，但*Windows 身份验证*也支持。 填写字段，如下所示使用服务器名称、 用户名和密码*你*Azure SQL server:

   | 设置       | 建议的值 | Description |
   | ------------ | ------------------ | ------------------------------------------------- | 
   | **服务器名称** | 完全限定的服务器名称 | 该名称应类似如下内容： **servername.database.windows.net，则** |
   | **身份验证** | SQL 登录名| 在本教程中使用 SQL 身份验证。 |
   | **用户名** | 服务器管理员帐户 | 此帐户是在创建服务器时指定的帐户。 |
   | **密码（SQL 登录名）** | 服务器管理员帐户的密码 | 此密码是在创建服务器时指定的密码。 |
   | **是否保存密码？** | 是或否 | 如果你不想要每次都输入密码，请选择是。 |
   | **数据库名称** | *将保留为空* | 你想要连接到数据库的名称。 |
   | **服务器组** | 选择<Default> | 如果你创建服务器组，你可以设置为特定服务器组。 | 

   ![新建连接图标](media/quickstart-sql-database/new-connection-screen.png)  

3. 如果你的服务器不具有的防火墙规则允许 SQL 操作 Studio 若要连接，**创建新的防火墙规则**窗体将打开。 完成表单创建新的防火墙规则。 有关详细信息，请参阅[防火墙规则](https://docs.microsoft.com/azure/sql-database/sql-database-firewall-configure)。

   ![新的防火墙规则](media/quickstart-sql-database/firewall.png)  

4. 在成功连接你的服务器打开后*服务器*侧栏。

## <a name="create-the-tutorial-database"></a>创建教程数据库

下列各节创建*TutorialDB*数据库用于多种[!INCLUDE[name-sos](../includes/name-sos-short.md)]教程。

1. 右键单击服务器边栏中的 Azure SQL 服务器上，然后选择**新查询。**

1. 下面的代码段粘贴到查询编辑器，然后单击**运行**:

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



## <a name="create-a-table"></a>创建表

查询编辑器是否仍连接*master*数据库中，但我们想要创建的表中*TutorialDB*数据库。 

1. 将连接上下文更改为**TutorialDB**:

   ![更改上下文](media/quickstart-sql-database/change-context.png)



1. 下面的代码段粘贴到查询编辑器，然后单击**运行**:

   > [!NOTE]
   > 可以追加到，也可以覆盖在编辑器中前面的查询。 请注意，单击**运行**执行所选查询。 如果未选择任何内容，则单击**运行**在编辑器中执行的所有查询。

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


## <a name="insert-rows"></a>插入行

- 下面的代码段粘贴到查询编辑器，然后单击**运行**:

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
1. 下面的代码段粘贴到查询编辑器，然后单击**运行**:

   ```sql
   -- Select rows from table 'Customers'
   SELECT * FROM dbo.Customers;
   ```

1. 显示查询的结果：

   ![选择结果](media/quickstart-sql-database/select-results.png)


## <a name="clean-up-resources"></a>清理资源

在此集合中的其他文章相互依赖本快速入门教程。 如果你打算继续使用后续快速入门，请执行不清理在本快速入门教程中创建的资源。 如果你不打算继续，使用以下步骤来删除此快速入门，Azure 门户中创建的资源。
通过删除不再需要的资源组来清理资源。 有关详细信息，请参阅[清理资源](https://docs.microsoft.com/en-us/azure/sql-database/sql-database-get-started-portal#clean-up-resources)。

## <a name="next-steps"></a>后续步骤

现在，你已成功连接到 Azure SQL 数据库并运行查询时，试用[代码编辑器教程](tutorial-sql-editor.md)。
