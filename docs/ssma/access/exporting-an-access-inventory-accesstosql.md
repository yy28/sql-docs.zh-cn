---
title: 导出 Access 清单 (AccessToSQL) |Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.technology: ssma
ms.tgt_pltfrm: ''
ms.topic: conceptual
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
manager: craigg
ms.openlocfilehash: 6256a21e699f3dbd6714da0e4778b9d00e8d940a
ms.sourcegitcommit: 79d4dc820767f7836720ce26a61097ba5a5f23f2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/16/2018
ms.locfileid: "40396037"
---
# <a name="exporting-an-access-inventory-accesstosql"></a>导出 Access 清单 (AccessToSQL)
如果有多个访问数据库，并且您不确定要迁移到哪些[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，可以将导出的项目中的所有访问数据库的清单。 然后，您可以查看和查询清单的元数据来确定哪些数据库和要迁移这些数据库中的对象。 此清单，它允许您快速查找常见问题的答案的问题，如下所示：  
  
-   最大数据库有哪些？  
  
-   谁拥有大部分数据库？  
  
-   哪些数据库是否包含相同的表？  
  
-   尚未在过去六个月中修改哪些数据库？  
  
-   哪些数据库包含私人信息？  
  
在本主题末尾提供了用于回答这些问题的查询示例。  
  
## <a name="exported-metadata"></a>导出的元数据  
SSMA 导出有关访问数据库、 表、 列、 索引、 外键、 查询、 报表、 窗体、 宏和模块的元数据。 有关每个项的类别的元数据导出到一个单独的表中。 有关这些表的架构，请参阅[Access 清单架构](access-inventory-schemas-accesstosql.md)。  
  
## <a name="exporting-inventory-data"></a>导出清单数据  
若要导出 Access 清单，您必须首次打开或创建 SSMA 项目，，然后添加你想要分析的 Access 数据库。 将数据库添加到 SSMA 项目后，将这些数据库有关的元数据导出到指定[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]数据库和架构。 如有必要，SSMA 创建表以存储的元数据。 SSMA 然后将添加到 Access 数据库有关的元数据[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]数据库。  
  
> [!NOTE]  
> Access 数据库可以拆分为多个文件： 包含表和包含查询、 窗体、 报表、 宏、 模块和快捷方式的前端数据库的后端数据库。 如果你想要拆分数据库迁移到[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，将前端数据库添加到 SSMA。  
  
下面的说明介绍如何创建项目、 将数据库添加到项目、 连接到[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，然后导出清单数据。  
  
**若要创建项目**  
  
1.  打开 access 的 SSMA。  
  
2.  在“文件”菜单中，选择“新建项目”。  
  
    此时将显示“新建项目”  对话框。  
  
3.  在中**名称**框中，输入你的项目的名称。  
  
4.  在中**位置**框中，输入或选择该项目的文件夹。  
  
5.  在中**迁移到**组合框中，选择你想要迁移，然后依次的目标版本**确定**。  
  
有关创建项目的详细信息，请参阅[创建和管理项目](creating-and-managing-projects-accesstosql.md)。  
  
**若要查找和添加数据库**  
  
1.  上**文件**菜单上，单击**查找数据库**。  
  
2.  在查找数据库向导中，输入驱动器、 文件路径或想要搜索的 UNC 路径。 或者，单击**浏览**选择驱动器或网络文件夹。  
  
3.  单击**添加**将位置添加到列表框。  
  
    重复前面的两个步骤添加其他搜索位置。  
  
4.  （可选） 添加搜索条件来完善的数据库返回的列表。  
  
    > [!IMPORTANT]  
    > **全部或部分文件名**文本框中不支持通配符字符。  
  
5.  单击**扫描**。  
  
    将显示扫描页。 这将显示已发现的数据库和搜索进度。 若要停止搜索，请单击**停止**。  
  
6.  在选择文件页上，选择你想要添加到项目的每个数据库。  
  
    可以使用**全**并**清除所有**要选择或清除所有数据库的列表顶部的按钮。 此外可以按住 CTRL 键来选择多个行，或按住 SHIFT 键以选择范围的行。  
  
7.  单击“下一步” 。  
  
8.  在验证页上，单击**完成**。  
  
有关将数据库添加到项目的详细信息，请参阅[添加和删除访问数据库文件](adding-and-removing-access-database-files-accesstosql.md)。  
  
**若要连接到 SQL Server**  
  
1.  上**文件**菜单中，选择**连接到 SQL Server**。  
  
2.  在连接对话框中，输入或选择的实例的名称[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。  
  
    -   如果要连接到本地计算机上的默认实例，则可以输入**localhost**或句点 (**。**)。  
  
    -   如果要连接到另一台计算机上的默认实例，输入的计算机的名称。  
  
    -   如果要连接到命名实例，则输入计算机名称、 一个反斜杠和实例名称。 例如： MyServer\MyInstance。  
  
3.  在中**数据库**框中，输入导出的元数据的目标数据库的名称。  
  
4.  如果你的实例[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]配置为接受非默认端口上的连接，请输入用于的端口号[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]中的连接**服务器端口**框。 对于默认实例的[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，默认端口号为 1433年。 对于命名实例，SSMA 尝试获取端口号从[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]浏览器服务。  
  
5.  在中**身份验证**下拉列表菜单中，选择要使用的连接身份验证类型。 若要使用当前 Windows 帐户，请选择**Windows 身份验证**。 若要使用[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]登录名，选择**SQL Server 身份验证**，然后提供用户名和密码。  
  
有关连接到详细信息[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，请参阅[连接到 SQL Server &#40;AccessToSQL&#41;](../../ssma/access/connecting-to-sql-server-accesstosql.md)。  
  
**若要导出清单信息**  
  
1.  在访问元数据资源管理器中，展开**访问元数据库**。  
  
2.  选中复选框旁边**数据库**。  
  
    若要省略了单独的数据库或数据库对象，展开**数据库**文件夹，然后再清除数据库或数据库对象旁边的复选框。  
  
3.  右键单击**数据库**，然后选择**导出架构**。  
  
4.  在中**选择用于导出的架构**对话框中，选择导出的元数据，目标架构，然后单击**确定**。  
  
导出元数据，每次 SSMA 将数据追加到清单。 在清单中的现有数据未更新或删除。  
  
## <a name="querying-the-exported-metadata"></a>查询导出的元数据  
导出有关访问数据库的元数据后，可以查询的元数据。 以下说明介绍如何使用中的查询编辑器窗口[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]运行查询。  
  
**若要查询的元数据**  
  
1.  从**启动**菜单，依次指向**所有程序**，指向**Microsoft [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2005年**或设置为**Microsoft [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2008**或设置为**Microsoft [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2012年**，然后单击**SQL Server Management Studio**。  
  
2.  在中**连接到服务器**对话框中，验证设置，然后依次**Connect**。  
  
3.  在 Management Studio 工具栏上，单击**新查询**以打开查询编辑器。  
  
4.  在查询编辑器窗口中，输入查询。 以下部分显示了一些示例。  
  
5.  按 F5 键以运行查询。  
  
## <a name="query-examples"></a>查询示例  
在运行任何以下查询之前，应运行 USE *database_name*查询，以确保针对包含导出的元数据的数据库运行查询。 例如，如果元数据导出为一个名为 MyAccessMetadata 数据库后，您将添加以下的开始处[!INCLUDE[tsql](../../includes/tsql-md.md)]代码：  
  
```  
USE MyAccessMetadata;  
GO  
```  
以下示例均使用**dbo**架构。 如果另一种架构导出元数据，请确保在运行这些查询时更改架构。  
  
### <a name="what-tables-and-columns-are-in-these-databases"></a>在这些数据库中哪些表和列？  
下面的查询联接表包含列、 表和数据库元数据，然后返回所有数据库、 表和列，按列名称的名称：  
  
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
以下查询返回数据库名称、 文件大小和数量的表中每个访问数据库，按文件大小：  
  
```  
SELECT DatabaseName, FileSize, TablesCount  
FROM dbo.SSMA_Access_InventoryDatabases  
ORDER BY FileSize DESC;  
```  
  
### <a name="who-is-the-owner-of-most-of-the-databases"></a>大部分数据库的所有者是谁？  
以下查询返回的数据库名称和所有者的每个访问数据库，按所有者排序。  
  
```  
SELECT DatabaseName, FileOwner  
FROM dbo.SSMA_Access_InventoryDatabases  
ORDER BY FileOwner;  
```  
  
### <a name="which-databases-contain-the-same-tables"></a>哪些数据库是否包含相同的表？  
下面的查询使用的子查询来查找所有出现在列表中的表，一次以上的表名称，然后使用此列表中的表以获取数据库名称。 结果返回为数据库名称，然后选择表名，并按表名称进行排序。  
  
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
以下查询获取当前日期、 六个月前，获取月份值，然后返回具有超过六个月以前的修改日期的数据库的列表。  
  
```  
SELECT DatabaseName, DateModified  
FROM dbo.SSMA_Access_InventoryDatabases  
WHERE DATEDIFF(month, DateModified, GETDATE()) > 6  
ORDER BY DateModified;  
```  
  
### <a name="which-databases-contain-private-information"></a>哪些数据库包含私人信息？  
您的 Access 数据库可能包含敏感或私人信息。 你可能想要移动到这些数据库[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]以利用其安全功能。 如果知道包含敏感数据的列具有特定名称，或包含特定字符，可以使用查询来查找包含该信息的所有列。 例如，可以找到所有列包含字符串"薪水"。  然后，查询返回数据库名称、 表名和列名。  
  
```  
SELECT DatabaseName, TableName, ColumnName   
FROM dbo.SSMA_Access_InventoryColumns C  
JOIN dbo.SSMA_Access_InventoryTables T  
ON C.TableId = T.TableId  
JOIN dbo.SSMA_Access_InventoryDatabases D  
ON T.DatabaseId = D. DatabaseId  
WHERE ColumnName LIKE '%salary%';  
```  
如果不知道的列名称，可以编写查询以返回所有列。 若要执行此操作，删除从之前的查询的 WHERE 子句。  
  
## <a name="see-also"></a>请参阅  
[为迁移准备 Access 数据库](preparing-access-databases-for-migration-accesstosql.md)  
  
