---
title: 使用 SQL Server Management Studio (SSMS) 连接和查询 SQL Server 实例
description: 有关使用 SQL Server Management Studio 连接到 SQL Server 实例和运行基本 T-SQL 查询的教程。
keywords: SQL Server, SSMS, SQL Server Management Studio
author: MashaMSFT
ms.author: mathoma
ms.reviewer: sstein
ms.topic: quickstart
ms.prod_service: sql-tools
ms.prod: sql
ms.technology: ssms
ms.custom: ''
ms.date: 03/13/2018
ms.openlocfilehash: eaf544085bfe6040bdf9f54300eb733ee4fd92f0
ms.sourcegitcommit: 8732161f26a93de3aa1fb13495e8a6a71519c155
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2019
ms.locfileid: "71708334"
---
# <a name="tutorial-connect-to-and-query-a-sql-server-instance-by-using-sql-server-management-studio-ssms"></a>教程：使用 SQL Server Management Studio (SSMS) 连接和查询 SQL Server 实例

本教程将指导如何使用 SQL Server Management Studio (SSMS) 连接到 SQL Server 实例以及运行一些基本的 Transact-SQL (T-SQL) 命令。 本文展示了如何按照以下步骤操作：

> [!div class="checklist"]
> * 连接到 SQL Server 实例
> * 创建数据库 ("TutorialDB")
> * 在新数据库中创建表（“客户”）
> * 在新表中插入行
> * 查询新表并查看结果
> * 使用查询窗口表验证连接属性
> * 更改查询窗口连接到的服务器

## <a name="prerequisites"></a>必备条件

若要完成本教程，需要 SQL Server Management Studio 以及针对 SQL Server 实例的访问权限。 

* 安装 [SQL Server Management Studio](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms)。

如果不能访问 SQL Server 实例，请从以下链接选择平台。 如果选择 SQL 身份验证，请使用 SQL Server 登录凭据。

*  Windows：[下载 SQL Server 2017 Developer Edition](https://www.microsoft.com/sql-server/sql-server-downloads)。
* **macOS**：[在 Docker 上下载 SQL Server 2017](https://docs.microsoft.com/sql/linux/quickstart-install-connect-docker)。

## <a name="connect-to-a-sql-server-instance"></a>连接到 SQL Server 实例

1. 启动 SQL Server Management Studio。 首次运行 SSMS 时，系统将打开“连接到服务器”窗口  。 如未打开，可以选择“对象资源管理器”   > “连接”   > “数据库引擎”  ，将其手动打开。

    ![对象资源管理器中的“连接”链接](media/connect-query-sql-server/connectobjexp.png)

2. 在“连接到服务器”窗口中，按照下表进行操作  ：

    * 对于“服务器类型”  ，选择“数据库引擎”  （通常的默认选项）。
    * 对于“服务器名称”，输入 SQL Server 实例的名称  。 （本文使用主机名 NODE5 [NODE5\SQL2016ST] 上的实例名称 SQL2016ST。）如果不知道如何确定 SQL Server 实例的名称，请参阅[使用 SSMS 的其他提示和技巧](ssms-tricks.md#determine-sql-server-name)。

    * 对于“身份验证”，选择“Windows 身份验证”   。 本文使用 Windows 身份验证，但也支持 SQL Server 登录。 如果选择“SQL 登录”  ，便会看到输入用户名和密码的提示。 有关身份验证类型的详细信息，请参阅[连接到服务器（数据库引擎）](https://docs.microsoft.com/sql/ssms/f1-help/connect-to-server-database-engine)。

    ![“服务器名称”字段与使用 SQL Server 实例的选项](media/connect-query-sql-server/connection2.png)

    也可以通过选择“选项”来修改其他连接选项  。 连接选项的示例包括你要连接到的数据库、连接超时值和网络协议。 本文对所有选项使用默认值。

3. 完成所有字段后，选择“连接”  。

### <a name="examples-of-successful-connections"></a>成功连接的示例

可通过展开和浏览“对象资源管理器”中的对象，验证 SQL Server 连接是否成功  。 这些对象因选择连接的服务器类型而异。 

* 连接到本地 SQL Server，示例中为 NODE5\SQL2016ST：![连接到本地服务器](media/connect-query-sql-server/connect-on-prem.png)

* 连接到 SQL Azure DB，示例中为 msftestserver.database.windows.net：![连接到 SQL Azure DB](media/connect-query-sql-server/connect-sql-azure.png)

  >[!NOTE]
  > 在本教程中，之前已使用 Windows 身份验证连接到本地 SQL Server，但此方法不支持连接到 SQL Azure DB  。 因此，此图像显示使用 SQL 身份验证连接到 SQL Azure DB。 有关详细信息，请参阅 [SQL 本地身份验证](../../relational-databases/security/choose-an-authentication-mode.md)和 [SQL Azure 身份验证](https://docs.microsoft.com/azure/sql-database/sql-database-security-overview#access-management)。 

## <a name="create-a-database"></a>创建数据库

按照以下步骤，创建一个名为 TutorialDB 的数据库：

1. 在“对象资源管理器”中右键单击服务器实例，然后选择“新建查询”  ：

   ![“新建查询”链接](media/connect-query-sql-server/newquery.png)

2. 将以下 T-SQL 代码片段粘贴到查询窗口： 

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

3. 若要执行查询，请选择“执行”（或选择键盘上的 F5）  。

   ![“执行”命令](media/connect-query-sql-server/execute.png)
  
    查询完成后，新的 TutorialDB 数据库会显示在“对象资源管理器”内的数据库列表中。 如未显示，请右键单击“数据库”节点，然后选择“刷新”   。  

## <a name="create-a-table-in-the-new-database"></a>在新数据库中创建表

本部分中将在新创建的 TutorialDB 数据库中创建一个表。 由于查询编辑器仍处于 master 数据库的上下文中，因此请按以下步骤操作，将连接上下文切换到 TutorialDB 数据库   ：

1. 在数据库下拉列表中，选择所需数据库，如下所示： 

   ![更改数据库](media/connect-query-sql-server/changedb.png)

2. 将以下 T-SQL 代码片段粘贴到查询窗口，选择它，再选择“执行”（或选择键盘上的 F5）。   
   可在查询窗口中替换现有文本或将其追加到末尾。 若要在查询窗口中执行所有文本，请选择“执行”  。 如果追加了文本，仅需执行部分文本，因此突出显示该部分，然后选择“执行”  。  
  
   ```sql
   USE [TutorialDB]
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

查询完成后，新的“客户”表会显示在对象资源管理器内的表列表中。 如果表未显示，请右键单击“对象资源管理器”中的“TutorialDB”   > “表”  节点，并选择“刷新”  。

## <a name="insert-rows-into-the-new-table"></a>将行插入新表

将一些行插入前面创建的“客户”表。 将以下 T-SQL 代码片段粘贴到查询窗口并选择“执行”来完成此操作  ：

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

## <a name="query-the-table-and-view-the-results"></a>查询表并查看结果

查询结果在查询文本窗口下可见。 要查询客户表和查看以前插入的行，请按照以下步骤操作：

1. 将以下 T-SQL 代码片段粘贴到查询窗口并选择“执行”  ：

   ```sql
   -- Select rows from table 'Customers'
   SELECT * FROM dbo.Customers;
   ```

    查询结果显示在输入文本的区域下： 

   ![“结果”列表](media/connect-query-sql-server/queryresults.png)

2. 可以通过选择以下选项之一来修改结果的显示方式：

     ![用于显示查询结果的三个选项](media/connect-query-sql-server/results.png)

    * 中间的按钮采用“网格视图”显示结果，这是默认选项  。 
    * 第一个按钮将在“文本视图”中显示结果，如下一部分中的图像所示  。
    * 第三个按钮可将结果保存为默认扩展名是 .rpt 的文件。

## <a name="verify-your-connection-properties-by-using-the-query-window-table"></a>使用查询窗口表验证连接属性

在查询结果下，可以找到有关连接属性的信息。 在运行前一步骤中的上述查询后，查看查询窗口底部的连接属性。

* 可以确定连接到的服务器和数据库，以及使用的用户名。
* 此外，还可以查看查询持续时间和之前执行的查询所返回的行数。

    ![连接属性](media/connect-query-sql-server/connectionproperties.png)

    > [!Note]
    > 在此图像中，结果显示在“文本视图”中  。

## <a name="change-the-server-based-on-the-query-window"></a>根据查询窗口更改服务器

通过执行以下步骤，可以更改当前查询窗口连接到的服务器：

1. 右键单击查询窗口，然后选择  “连接” >   “更改连接”。 “连接到服务器”  窗口将再次打开。

2. 更改查询使用的服务器。

   ![“更改连接”命令](media/connect-query-sql-server/changeconnection.png)

    > [!NOTE]
    > 此操作仅更改查询窗口连接到的服务器，而不更改对象资源管理器使用的服务器。

## <a name="next-steps"></a>后续步骤

熟悉 SSMS 的最好方式是进行实践演练。 这些文章可帮助你使用 SSMS 的各种功能。  这些文章教你如何管理 SSMS 组件，以及如何查找常用功能。

* [脚本](scripting-ssms.md)
* [在 SSMS 中使用模板](../template/templates-ssms.md)
* [SSMS 配置](ssms-configuration.md)
* [使用 SSMS 的其他提示和技巧](ssms-tricks.md)
