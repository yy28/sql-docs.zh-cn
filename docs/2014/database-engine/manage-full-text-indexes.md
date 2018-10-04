---
title: 管理全文索引 |Microsoft Docs
ms.custom: ''
ms.date: 03/08/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: search
ms.topic: conceptual
ms.assetid: 28ff17dc-172b-4ac4-853f-990b5dc02fd1
author: craigg-msft
ms.author: craigg
manager: craigg
ms.openlocfilehash: d55a1a8bef5e3d4a74aa2bb09c27e3f7c2a8dc82
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2018
ms.locfileid: "48066800"
---
# <a name="manage-full-text-indexes"></a>管理全文索引
     
##  <a name="view"></a> 查看和更改全文索引的属性  
  
#### <a name="to-view-or-change-the-properties-of-a-full-text-index-in-management-studio"></a>在 Management Studio 中查看或更改全文索引的属性  
  
1.  在对象资源管理器中，展开服务器。  
  
2.  展开“数据库”，然后展开包含全文索引的数据库。  
  
3.  展开 **“表”**。  
  
4.  右键单击对其定义了全文索引的表，选择“全文索引”，然后在“全文索引”上下文菜单中单击“属性”。 此时将打开“全文索引属性”对话框。  
  
5.  在 **“选择页”** 窗格中，您可以选择下列页中的任一页：  
  
    |第|Description|  
    |----------|-----------------|  
    |**常规**|显示全文索引的基本属性。 这些基本属性包括若干个可修改属性和多个不可更改属性，后者如数据库名称、表名和全文键列的名称。 可修改属性包括：<br /><br /> **全文索引非索引字表**<br /><br /> **全文索引已启用**<br /><br /> **更改跟踪**<br /><br /> **搜索属性列表**<br /><br /> <br /><br /> 有关详细信息，请参阅[全文本索引属性（常规页）](full-text-index-properties-general-page.md)。|  
    |**“列”**|显示可用于全文索引的表列。 对于选中的列，均会创建全文索引。 您可以根据需要选择将任意数目的可用列包括在全文索引中。 有关详细信息，请参阅[全文本索引属性（列页）](../../2014/database-engine/full-text-index-properties-columns-page.md)。|  
    |**计划**|使用此页可以创建或管理 SQL Server 代理作业的计划，该作业用于启动全文索引填充的表增量填充。 有关详细信息，请参阅 [填充全文索引](../relational-databases/indexes/indexes.md)。<br /><br /> **\*\* 重要\* \*** 退出后**全文本索引属性**对话框中，所有新创建的计划程序与 SQL Server 代理作业 （启动表增量填充*database_name*。*table_name*)。|  
  
6.  [!INCLUDE[clickOK](../includes/clickok-md.md)] 以保存任何更改并退出“全文索引属性”对话框。  
  
##  <a name="props"></a> 查看索引的表和列的属性  
 一些 [!INCLUDE[tsql](../includes/tsql-md.md)] 函数（例如 OBJECTPROPERTYEX）可用来获取各种全文索引属性的值。 此信息可用于全文搜索的管理和故障排除。  
  
 下表列出了与索引表和列相关的全文属性及其相关 [!INCLUDE[tsql](../includes/tsql-md.md)] 函数。  
  
|“属性”|Description|函数|  
|--------------|-----------------|--------------|  
|`FullTextTypeColumn`|表中的 TYPE COLUMN，其中包含列的文档类型信息。|[COLUMNPROPERTY](/sql/t-sql/functions/columnproperty-transact-sql)|  
|`IsFulltextIndexed`|列是否启用了全文索引。|COLUMNPROPERTY|  
|`IsFulltextKey`|索引是否为表的全文键。|[INDEXPROPERTY](/sql/t-sql/functions/indexproperty-transact-sql)|  
|**TableFulltextBackgroundUpdateIndexOn**|表是否具有全文后台更新索引。|[OBJECTPROPERTYEX](/sql/t-sql/functions/objectproperty-transact-sql)|  
|`TableFulltextCatalogId`|表的全文索引数据所在的全文目录 ID。|OBJECTPROPERTYEX|  
|`TableFulltextChangeTrackingOn`|表是否启用了全文更改跟踪。|OBJECTPROPERTYEX|  
|`TableFulltextDocsProcessed`|自开始全文检索以来所处理的行数。|OBJECTPROPERTYEX|  
|**TableFulltextFailCount**|全文搜索未编制索引的行数。|OBJECTPROPERTYEX|  
|**TableFulltextItemCount**|成功编制了全文索引的行数。|OBJECTPROPERTYEX|  
|`TableFulltextKeyColumn`|全文唯一键列的列 ID。|OBJECTPROPERTYEX|  
|`TableFullTextMergeStatus`|具有全文索引的表当前是否正在合并。|OBJECTPROPERTYEX|  
|**TableFulltextPendingChanges**|要处理的挂起更改跟踪项的数目。|OBJECTPROPERTYEX|  
|`TableFulltextPopulateStatus`|全文表的填充状态。|OBJECTPROPERTYEX|  
|`TableHasActiveFulltextIndex`|表是否具有活动的全文索引。|OBJECTPROPERTYEX|  
  
##  <a name="key"></a> 获取有关全文索引键列的信息  
 通常情况下，CONTAINSTABLE 或 FREETEXTTABLE 行集值函数的结果需要与基表相联接。 在这样的情况下，需要知道唯一键列名称。 可以查询给定的唯一索引是否作为全文键使用，并且可以获取全文键列的标识符。  
  
#### <a name="to-inquire-whether-a-given-unique-index-is-used-as-the-full-text-key-column"></a>查询给定的唯一索引是否作为全文键列使用  
  
1.  使用 [SELECT](/sql/t-sql/queries/select-transact-sql) 语句调用 [INDEXPROPERTY](/sql/t-sql/functions/indexproperty-transact-sql) 函数。 在函数中调用使用 OBJECT_ID 函数将转换的表的名称 (*table_name*) 转换为表 ID，指定表中，唯一索引的名称，并指定`IsFulltextKey`索引属性，按如下所示：  
  
    ```  
    SELECT INDEXPROPERTY( OBJECT_ID('table_name'), 'index_name',  'IsFulltextKey' );  
    ```  
  
     如果使用此索引来强制实现全文键列的唯一性，此语句返回 1，否则返回 0。  
  
 **示例**  
  
 下例查询 `PK_Document_DocumentID` 索引是否用于强制实现全文键列的唯一性，如下所示：  
  
```  
USE AdventureWorks  
GO  
SELECT INDEXPROPERTY ( OBJECT_ID('Production.Document'), 'PK_Document_DocumentID',  'IsFulltextKey' )  
```  
  
 如果使用 `PK_Document_DocumentID` 索引来强制实现全文键列的唯一性，则此示例返回 1。 否则，它返回 0 或 NULL。 NULL 表示您使用的是无效索引名称，索引名称与表不对应，或表不存在，等等。  
  
#### <a name="to-find-the-identifier-of-the-full-text-key-column"></a>查找全文键列的标识符  
  
1.  每个启用全文的表都有一个列，该列用于强制实现表中行的唯一性（“唯一键列”）。 从 OBJECTPROPERTYEX 函数获取的 `TableFulltextKeyColumn` 属性包含唯一键列的列 ID。  
  
     若要获取此标识符，可以使用 SELECT 语句调用 OBJECTPROPERTYEX 函数。 使用 OBJECT_ID 函数将转换的表的名称 (*table_name*) 转换为表 ID，并指定`TableFulltextKeyColumn`属性，如下所示：  
  
    ```  
    SELECT OBJECTPROPERTYEX(OBJECT_ID( 'table_name'), 'TableFulltextKeyColumn' ) AS 'Column Identifier';  
    ```  
  
 **示例**  
  
 下例返回全文键列的标识符或 NULL。 NULL 表示您使用的是无效索引名称，索引名称与表不对应，或表不存在，等等。  
  
```  
USE AdventureWorks;  
GO  
SELECT OBJECTPROPERTYEX(OBJECT_ID('Production.Document'), 'TableFulltextKeyColumn');  
GO  
```  
  
 下例说明如何使用唯一键列的标识符获取列的名称。  
  
```  
USE AdventureWorks;  
GO  
DECLARE @key_column sysname  
SET @key_column = Col_Name(Object_Id('Production.Document'),  
ObjectProperty(Object_id('Production.Document'),  
'TableFulltextKeyColumn')   
)  
SELECT @key_column AS 'Unique Key Column';  
GO  
```  
  
 此示例返回一个名为 `Unique Key Column`的结果集列，该结果集列显示单个行，该行包含 Document 表的唯一键列 DocumentID 的名称。 请注意，如果此查询包含无效的索引名称，索引名称与表不对应或表不存在等，它将返回 NULL。  
  
##  <a name="disable"></a> 如果禁用或重新启用全文索引的表  
 在 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 中，默认情况下所有由用户创建的数据库都启用了全文索引。 另外，在为表创建全文索引并将列添加到索引之后，就会自动为单个表启用全文索引。 从表的全文索引中删除最后一列时，会自动为表禁用全文索引。  
  
 对于具有全文索引的表，可以使用 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] 手动为表禁用或重新启用全文索引。  
  
#### <a name="to-enable-a-table-for-full-text-indexing"></a>为表启用全文索引  
  
1.  展开服务器组，展开“数据库”，再展开包含要为其启用全文索引的表的数据库。  
  
2.  展开“表”，然后右键单击要为其禁用或重新启用全文索引的表。  
  
3.  选择“全文索引”，然后单击“禁用全文索引”或“启用全文索引”。  
  
##  <a name="remove"></a> 从表中删除全文索引  
  
#### <a name="to-remove-a-full-text-index-from-a-table"></a>从表中删除全文索引  
  
1.  在对象资源管理器中，右键单击要删除的全文索引所在的表。  
  
2.  选择“删除全文索引”。  
  
3.  在出现提示时，单击“确定”，确认是否要删除该全文索引。  
  
  
