---
title: 快速入门： 连接和查询 SQL Server 使用 SQL 操作 Studio （预览版） |Microsoft 文档
description: 本快速入门演示如何使用 SQL 操作 Studio （预览版） 以连接到 SQL Server 并运行查询
ms.custom: tools|sos
ms.date: 03/08/2018
ms.prod: sql
ms.reviewer: alayu; erickang; sstein
ms.suite: sql
ms.prod_service: sql-tools
ms.component: sos
ms.tgt_pltfrm: ''
ms.topic: quickstart
author: yualan
ms.author: alayu
manager: craigg
ms.openlocfilehash: 287cd20b7db0a1b816211d48bc7a19c8f5066e8c
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="quickstart-connect-and-query-sql-server-using-includename-sosincludesname-sos-shortmd"></a>快速入门： 连接和查询 SQL Server 使用 [!INCLUDE[name-sos](../includes/name-sos-short.md)]
本快速入门演示如何使用[!INCLUDE[name-sos](../includes/name-sos-short.md)]连接到 SQL Server，然后使用 TRANSACT-SQL (T-SQL) 语句来创建*TutorialDB*中使用[!INCLUDE[name-sos](../includes/name-sos-short.md)]教程。

## <a name="prerequisites"></a>必要條件

若要完成本快速入门教程，你需要[!INCLUDE[name-sos](../includes/name-sos-short.md)]，并且有权访问 SQL Server。

- [安装[!INCLUDE[name-sos](../includes/name-sos-short.md)] ](download.md)。

如果你没有访问 SQL Server，从以下链接中选择你的平台 （请确保记住您的 SQL 登录名和密码 ！）：
- [Windows - 下载 SQL Server 2017 Developer Edition](https://www.microsoft.com/en-us/sql-server/sql-server-downloads)
- [macOS - 在 Docker 上下载 SQL Server 2017](https://docs.microsoft.com/en-us/sql/linux/quickstart-install-connect-docker)
- [Linux-下载 SQL Server 自 2017 年 Developer Edition](https://docs.microsoft.com/en-us/sql/linux/sql-server-linux-overview#install) -只需最多遵循步骤*创建和查询数据*。


## <a name="connect-to-a-sql-server"></a>连接到 SQL Server

   
1. 启动**[!INCLUDE[name-sos](../includes/name-sos-short.md)]**。
1. 首次运行*[!INCLUDE[name-sos](../includes/name-sos-short.md)]* **连接**对话框随即打开。 如果**连接**对话框不会打开，请单击**新连接**图标**服务器**页：
   
   ![新建连接图标](media/quickstart-sql-server/new-connection-icon.png)

1. 本文章将使用*SQL 登录名*，但*Windows 身份验证*支持。 如下所示填写字段：
 
    - **服务器名称：** localhost
    - **身份验证类型：** SQL 登录名  
    - **用户名：** SQL Server 的用户名称  
    - **密码：** SQL 服务器密码  
    - **数据库名称：**将此字段留空 
    - **服务器组：** \<默认\>  

   ![新的连接屏幕](media/quickstart-sql-server/new-connection-screen.png)



## <a name="create-a-database"></a>创建数据库

以下步骤创建一个名为**TutorialDB**:

1. 你的服务器，右键单击**localhost**，然后选择**新查询。**
1. 将以下代码段粘贴到查询窗口中： 

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

   ALTER DATABASE [TutorialDB] SET QUERY_STORE=ON
   GO
   ```
1. 若要执行查询时，请单击**运行**。

查询完成后，新**TutorialDB**将出现在数据库列表。 如果你未看到它，请右键单击**数据库**节点，然后选择**刷新**。


## <a name="create-a-table"></a>创建表

查询编辑器是否仍连接*master*数据库中，但我们想要创建的表中*TutorialDB*数据库。 

1. 将连接上下文更改为**TutorialDB**:

   ![更改上下文](media/quickstart-sql-server/change-context.png)



1. 将以下代码段粘贴到查询窗口并单击**运行**:

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

查询完成后，新**客户**表将显示在表的列表。 你可能需要右键单击**TutorialDB > 表**节点，然后选择**刷新**。

## <a name="insert-rows"></a>插入行

- 将以下代码段粘贴到查询窗口并单击**运行**:

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



## <a name="view-the-data-returned-by-a-query"></a>查看由查询返回的数据
1. 将以下代码段粘贴到查询窗口并单击**运行**:

   ```sql
   -- Select rows from table 'Customers'
   SELECT * FROM dbo.Customers;
   ```

1. 显示查询的结果：

   ![选择结果](media/quickstart-sql-server/select-results.png)


## <a name="next-steps"></a>后续步骤
现在，你已成功连接到 SQL 服务器，并运行查询，试用[代码编辑器教程](tutorial-sql-editor.md)。


