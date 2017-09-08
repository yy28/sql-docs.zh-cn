---
title: "导出访问清单 (AccessToSQL) |Microsoft 文档"
ms.prod: sql-non-specified
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.technology:
- sql-ssma
ms.tgt_pltfrm: 
ms.topic: article
applies_to:
- Azure SQL Database
- SQL Server
helpviewer_keywords:
- Access databases
- Access databases, exporting metadata
- exporting
- exporting Access metadata
- exporting, Access metadata
- exporting, querying exported metadata
- inventories of Access databases
- querying exported metadata
ms.assetid: 7e1941fb-3d14-4265-aff6-c77a4026d0ed
caps.latest.revision: 18
author: Shamikg
ms.author: Shamikg
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 55f91e6b5e83b3a317f74b71e591de7e08009413
ms.contentlocale: zh-cn
ms.lasthandoff: 08/02/2017

---
# <a name="exporting-an-access-inventory-accesstosql"></a>导出访问清单 (AccessToSQL)
如果有多个访问数据库，并且你不确定要将迁移到哪些[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]，您可以将导出的项目中的所有访问数据库的清单。 然后，你可以查看和查询的清单元数据，以确定哪些数据库和要迁移这些数据库中的对象。 此清单，它使你能够快速地查找诸如以下问题的答案：  
  
-   最大数据库有哪些？  
  
-   谁拥有的大多数数据库？  
  
-   哪些数据库是否包含相同的表？  
  
-   尚未在过去六个月中修改哪些数据库？  
  
-   哪些数据库包含隐私信息？  
  
在本主题末尾提供了用于回答以下问题的查询示例。  
  
## <a name="exported-metadata"></a>导出的元数据  
SSMA 导出有关访问数据库、 表、 列、 索引、 外键、 查询、 报表、 窗体、 宏和模块的元数据。 有关每个项的这些类别的元数据导出到一个单独的表中。 有关这些表的架构，请参阅[访问清单架构](http://msdn.microsoft.com/en-us/fdd3cff2-4d62-4395-8acf-71ea8f17f524)。  
  
## <a name="exporting-inventory-data"></a>导出清单数据  
若要导出访问清单，必须首先打开或创建一个 SSMA 项目，并将你想要分析的 Access 数据库。 将数据库添加到的 SSMA 项目后，将这些数据库有关的元数据导出到指定[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]数据库和架构。 如有必要，SSMA 创建表以存储元数据。 SSMA 然后将添加到在 Access 数据库有关的元数据[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]数据库。  
  
> [!NOTE]  
> Access 数据库可以拆分为多个文件： 包含表和包含查询、 窗体、 报表、 宏、 模块和快捷方式的前端数据库后端数据库。 如果你想要拆分将数据库迁移到[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]，将前端数据库添加到 SSMA。  
  
下面的说明介绍如何创建一个项目，将数据库添加到项目，连接到[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]，然后导出清单数据。  
  
**创建项目**  
  
1.  打开访问 SSMA。  
  
2.  在“文件”菜单中，选择“新建项目”。  
  
    此时将显示“新建项目”  对话框。  
  
3.  在**名称**框中，输入你的项目的名称。  
  
4.  在**位置**框中，输入或选择用于项目的文件夹。  
  
5.  在**迁移到**组合框中，选择你想要迁移，并依次的目标版本**确定**。  
  
有关创建项目的详细信息，请参阅[创建和管理项目](http://msdn.microsoft.com/en-us/f2d1f0b0-5394-4adb-b3f3-abd71eb68ca7)。  
  
**可以查找和添加数据库**  
  
1.  上**文件**菜单上，单击**查找数据库**。  
  
2.  在查找数据库向导中，输入驱动器、 文件路径或你想要搜索的 UNC 路径。 或者，单击**浏览**以选择的驱动器或网络文件夹。  
  
3.  单击**添加**若要将位置添加到列表框中。  
  
    重复前面的两个步骤以添加其他搜索位置。  
  
4.  （可选） 添加搜索条件来完善的返回的数据库列表。  
  
    > [!IMPORTANT]  
    > **文件名称的全部或部分**文本框中不支持通配符。  
  
5.  单击**扫描**。  
  
    将显示扫描页。 这将显示已发现的数据库和搜索进度。 若要停止搜索，请单击**停止**。  
  
6.  在选择文件页上，选择你想要添加到项目的每个数据库。  
  
    你可以使用**选择所有**和**清除所有**要选中或清除所有数据库的列表顶部的按钮。 你还可以按住 CTRL 键来选择多个行，或按住 SHIFT 键以选择范围的行。  
  
7.  单击“下一步” 。  
  
8.  在验证页上，单击**完成**。  
  
有关将数据库添加到项目的详细信息，请参阅[添加和删除访问数据库文件](http://msdn.microsoft.com/en-us/e944c740-4c8a-4bc1-b0ed-be57bc06dced)。  
  
**若要连接到 SQL Server**  
  
1.  上**文件**菜单上，选择**连接到 SQL Server**。  
  
2.  在连接对话框中，输入或选择的实例的名称[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]。  
  
    -   如果你要连接到本地计算机上的默认实例，则可以输入**localhost**或句点 (**。**)。  
  
    -   如果你要连接到另一台计算机上的默认实例，输入的计算机的名称。  
  
    -   如果你要连接到命名实例，输入计算机名称、 反斜杠和实例名称。 例如： MyServer\MyInstance。  
  
3.  在**数据库**框中，输入导出元数据的目标数据库的名称。  
  
4.  如果你的实例[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]配置为接受非默认端口上的连接，请输入端口号用于[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]中的连接**服务器端口**框。 对于默认实例[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]，默认端口号为 1433年。 对于命名实例，SSMA 尝试获取中的端口号[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]浏览器服务。  
  
5.  在**身份验证**下拉菜单中，选择要用于连接的身份验证类型。 若要使用当前的 Windows 帐户，请选择**Windows 身份验证**。 若要使用[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]登录名选择**SQL Server 身份验证**，然后提供用户名和密码。  
  
有关连接到[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]，请参阅[连接到 SQL Server &#40;AccessToSQL &#41;](../../ssma/access/connecting-to-sql-server-accesstosql.md).  
  
**若要导出清单信息**  
  
1.  在访问元数据资源管理器中，展开**访问元数据库**。  
  
2.  选中的复选框旁边**数据库**。  
  
    若要忽略的单个数据库或数据库对象，展开**数据库**文件夹，然后再清除数据库或数据库对象旁边的复选框。  
  
3.  右键单击**数据库**和选择**导出架构**。  
  
4.  在**选择导出的架构**对话框中，选择导出的元数据，目标架构，然后单击**确定**。  
  
导出元数据，每次 SSMA 将数据追加到清单。 不更新或删除了在清单中的现有数据。  
  
## <a name="querying-the-exported-metadata"></a>查询导出的元数据  
导出有关访问数据库的元数据后，你可以查询的元数据。 下面的说明介绍若要使用中的查询编辑器窗口[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull_md.md)]运行查询。  
  
**若要查询的元数据**  
  
1.  从**启动**菜单上，指向**所有程序**，指向**Microsoft [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 2005年**或**Microsoft [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 2008年**或**Microsoft [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 2012年**，然后单击**SQL Server Management Studio**。  
  
2.  在**连接到服务器**对话框中，验证设置，并依次**连接**。  
  
3.  在 Management Studio 工具栏上，单击**新查询**打开查询编辑器。  
  
4.  在查询编辑器窗口中，输入查询。 下面的部分中显示了一些示例。  
  
5.  按 F5 键以运行查询。  
  
## <a name="query-examples"></a>查询示例  
在运行任何以下查询之前，应运行使用*database_name*查询，以确保对包含导出的元数据的数据库运行查询。 例如，如果元数据导出到名为 MyAccessMetadata 的数据库中时，你将添加以下开头[!INCLUDE[tsql](../../includes/tsql_md.md)]代码：  
  
```  
USE MyAccessMetadata;  
GO  
```  
下面的示例均使用**dbo**架构。 如果你导出到另一个架构的元数据，请确保更改架构，当你运行这些查询。  
  
### <a name="what-tables-and-columns-are-in-these-databases"></a>这些数据库中哪些表和列？  
下面的查询联接中包含列、 表和数据库元数据的表，然后返回的所有数据库、 表和列，按列名称排序的名称：  
  
```  
SELECT DatabaseName, TableName, ColumnName   
FROM dbo.SSMA_Access_InventoryColumns C  
JOIN dbo.SSMA_Access_InventoryTables T  
ON C.TableId = T.TableId  
JOIN dbo.SSMA_Access_InventoryDatabases D  
ON T.DatabaseId = D.DatabaseId  
ORDER BY ColumnName;  
```  
  
### <a name="what-are-the-largest-databases"></a>最大数据库有哪些？  
以下查询返回在每个访问数据库中，按文件的大小排序的数据库名称、 文件大小和数量的表：  
  
```  
SELECT DatabaseName, FileSize, TablesCount  
FROM dbo.SSMA_Access_InventoryDatabases  
ORDER BY FileSize DESC;  
```  
  
### <a name="who-is-the-owner-of-most-of-the-databases"></a>大多数数据库的所有者是谁？  
以下查询返回的数据库名称和所有者按排序每个访问数据库的所有者。  
  
```  
SELECT DatabaseName, FileOwner  
FROM dbo.SSMA_Access_InventoryDatabases  
ORDER BY FileOwner;  
```  
  
### <a name="which-databases-contain-the-same-tables"></a>哪些数据库是否包含相同的表？  
以下查询使用子查询来查找的表，列表中多次出现的所有表名称，然后使用此列表的表来获取的数据库名称。 结果返回为数据库名称，然后选择表名，并按表名称进行排序。  
  
```  
SELECT DatabaseName, TableName   
FROM dbo.SSMA_Access_InventoryTables T  
JOIN dbo.SSMA_Access_InventoryDatabases D  
ON D.DatabaseId = T.DatabaseId  
WHERE TableName IN (  
SELECT TableName   
FROM dbo.SSMA_Access_InventoryTables  
GROUP BY TableName   
HAVING count(*)>1  
)  
ORDER BY TableName;  
```  
  
### <a name="which-databases-were-not-modified-in-the-last-six-months"></a>在过去六个月内未修改哪些数据库？  
以下查询获取当前日期，月份值获取六个月前，，然后返回使用大于六个月前的修改日期的数据库列表。  
  
```  
SELECT DatabaseName, DateModified  
FROM dbo.SSMA_Access_InventoryDatabases  
WHERE DATEDIFF(month, DateModified, GETDATE()) > 6  
ORDER BY DateModified;  
```  
  
### <a name="which-databases-contain-private-information"></a>哪些数据库包含隐私信息？  
Access 数据库可能包含敏感或私人信息。 你可能想要移动到这些数据库[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]以利用其安全功能。 如果你知道包含敏感数据的列具有特定名称，或包含特定的字符，可以使用查询来查找包含该信息的所有列。 例如，可以找到包含字符串的所有列"薪金"。  然后，查询返回的数据库名称、 表名称和列名称。  
  
```  
SELECT DatabaseName, TableName, ColumnName   
FROM dbo.SSMA_Access_InventoryColumns C  
JOIN dbo.SSMA_Access_InventoryTables T  
ON C.TableId = T.TableId  
JOIN dbo.SSMA_Access_InventoryDatabases D  
ON T.DatabaseId = D. DatabaseId  
WHERE ColumnName LIKE '%salary%';  
```  
如果不知道的列名称，您可以编写查询以返回所有列。 若要执行此操作，删除从先前查询的 WHERE 子句。  
  
## <a name="see-also"></a>另请参阅  
[为迁移准备的 Access 数据库](http://msdn.microsoft.com/en-us/9b80a9e0-08e7-4b4d-b5ec-cc998d3f5114)  
  

