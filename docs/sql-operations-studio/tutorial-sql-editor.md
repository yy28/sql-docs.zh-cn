---
title: 教程： 使用 SQL 操作 Studio （预览版） TRANSACT-SQL 编辑器创建数据库对象 |Microsoft 文档
description: 本教程演示简化使用 T-SQL 的 SQL 操作 Studio （预览版） 中的关键功能。
ms.custom: tools|sos
ms.date: 03/13/2018
ms.prod: sql
ms.reviewer: alayu; sstein
ms.suite: sql
ms.prod_service: sql-tools
ms.component: sos
ms.tgt_pltfrm: ''
ms.topic: tutorial
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 5ea03ea9ee0d45e15ec81dda9be95d38ad99c6d6
ms.sourcegitcommit: 6fd8a193728abc0a00075f3e4766a7e2e2859139
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/17/2018
---
# <a name="tutorial-use-the-transact-sql-editor-to-create-database-objects---includename-sosincludesname-sos-shortmd"></a>教程： 使用 TRANSACT-SQL 编辑器创建数据库对象的 [!INCLUDE[name-sos](../includes/name-sos-short.md)]

创建和运行查询，存储的过程、 脚本等将是数据库专业人员的核心任务。 本教程演示如何在 T-SQL 编辑器中创建数据库对象的主要功能。

在本教程中，你将学习如何使用[!INCLUDE[name-sos-short](../includes/name-sos-short.md)]到：
> [!div class="checklist"]
> * 搜索数据库对象
> * 编辑表数据 
> * 使用代码段快地编写 T-SQL
> * 查看数据库对象详细信息使用*查看定义*和*转到定义*


## <a name="prerequisites"></a>必要條件

本教程需要安装 SQL Server 或 Azure SQL 数据库*TutorialDB*。 若要创建*TutorialDB*数据库，请完成以下快速入门之一：

- [连接和查询 SQL Server 使用 [!INCLUDE[name-sos-short](../includes/name-sos-short.md)]](quickstart-sql-server.md)
- [连接和查询使用 Azure SQL 数据库 [!INCLUDE[name-sos-short](../includes/name-sos-short.md)]](quickstart-sql-database.md)


## <a name="quickly-locate-a-database-object-and-perform-a-common-task"></a>快速查找的数据库对象和执行一项常见任务

[!INCLUDE[name-sos-short](../includes/name-sos-short.md)] 提供搜索小组件可以快速找到数据库对象。 结果列表中的常见任务与所选对象，提供了上下文菜单如*编辑数据*表。

1. 打开服务器边栏 (**Ctrl + G**)，展开**数据库**，然后选择**TutorialDB**。 

1. 打开*TutorialDB 仪表板*通过右键单击**TutorialDB**并选择**管理**从上下文菜单：

   ![上下文菜单-管理](./media/tutorial-sql-editor/insight-open-dashboard.png)

1. 在仪表板中，右键单击**dbo。客户**（在搜索小组件），然后选择**编辑数据**。
   
   > [!TIP]
   > 对于包含许多对象的数据库，使用搜索小组件快速找到表、 视图、 你正在寻找的等。

   ![快速搜索小组件](./media/tutorial-sql-editor/quick-search-widget.png)

1. 编辑**电子邮件**第一行中，类型的列*orlando0@adventure-works.com*，按**Enter**以保存更改。

   ![编辑数据](./media/tutorial-sql-editor/edit-data.png)

## <a name="use-t-sql-snippets-to-create-stored-procedures"></a>使用 T-SQL 的代码段创建存储的过程

SQL Operations Studio 提供許多內建的 T-SQL 程式碼片段，可快速建立陳述式。


1. 打开一个新的查询编辑器按**Ctrl + N**。

2. 类型**sql**在编辑器中，向下箭头**sqlCreateStoredProcedure**，按*选项卡*密钥 (或*Enter*) 加载存储创建过程代码段。

   ![snippet-list](./media/tutorial-sql-editor/snippet-list.png)

3. 创建存储的过程代码段包含为快速编辑设置的两个字段*StoredProcedureName*和*SchemaName*。 选择*StoredProcedureName*，右键单击，并选择**更改所有匹配项**。 现在，键入*getCustomer*和全部*StoredProcedureName*条目更改为*getCustomer*。

   ![代码段](./media/tutorial-sql-editor/snippet.png)

5. 更改的所有匹配项*SchemaName*到*dbo*。 
6. 代码段包含占位符参数和需要更新的正文。 *执行*语句还包含占位符文本，因为它不知道过程将具有多少参数。 本教程中更新代码段因此它类似于以下代码：

    ```sql
    -- Create a new stored procedure called 'getCustomer' in schema 'dbo'
    -- Drop the stored procedure if it already exists
    IF EXISTS (
    SELECT *
    FROM INFORMATION_SCHEMA.ROUTINES
    WHERE SPECIFIC_SCHEMA = N'dbo'
    AND SPECIFIC_NAME = N'getCustomer'
    )
    DROP PROCEDURE dbo.getCustomer
    GO
    -- Create the stored procedure in the specified schema
    CREATE PROCEDURE dbo.getCustomer
    @ID int
    -- add more stored procedure parameters here
    AS
    -- body of the stored procedure
    SELECT  c.CustomerId, 
    c.Name, 
    c.Location, 
    c.Email
    FROM dbo.Customers c
    WHERE c.CustomerId = @ID
    FOR JSON PATH

    GO
    -- example to execute the stored procedure we just created
    EXECUTE dbo.getCustomer 1
    GO
    ```
    
5. 若要创建存储的过程，并为其提供测试运行，请按**F5**。

现在创建存储的过程，与**结果**窗格将显示在 JSON 中返回的客户。 若要查看已设置格式的 JSON，请单击返回的记录。 


## <a name="use-peek-definition"></a>使用查看定义 

SQL 操作 Studio 提供的功能，若要查看使用查看定义功能的对象定义。 本部分创建的第二个存储的过程，并使用查看定义查看表以快速创建存储过程的正文中有哪些列。

1. 通过按下打开新的编辑器**Ctrl + N**。 

2. 类型*sql*在编辑器中，向下箭头*sqlCreateStoredProcedure*，按*选项卡*密钥 (或*Enter*) 加载存储创建过程代码段。
3. 键入*setCustomer*为*StoredProcedureName*和*dbo*为*SchemaName*

3. 替换@param占位符替换为以下参数定义：

   ```sql
   @json_val nvarchar(max)
   ```

4. 存储过程的正文替换为以下代码：
   ```sql
   INSERT INTO dbo.Customers
   ```

5. 在*插入*行刚添加的右键单击**dbo。客户**和选择**查看定义**。

   ![查看定义](./media/tutorial-sql-editor/peek-definition.png)

6. 显示的表定义的以便你可以快速查看列包括在表中。 引用列列表以方便地完成你的存储过程的语句。 完成创建 INSERT 语句你以前添加来完成的存储过程的正文并关闭查看定义窗口：

   ```sql
   INSERT INTO dbo.Customers (CustomerId, Name, Location, Email)
       SELECT CustomerId, Name, Location, Email
       FROM OPENJSON (@json_val)
       WITH(   CustomerId int, 
               Name nvarchar(50), 
               Location nvarchar(50), 
               Email nvarchar(50)
    )
   ```
7. 刪除 （或註解）查詢底下的 *EXECUTE* 命令。
8. 整个语句应类似下面的代码：

   ```sql
   -- Create a new stored procedure called 'setCustomer' in schema 'dbo'
   -- Drop the stored procedure if it already exists
   IF EXISTS (
   SELECT *
       FROM INFORMATION_SCHEMA.ROUTINES
       WHERE SPECIFIC_SCHEMA = N'dbo'
       AND SPECIFIC_NAME = N'setCustomer'
   )
   DROP PROCEDURE dbo.setCustomer
   GO
   -- Create the stored procedure in the specified schema
   CREATE PROCEDURE dbo.setCustomer
       @json_val nvarchar(max) 
   AS
       -- body of the stored procedure
       INSERT INTO dbo.Customers (CustomerId, Name, Location, Email)
       SELECT CustomerId, Name, Location, Email
       FROM OPENJSON (@json_val)
       WITH(   CustomerId int, 
               Name nvarchar(50), 
               Location nvarchar(50), 
               Email nvarchar(50)
       )
   GO
   ```

8. 若要创建*setCustomer*存储过程中，按**F5**。

## <a name="use-save-query-results-as-json-to-test-the-setcustomer-stored-procedure"></a>使用将查询结果保存为 JSON 测试 setCustomer 存储过程

*SetCustomer*在上一节中创建的存储的过程需要 JSON 将数据传入*@json_val*参数。 本部分演示如何获取要传递到参数，以便你可以测试存储的过程的 JSON 格式正确位。

1. 在**服务器**边栏右键单击*dbo。客户*表，然后单击**选择前 1000年行**。

2. 在结果视图中选择的第一行，请确保选择整行 （单击最左边的列中的数字 1），然后选择**将另存为 JSON**。  
3. 将文件夹更改到的位置，你会记得以便你可以删除的文件更高版本 （对于示例桌面） 并单击**保存**。 JSON 格式的文件将打开。

   ![将另存为 JSON](./media/tutorial-sql-editor/save-as-json.png)

4. 选择编辑器中的 JSON 数据并将其复制。
5. 通过按下打开新的编辑器**Ctrl + N**。
6. 前面的步骤显示如何可以轻松地获取格式正确的数据，以完成到调用*setCustomer*过程。 你可以看到下面的代码使用新客户详细信息使用相同的 JSON 格式，因此，我们可以测试*setCustomer*过程。 语句包含语法来声明参数和运行新的 get 和 set 过程。 你可以粘贴复制的数据与前一节和对其进行编辑，因此它等同于以下示例中，或只需将以下语句粘贴到查询编辑器。

   ```sql
   -- example to execute the stored procedure we just created
   declare @json nvarchar(max) =
   N'[
       {
           "CustomerId": 5,
           "Name": "Lucy",
           "Location": "Canada",
           "Email": "lucy0@adventure-works.com"
       }
   ]'

   EXECUTE dbo.setCustomer @json_val = @json
   GO

   EXECUTE dbo.getCustomer @ID = 5
   ```

7. 通过按执行该脚本**F5**。 该脚本插入新客户，并以 JSON 格式返回新客户的信息。 单击要打开的格式化的视图的结果。

   ![测试结果](./media/tutorial-sql-editor/test-result.png)

## <a name="next-steps"></a>后续步骤
在本教程中，您学习了如何：
> [!div class="checklist"]
> * 快速搜索架构对象
> * 编辑表数据 
> * 编写使用代码段的 T-SQL 脚本
> * 了解有关使用查看定义的数据库对象详细信息，然后转到定义


若要了解如何启用**五个最慢的查询**小组件中，完成下一步教程：

> [!div class="nextstepaction"]
> [启用速度慢的查询示例见解小组件](tutorial-qds-sql-server.md)
