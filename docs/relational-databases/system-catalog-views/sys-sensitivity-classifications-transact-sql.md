---
title: sys.sensitivity_classifications (Transact SQL) |Microsoft 文档
ms.date: 06/17/2018
ms.reviewer: ''
ms.prod: sql
ms.prod_service: sql-database
ms.service: sql-database
ms.technology: t-sql
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: language-reference
ms.custom: ''
ms.manager: craigg
ms.author: giladm
author: giladmit
f1_keywords:
- 'sys.sensitivity_classifications '
dev_langs:
- TSQL
helpviewer_keywords:
- sys.sensitivity_classifications statement
- dropping labels
- drop labels
- removing labels
- remove labels
- classification [SQL]
- labels [SQL]
- information types
monikerRange: = azuresqldb-current || = sqlallproducts-allversions
ms.openlocfilehash: d0adbbeb82c06d6a44f3a7439bcbf479d7358401
ms.sourcegitcommit: 70882926439a63ab9d812809429c63040eb9a41b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36262880"
---
# <a name="syssensitivityclassifications-transact-sql"></a>sys.sensitivity_classifications (TRANSACT-SQL)
[!INCLUDE[tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md.md)]

返回数据库中的每个已分类的项的行。

|列名|数据类型|Description|
|-----------------|---------------|-----------------|  
|class|**int**|标识在其存在该分类的项的类|  
|**class_desc**|**varchar(16)**|在其存在该分类的项的类的说明|  
|**major_id**|**int**|在其上是否存在该分类的项的 ID。 < 巴西\>< 巴西\>major_id 如果类是 0，始终是 0。<br>如果 class 为 1、2 或 7，则 major_id 为 object_id。|  
|**minor_id**|**int**|项在其存在该分类，根据其类解释辅助 ID。<br><br>如果类 = 1，minor_id 是 column_id (如果列)，否则 0 (如果对象)。<br>如果 class = 2，则 minor_id 为 parameter_id。<br>如果类 = 7，minor_id 是 index_id。 |  
|label|**sysname**|已分配敏感度分类标签 （用户可读）|  
|**label_id**|**sysname**|可以使用信息保护系统等 Azure 信息保护 (AIP) 的标签与关联的 ID|  
|**information_type**|**sysname**|分配敏感度分类的信息类型 （用户可读）|  
|**information_type_id**|**sysname**|可以使用信息保护系统等 Azure 信息保护 (AIP) 的信息类型与关联的 ID|  
| &nbsp; | &nbsp; | &nbsp; |

## <a name="remarks"></a>Remarks  

- 此视图提供可见性的数据库的分类状态。 它可用于管理数据库分类，以及生成报表。
- 支持的数据库列的当前仅分类。 因此：
    - **类**-将始终具有值 1 （表示列）
    - **class_desc** -将始终具有值*OBJECT_OR_COLUMN*
    - **major_id** -表示包含已分类的列，表与 sys.all_objects.object_id 相对应的 ID
    - **minor_id** -表示在其是否存在该分类，sys.all_columns.column_id 与相应的列的 ID

## <a name="examples"></a>示例

### <a name="a-listing-all-classified-columns-and-their-corresponding-classification"></a>A. 列出所有已分类的列和其相应的分类

以下示例返回一张表，列出表名称、 列名称、 标签，标签 ID，信息类型，在数据库中每个已分类列的信息类型 ID。

```sql
SELECT
    sys.all_objects.name AS TableName, sys.all_columns.name As ColumnName,
    Label, Label_ID, Information_Type, Information_Type_ID
FROM
          sys.sensitivity_classifications
left join sys.all_objects on sys.sensitivity_classifications.major_id = sys.all_objects.object_id
left join sys.all_columns on sys.sensitivity_classifications.major_id = sys.all_columns.object_id
                         and sys.sensitivity_classifications.minor_id = sys.all_columns.column_id
```

## <a name="see-also"></a>请参阅  

[添加敏感度 CLASSIFICTION (Transact SQL)](../../t-sql/statements/add-sensitivity-classification-transact-sql.md)

[删除敏感度 CLASSIFICTION (Transact SQL)](../../t-sql/statements/drop-sensitivity-classification-transact-sql.md)

[开始使用 SQL 信息保护](http://aka.ms/sqlip)
