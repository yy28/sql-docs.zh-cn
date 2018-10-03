---
title: 快速入门： 连接和查询 Azure SQL 数据仓库使用 Azure Data Studio |Microsoft Docs
description: 本快速入门介绍如何使用 Azure Data Studio 来连接到 SQL 数据库并运行查询
ms.custom: tools|sos
ms.date: 09/24/2018
ms.prod: sql
ms.reviewer: alayu; sstein
ms.prod_service: sql-tools
ms.topic: quickstart
author: yualan
ms.author: alayu
manager: craigg
ms.openlocfilehash: fa71292e0b850f765f03f9f11c97d3b26c40a45f
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "48038020"
---
# <a name="quickstart-use-includename-sosincludesname-sos-shortmd-to-connect-and-query-data-in-azure-sql-data-warehouse"></a>快速入门： 使用[!INCLUDE[name-sos](../includes/name-sos-short.md)]进行连接和查询 Azure SQL 数据仓库中的数据

本快速入门演示如何使用[!INCLUDE[name-sos](../includes/name-sos-short.md)]连接到 Azure SQL 数据仓库，然后使用 TRANSACT-SQL 语句来创建、 插入和选择数据。 

## <a name="prerequisites"></a>必要條件
若要完成本快速入门教程，需要[!INCLUDE[name-sos](../includes/name-sos-short.md)]，和 Azure SQL 数据仓库。

- [安装[!INCLUDE[name-sos](../includes/name-sos-short.md)] ](download.md)。

如果还没有 SQL 数据仓库，请参阅[创建 SQL 数据仓库](https://docs.microsoft.com/azure/sql-data-warehouse/sql-data-warehouse-get-started-provision)。

请注意，服务器名称和登录凭据 ！


## <a name="connect-to-your-data-warehouse"></a>连接到数据仓库

使用[!INCLUDE[name-sos](../includes/name-sos-short.md)]来建立与 Azure SQL 数据仓库服务器的连接。

1. 首次运行[!INCLUDE[name-sos](../includes/name-sos-short.md)]**连接**应打开页面。 如果没有看到**连接**页上，单击**添加连接**，或**新连接**中的图标**服务器**边栏：
   
   ![新的连接图标](media/quickstart-sql-dw/new-connection-icon.png)

2. 本文使用*SQL 登录名*，但*Windows 身份验证*也受支持。 填写字段，如下所示使用服务器名称、 用户名和密码*你*Azure SQL 服务器：

   | 设置       | 建议的值 | Description |
   | ------------ | ------------------ | ------------------------------------------------- | 
   | **服务器名称** | 完全限定的服务器名称 | 名称应类似于此： **sqldwsample.database.windows.net** |
   | **身份验证** | SQL 登录名| 在本教程中使用 SQL 身份验证。 |
   | **用户名** | 服务器管理员帐户 | 此帐户是在创建服务器时指定的帐户。 |
   | **密码（SQL 登录名）** | 服务器管理员帐户的密码 | 此密码是在创建服务器时指定的密码。 |
   | **是否保存密码？** | 是或否 | 如果您不想要每次都输入密码，请选择是。 |
   | **数据库名称** | *将保留为空* | 要连接到的数据库的名称。 |
   | **服务器组** | 选择<Default> | 如果你创建服务器组，您可以设置为特定的服务器组。 | 

   ![新的连接图标](media/quickstart-sql-dw/new-connection-screen.png) 

3. 如果你的服务器的防火墙规则允许 Azure Data Studio，若要连接，没有**创建新的防火墙规则**窗体将打开。 完成窗体以创建新的防火墙规则。 有关详细信息，请参阅[防火墙规则](https://docs.microsoft.com/azure/sql-database/sql-database-firewall-configure)。

   ![新的防火墙规则](media/quickstart-sql-dw/firewall.png)  

4. 在将服务器连接成功打开后*服务器*侧栏。

## <a name="create-the-tutorial-data-warehouse"></a>创建教程数据仓库
1. 在服务器上，在对象资源管理器中右键单击并选择**新查询。**

1. 以下代码片段粘贴到查询编辑器，然后单击**运行**:

   ```sql
    IF NOT EXISTS (
       SELECT name
       FROM sys.databases
       WHERE name = N'TutorialDB'
    )
    CREATE DATABASE [TutorialDB] (EDITION = 'datawarehouse', SERVICE_OBJECTIVE='DW100');
    GO  
    
    ALTER DATABASE [TutorialDB] SET QUERY_STORE=ON
    GO
   ```


## <a name="create-a-table"></a>创建表

查询编辑器仍连接到*主*数据库中，但我们想要创建的表中*TutorialDB*数据库。 

1. 更改到的连接上下文**TutorialDB**:

   ![更改上下文](media/quickstart-sql-database/change-context.png)


1. 以下代码片段粘贴到查询编辑器，然后单击**运行**:

   > [!NOTE]
   > 可以将其追加或覆盖在编辑器中前面的查询。 请注意，单击**运行**执行所选查询。 如果未选择任何项，则单击**运行**执行所有查询编辑器中。

   ```sql
   -- Create a new table called 'Customers' in schema 'dbo'
   -- Drop the table if it already exists
   IF OBJECT_ID('dbo.Customers', 'U') IS NOT NULL
   DROP TABLE dbo.Customers
   GO
   -- Create the table in the specified schema
   CREATE TABLE dbo.Customers
   (
      CustomerId        INT     NOT NULL,
      Name      [NVARCHAR](50)  NOT NULL,
      Location  [NVARCHAR](50)  NOT NULL,
      Email     [NVARCHAR](50)  NOT NULL
   );
   GO
   ```


## <a name="insert-rows"></a>插入行

1. 以下代码片段粘贴到查询编辑器，然后单击**运行**:

   ```sql
   -- Insert rows into table 'Customers'
   INSERT INTO dbo.Customers
      ([CustomerId],[Name],[Location],[Email])
      SELECT 1, N'Orlando',N'Australia', N'' UNION ALL
      SELECT 2, N'Keith', N'India', N'keith0@adventure-works.com' UNION ALL
      SELECT 3, N'Donna', N'Germany', N'donna0@adventure-works.com' UNION ALL
      SELECT 4, N'Janet', N'United States', N'janet1@adventure-works.com'
   ```


## <a name="view-the-result"></a>查看结果
1. 以下代码片段粘贴到查询编辑器，然后单击**运行**:

   ```sql
   -- Select rows from table 'Customers'
   SELECT * FROM dbo.Customers;
   ```

1. 显示查询的结果：

   ![选择结果](media/quickstart-sql-dw/select-results.png)


## <a name="clean-up-resources"></a>清理资源

在本快速入门生成此集合中的其他文章。 如果你打算继续使用后续快速入门，请执行不清理在本快速入门教程中创建的资源。 如果不打算继续，请使用以下步骤删除本快速入门在 Azure 门户中创建的资源。
通过删除不再需要的资源组来清理资源。 有关详细信息，请参阅[清理资源](https://docs.microsoft.com/azure/sql-database/sql-database-get-started-portal#clean-up-resources)。


## <a name="next-steps"></a>后续步骤

现在，你已成功连接到 Azure SQL 数据仓库，并运行查询，尝试[代码编辑器教程](tutorial-sql-editor.md)。
