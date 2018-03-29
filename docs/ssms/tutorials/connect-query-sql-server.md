---
Title: 'Tutorial: Connect and Query SQL Server using SQL Server Management Studio'
description: 有关使用 SQL Server Management Studio 连接到 SQL Server 和运行基本 T-SQL 查询的教程。
keywords: SQL Server, SSMS, SQL Server Management Studio
author: MashaMSFT
ms.author: mathoma
ms.date: 03/13/2018
ms.topic: tutorial
ms.suite: sql
ms.prod_service: sql-tools
ms.reviewer: sstein
manager: craigg
ms.openlocfilehash: 6f4110a0ae1b4ca349cc9b990cc9a32f7d41764d
ms.sourcegitcommit: ccb05cb5a4cccaf7ffa9e85a4684fa583bab914e
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/22/2018
---
# <a name="tutorial-connect-and-query-sql-server-using-sql-server-management-studio"></a>教程：使用 SQL Server Management Studio 连接和查询 SQL Server
本教程将指导如何使用 SQL Server Management Studio (SSMS) 连接到 SQL Server 实例以及运行一些基本的 Transact-SQL (T-SQL) 命令。 本文演示如何执行以下操作：

> [!div class="checklist"]
> * [连接到 SQL Server](#connect-to-a-sql-server)
> * [新建数据库 (TutorialDB)](#create-a-database)
> * [在新数据库中创建表（“客户”）](#create-a-table)
> * [在新“客户”表中插入行](#insert-rows)
> * [查询“客户”表并查看结果](#view-query-results)
> * [使用查询窗口表验证连接属性](#verify-your-query-window-connection-properties)
> * [更改查询窗口连接到的服务器](#change-server-connection-within-query-window)


## <a name="prerequisites"></a>必备条件
若要完成本教程，需要 SQL Server Management Studio 以及针对 SQL Server 的访问权限。 

- 安装 [SQL Server Management Studio](https://docs.microsoft.com/en-us/sql/ssms/download-sql-server-management-studio-ssms)。

如果没有 SQL Server 的访问权限，请从以下链接选择你的平台（如果选择 SQL 身份验证，请确保记住 SQL 登录名和密码！）：
- [Windows - 下载 SQL Server 2017 Developer Edition](https://www.microsoft.com/en-us/sql-server/sql-server-downloads)
- [macOS - 在 Docker 上下载 SQL Server 2017](https://docs.microsoft.com/en-us/sql/linux/quickstart-install-connect-docker)


## <a name="connect-to-a-sql-server"></a>连接到 SQL Server

1. 启动 SQL Server Management Studio (SSMS)。
1. 首次运行 SSMS 时，系统将打开“连接到服务器”对话框。 
      - 如果“连接到服务器”对话框未打开，则可在“对象资源管理器” > “连接”（或它旁边的图标）>“数据库引擎”中手动打开。

        ![在对象资源管理器中连接](media/connect-query-sql-server/connectobjexp.png)

1. 在“连接到服务器”对话框中，填写连接选项： 

    - **服务器类型**：数据库引擎（通常默认选择此选项）
    - **身份验证**：Windows 身份验证（本文使用 Windows 身份验证，但支持 SQL 登录，如果选择，系统将提示输入用户名/密码）

      ![连接](media/connect-query-sql-server/connection.png)

        还可以通过单击“选项”按钮修改其他连接选项（例如要连接的数据库、连接超时值和网络协议）。 对于本文，所有内容均保留默认值。 

1. 填写字段后，单击“连接”。 

1. 可通过浏览“对象资源管理器”中的对象，验证是否成功连接到 SQL Server： 

   ![成功的连接](media/connect-query-sql-server/successfulconnection.png)


## <a name="create-a-database"></a>创建数据库
以下步骤创建一个名为 TutorialDB 的数据库。 

1. 在“对象资源管理器”中右键单击服务器，选择“新建查询”：

   ![新建查询](media/connect-query-sql-server/newquery.png)
   
1. 将以下 T-SQL 代码片段粘贴到查询窗口： 
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
2. 若要执行查询，请单击“执行”（或在键盘上按 F5）。 

   ![执行查询](media/connect-query-sql-server/execute.png)
  
 
完成查询后，新的“TutorialDB”会显示在“对象资源管理器”内的数据库列表中。 如果未显示，请右键单击“数据库”节点，然后选择“刷新”。  


## <a name="create-a-table"></a>创建表
以下步骤将在新创建的“TutorialDB”数据库中创建一个表。 但是，查询编辑器仍处于 master 数据库上下文中，并且你想要在 TutorialDB 数据库中创建一个表。 

1. 通过从数据库下拉列表中选择所需数据库，将查询的连接上下文从 master 数据库更改到“TutorialDB”。 

   ![更改数据库](media/connect-query-sql-server/changedb.png)

1. 将以下 T-SQL 代码片段粘贴到查询窗口，突出显示该片段，并单击“执行”（或在键盘上按 F5）： 
    - 可在查询窗口中替换现有文本或将其追加到末尾。 若要在查询窗口中执行所有文本，请单击“执行”。 若要执行部分文本，请突出显示该部分，然后单击“执行”。  
  
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
完成查询后，新的“客户”表会显示在“对象资源管理器”内的表列表中。 如果未显示该表，请右键单击“对象资源管理器”中的“TutorialDB”>“表”节点并选择“刷新”。

## <a name="insert-rows"></a>插入行
以下步骤将在之前创建的“客户”表中插入一些行。 

将以下 T-SQL 代码片段粘贴到查询窗口并单击“执行”： 


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

## <a name="view-query-results"></a>查看查询结果
查询结果在查询文本窗口下可见。 通过以下步骤，可以查询“客户”表和查看以前插入的行。  

1. 将以下 T-SQL 代码片段粘贴到查询窗口并单击“执行”： 

   ```sql
   -- Select rows from table 'Customers'
   SELECT * FROM dbo.Customers;
   ```
1. 查询结果显示在输入文本的区域下： 

   ![查询结果](media/connect-query-sql-server/queryresults.png)


1.  可以通过选择以下选项之一来修改结果的显示方式：

     ![结果](media/connect-query-sql-server/results.png)

    - 默认情况下，结果将位于“网格视图”中，该视图为中间按钮并将结果显示在表中。 
    - 第一个按钮将在“文本视图”中显示结果，如下一部分中的图像所示。
    - 通过第三个按钮，可以将结果保存到默认以 *.rpt 结尾的文件中。

## <a name="verify-your-query-window-connection-properties"></a>验证查询窗口连接属性
在查询结果下，可以找到有关连接属性的信息。 
- 在运行前一步骤中的上述查询后，查看查询窗口底部的连接属性。
    - 可以确定连接到的服务器和数据库，以及登录所使用的用户。
    - 此外，还可以查看查询持续时间和之前执行的查询所返回的行数。
    
    ![连接属性](media/connect-query-sql-server/connectionproperties.png)  
    在此图像中，结果显示在“文本视图”中。  

## <a name="change-server-connection-within-query-window"></a>更改查询窗口中的服务器连接
通过执行以下步骤，可以更改当前查询窗口连接到的服务器。
1. 在查询窗口中单击右键 >“连接”>“更改连接”。
2. 这将再次打开“连接到服务器”对话框，从而允许更改查询连接到的服务器。 
 
   ![更改连接](media/connect-query-sql-server/changeconnection.png)
   - 请注意，这不会更改“对象资源管理器”连接到的服务器，只会更改当前查询窗口。 



