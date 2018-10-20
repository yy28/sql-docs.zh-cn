---
title: 教程： 使用 Azure 数据 Studio TRANSACT-SQL 编辑器来创建数据库对象 |Microsoft Docs
description: 本教程演示简化使用 T-SQL 在 Azure Data Studio 中的主要功能。
ms.custom: tools|sos
ms.date: 09/24/2018
ms.prod: sql
ms.technology: azure-data-studio
ms.reviewer: alayu; sstein
ms.topic: tutorial
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: c2a517b1efb6a86d70bd05f9a1418792c0b61098
ms.sourcegitcommit: 35e4c71bfbf2c330a9688f95de784ce9ca5d7547
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/16/2018
ms.locfileid: "49355928"
---
# <a name="tutorial-use-the-transact-sql-editor-to-create-database-objects---includename-sosincludesname-sos-shortmd"></a>教程： 使用 TRANSACT-SQL 编辑器来创建数据库对象， [!INCLUDE[name-sos](../includes/name-sos-short.md)]

创建并运行查询，存储的过程、 脚本等是数据库专业人员的核心任务。 本教程演示如何在 T-SQL 编辑器中创建数据库对象的主要功能。

您可以在本教學課程中，了解如何使用 [!INCLUDE[name-sos-short](../includes/name-sos-short.md)] 來完成下列工作：
> [!div class="checklist"]
> * 搜索数据库对象
> * 编辑表数据 
> * 使用代码段快速编写 T-SQL
> * 使用查看数据库对象详细信息*速览定义*和*转到定义*


## <a name="prerequisites"></a>必要條件

本教程需要安装 SQL Server 或 Azure SQL 数据库*TutorialDB*。 若要创建*TutorialDB*数据库，请完成以下快速入门之一：

- [使用 SQL Server 连接和查询 [!INCLUDE[name-sos-short](../includes/name-sos-short.md)]](quickstart-sql-server.md)
- [Azure SQL 数据库使用连接和查询 [!INCLUDE[name-sos-short](../includes/name-sos-short.md)]](quickstart-sql-database.md)


## <a name="quickly-locate-a-database-object-and-perform-a-common-task"></a>快速找到数据库对象并执行常见任务

[!INCLUDE[name-sos-short](../includes/name-sos-short.md)] 提供了搜索小组件以快速查找数据库对象。 结果列表中与所选对象相关的常见任务提供了上下文菜单等*编辑数据*表。

1. 打开服务器侧栏 (**Ctrl + G**)，展开**数据库**，然后选择**TutorialDB**。 

1. 打开*TutorialDB 仪表板*通过右击**TutorialDB** ，然后选择**管理**从上下文菜单：

   ![上下文菜单-管理](./media/tutorial-sql-editor/insight-open-dashboard.png)

1. 在仪表板中，右键单击**dbo。客户**（在搜索小组件），然后选择**编辑数据**。
   
   > [!TIP]
   > 对于具有多个对象的数据库，使用搜索小组件来快速查找表、 视图、 你正在寻找的等。

   ![快速搜索小组件](./media/tutorial-sql-editor/quick-search-widget.png)

1. 编辑**电子邮件**列中的第一行，类型*orlando0@adventure-works.com*，然后按**Enter**以保存更改。

   ![编辑数据](./media/tutorial-sql-editor/edit-data.png)

## <a name="use-t-sql-snippets-to-create-stored-procedures"></a>使用 T-SQL 代码段创建存储的过程

[!INCLUDE[name-sos](../includes/name-sos-short.md)] 用于快速创建语句提供了许多内置的 T-SQL 代码片段。


1. 按打开新查询编辑器**Ctrl + N**。

2. 类型**sql**在编辑器中，向下箭头**sqlCreateStoredProcedure**，然后按*选项卡*密钥 (或*Enter*) 以加载创建存储过程代码段。

   ![snippet-list](./media/tutorial-sql-editor/snippet-list.png)

3. 创建存储的过程代码片段有两个字段设置以进行快速编辑*StoredProcedureName*并*SchemaName*。 选择*StoredProcedureName*，右键单击，然后选择**更改所有匹配项**。 现在，键入*getCustomer*和全部*StoredProcedureName*条目更改为*getCustomer*。

   ![代码片段](./media/tutorial-sql-editor/snippet.png)

5. 更改所有匹配项*SchemaName*到*dbo*。 
6. 代码段中包含占位符参数和需要更新的正文文本。 *EXECUTE*语句还包含占位符文本，因为它不知道该过程将具有的参数的数目。 对于本教程中更新该代码段因此看起来如以下代码：

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
    
5. 若要创建存储的过程并对其进行测试运行，按**F5**。

现已创建存储的过程，并**结果**窗格将显示在 JSON 中返回的客户。 若要查看格式化的 JSON，请单击返回的记录。 


## <a name="use-peek-definition"></a>使用查看定义 

[!INCLUDE[name-sos](../includes/name-sos-short.md)] 提供的功能，若要查看使用窥视定义功能的对象定义。 本部分中创建第二个存储的过程，并使用查看定义查看一个表以快速创建存储过程的正文中包括的列。

1. 按打开的新编辑器**Ctrl + N**。 

2. 类型*sql*在编辑器中，向下箭头*sqlCreateStoredProcedure*，然后按*选项卡*密钥 (或*Enter*) 以加载创建存储过程代码段。
3. 在键入*setCustomer*有关*StoredProcedureName*并*dbo*为*SchemaName*

3. 替换为@param占位符替换以下参数定义：

   ```sql
   @json_val nvarchar(max)
   ```

4. 存储过程的主体替换为以下代码：
   ```sql
   INSERT INTO dbo.Customers
   ```

5. 在中*插入*行只是添加了，右键单击**dbo。客户**，然后选择**查看定义**。

   ![查看定义](./media/tutorial-sql-editor/peek-definition.png)

6. 表定义会显示您可以快速查看表中包括的列。 请参阅要轻松地填写你的存储过程的语句的列列表。 完成创建您以前添加来完成的存储过程的正文并关闭速览定义窗口的 INSERT 语句：

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
8. 整个语句应如以下代码所示：

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

## <a name="use-save-query-results-as-json-to-test-the-setcustomer-stored-procedure"></a>使用将查询结果保存为 JSON，以便测试 setCustomer 存储过程

*SetCustomer*在上一节中创建的存储的过程需要 JSON 数据传递到*@json_val*参数。 本部分演示如何获取少量格式正确的 JSON 传递到参数，以便可以测试存储的过程。

1. 在中**服务器**右键单击侧栏*dbo。客户*表，然后单击**选择前 1000年行**。

2. 在结果视图中选择的第一行，请确保选择整行 （单击最左边的列中的数字 1），然后选择**另存为 JSON**。  
3. 将文件夹更改为你会记得以便可以删除的文件更高版本 （对于示例桌面版） 并单击的位置**保存**。 JSON 格式设置文件随即打开。

   ![将另存为 JSON](./media/tutorial-sql-editor/save-as-json.png)

4. 在编辑器中选择的 JSON 数据并将其复制。
5. 按打开的新编辑器**Ctrl + N**。
6. 上一步骤演示了如何轻松地获取格式正确的数据，以完成对调用*setCustomer*过程。 您可以看到下面的代码与新客户详细信息使用相同的 JSON 格式，因此我们可以测试*setCustomer*过程。 语句包含语法来声明参数和运行新的 get 和 set 过程。 可以粘贴前一部分中复制的数据并对其进行编辑，因此，以下示例中，与相同或只需将以下语句粘贴到查询编辑器。

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

7. 执行该脚本通过按**F5**。 该脚本插入新客户，并以 JSON 格式返回新客户的信息。 单击要打开格式化的视图的结果。

   ![测试结果](./media/tutorial-sql-editor/test-result.png)

## <a name="next-steps"></a>后续步骤
在本教程中，您学习了如何：
> [!div class="checklist"]
> * 快速搜索架构对象
> * 编辑表数据 
> * 编写使用代码段的 T-SQL 脚本
> * 了解如何使用查看定义的数据库对象详细信息，并转到定义


若要了解如何启用**五个最慢的查询**小组件中，完成下一教程：

> [!div class="nextstepaction"]
> [启用速度慢的查询示例见解小组件](tutorial-qds-sql-server.md)
