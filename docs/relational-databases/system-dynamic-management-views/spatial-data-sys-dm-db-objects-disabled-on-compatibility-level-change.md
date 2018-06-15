---
title: sys.dm_db_objects_disabled_on_compatibility_level_change (Transact SQL) |Microsoft 文档
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- dm_db_objects_disabled_on_compatibility_level_change
- dm_db_objects_disabled_on_compatibility_level_change_TSQL
- sys.dm_db_objects_disabled_on_compatibility_level_change
- sys.dm_db_objects_disabled_on_compatibility_level_change_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_db_objects_disabled_on_compatibility_level_change catalog view
ms.assetid: a5d70064-0330-48b9-b853-01eba50755d0
caps.latest.revision: 16
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: = azuresqldb-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 083af55f2629a14f2ad28b293bb84ea9184a0345
ms.sourcegitcommit: 7019ac41524bdf783ea2c129c17b54581951b515
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/23/2018
ms.locfileid: "34467103"
---
# <a name="spatial-data---sysdmdbobjectsdisabledoncompatibilitylevelchange"></a>空间数据-sys.dm_db_objects_disabled_on_compatibility_level_change
[!INCLUDE[tsql-appliesto-ss2012-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-asdb-xxxx-xxx-md.md)]

  列出由于更改 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中的兼容级别而将禁用的索引和约束。 在升级或更改兼容级别之后，包含持久化计算列且其表达式使用空间 UDT 的索引和约束将被禁用。 使用此动态管理函数可以确定兼容级别变化所带来的影响。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```sql  
sys.dm_db_objects_disabled_on_compatibility_level_change ( compatibility_level )   
```  
  
##  <a name="Arguments"></a> 参数  
 *compatibility_level*  
 **int**标识你打算设置的兼容性级别。  
  
## <a name="table-returned"></a>返回的表  
  
|列名|数据类型|Description|  
|-----------------|---------------|-----------------|  
|class|**int**|1 = 约束<br /><br /> 7 = 索引和堆|  
|**class_desc**|**nvarchar(60)**|约束的 OBJECT 或 COLUMN<br /><br /> 索引和堆的 INDEX|  
|**major_id**|**int**|约束的 OBJECT ID<br /><br /> 包含索引和堆的表的 OBJECT ID|  
|**minor_id**|**int**|对于约束为 NULL<br /><br /> 索引和堆的 Index_id|  
|**依赖项**|**nvarchar(60)**|导致禁用约束或索引的依赖项的说明。 在升级过程中引发的警告中也使用相同的值。 这方面的例子有：<br /><br /> “space”对应于内部<br /><br /> “geometry”对应于系统 UDT<br /><br /> “geography::Parse”对应于系统 UDT 的一个方法|  
  
## <a name="general-remarks"></a>一般备注  
 当更改兼容级别时，将禁用使用某些内部函数的持久化计算列。 此外，当升级数据库时，将禁用使用任何 Geometry 或 Geography 方法的持久化计算列。  
  
### <a name="which-functions-cause-persisted-computed-columns-to-be-disabled"></a>哪些函数会导致禁用持久化计算列？  
 当在持久化计算列的表达式中使用以下函数时，如果兼容级别从 80 更改为 90，则它们会导致禁用引用这些列的索引和约束：  
  
-   **IsNumeric**  
  
 当在持久化计算列的表达式中使用以下函数时，如果兼容级别从 100 更改为 110 或更高级别，则它们会导致禁用引用这些列的索引和约束：  
  
-   **Soundex**  
  
-   **Geography:: GeomFromGML**  
  
-   **Geography:: STGeomFromText**  
  
-   **Geography:: STLineFromText**  
  
-   **Geography:: STPolyFromText**  
  
-   **Geography:: STMPointFromText**  
  
-   **Geography:: STMLineFromText**  
  
-   **Geography:: STMPolyFromText**  
  
-   **Geography:: STGeomCollFromText**  
  
-   **Geography:: STGeomFromWKB**  
  
-   **Geography:: STLineFromWKB**  
  
-   **Geography:: STPolyFromWKB**  
  
-   **Geography:: STMPointFromWKB**  
  
-   **Geography:: STMLineFromWKB**  
  
-   **Geography:: STMPolyFromWKB**  
  
-   **Geography:: STUnion**  
  
-   **Geography:: STIntersection**  
  
-   **Geography:: STDifference**  
  
-   **Geography:: STSymDifference**  
  
-   **Geography:: STBuffer**  
  
-   **Geography:: BufferWithTolerance**  
  
-   **Geography:: 分析**  
  
-   **Geography:: 减少**  
  
### <a name="behavior-of-the-disabled-objects"></a>已禁用对象的行为  
 **索引**  
  
 如果已禁用的聚集的索引，或如果非聚集索引而强制，会引发以下错误:"查询处理器不能生成计划，因为索引 %。\*ls 表或视图 %。\*ls 已禁用。" 若要重新启用这些对象，重新生成索引升级后通过调用**ALTER INDEX ON...重新生成**。  
  
 **堆**  
  
 如果使用具有已禁用堆的表，则会引发以下错误。 若要重新启用这些对象，升级后重新生成通过调用**ALTER INDEX 所有 ON...重新生成**。  
  
```  
// ErrorNumber: 8674  
// ErrorSeverity: EX_USER  
// ErrorFormat: The query processor is unable to produce a plan because the table or view '%.*ls' is disabled.  
// ErrorCause: The table has a disabled heap.   
// ErrorCorrectiveAction: Rebuild the disabled heap to enable it.   
// ErrorInserts: table or view name   
// ErrorOwner: mtintor   
// ErrorFirstProduct: SQL11  
```  
  
 如果你尝试在联机操作期间重新生成堆时，将引发错误。  
  
 **Check 约束和外键**  
  
 禁用的检查约束和外键不会引发错误。 但修改行时，不强制执行约束。 若要重新启用这些对象，可通过调用升级后检查约束**ALTER TABLE...CHECK 约束**。  
  
 **持久化计算的列**  
  
 由于无法禁用单个列，因此将通过禁用聚集索引或堆来禁用整个表。  
  
## <a name="security"></a>Security  
  
### <a name="permissions"></a>权限  
 需要拥有 VIEW DATABASE STATE 权限。  
  
## <a name="example"></a>示例  
 下面的示例演示上一个查询查询**sys.dm_db_objects_disabled_on_compatibility_level_change**来查找更改兼容性级别为 120 受影响的对象。  
  
```sql  
SELECT * FROM sys.dm_db_objects_disabled_on_compatibility_level_change(120);  
GO  
  
```  
  
  
