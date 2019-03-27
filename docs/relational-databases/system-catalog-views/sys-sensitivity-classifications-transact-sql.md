---
title: sys.sensitivity_classifications (TRANSACT-SQL) |Microsoft Docs
ms.date: 03/25/2019
ms.reviewer: ''
ms.prod: sql
ms.technology: t-sql
ms.topic: language-reference
ms.custom: ''
ms.manager: craigg
ms.author: arib
author: vainolo
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
ms.openlocfilehash: e75ebba2f48d0e2ec15ea871fe8d70a4b49e7318
ms.sourcegitcommit: 2db83830514d23691b914466a314dfeb49094b3c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/27/2019
ms.locfileid: "58493048"
---
# <a name="syssensitivityclassifications-transact-sql"></a>sys.sensitivity_classifications (Transact SQL)
[!INCLUDE[tsql-appliesto-xxxxxx-asdb-asdw-xxx-md](../../includes/tsql-appliesto-xxxxxx-asdb-asdw-xxx-md.md)]

返回数据库中的每个已分类的项的行。

|列名|数据类型|Description|
|-----------------|---------------|-----------------|  
|class|**int**|标识的类的分类在其存在的项|  
|**class_desc**|**varchar(16)**|分类在其存在的项的类的说明|  
|**major_id**|**int**|分类在其存在的项的 ID。 < b \>< b\>如果 class 为 0，则 major_id 始终是 0。<br>如果 class 为 1、2 或 7，则 major_id 为 object_id。|  
|**minor_id**|**int**|分类存在于其上，根据其类进行解释的项的辅助 ID。<br><br>如果类 = 1，minor_id 是 column_id (如果列)、 0 (如果对象)。<br>如果 class = 2，则 minor_id 为 parameter_id。<br>如果类 = 7，minor_id 为 index_id。 |  
|label|**sysname**|分配敏感度分类的标签 （用户可读）|  
|**label_id**|**sysname**|与标签，这是信息保护系统等 Azure 信息保护 (AIP) 可以使用关联的 ID|  
|**information_type**|**sysname**|敏感度分类分配的信息类型 （用户可读）|  
|**information_type_id**|**sysname**|可以使用通过信息保护系统等 Azure 信息保护 (AIP) 的信息类型与关联的 ID|  
| &nbsp; | &nbsp; | &nbsp; |

## <a name="remarks"></a>备注  

- 此视图提供可见性数据库分类状态。 它可以用于管理数据库分类，以及用于生成报告。
- 支持的数据库列的当前仅分类。 因此：
    - **类**-将始终具有值 1 （表示某一列）
    - **class_desc** -将始终具有值*OBJECT_OR_COLUMN*
    - **则 major_id** -表示包含已分类的列的表与 sys.all_objects.object_id 相对应的 ID
    - **minor_id** -表示分类存在于其，使用 sys.all_columns.column_id 相应的列的 ID

## <a name="examples"></a>示例

### <a name="a-listing-all-classified-columns-and-their-corresponding-classification"></a>A. 列出所有已分类的列和其相应的分类

以下示例返回一个表，该表列出表名、 列名、 标签，标签 ID，信息类型，在数据库中每个已分类列的信息类型 ID。

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

## <a name="permissions"></a>权限  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] 有关详细信息，请参阅 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)。  

## <a name="see-also"></a>请参阅  

[ADD SENSITIVITY CLASSIFICATION (Transact-SQL)](../../t-sql/statements/add-sensitivity-classification-transact-sql.md)

[DROP SENSITIVITY CLASSIFICATION (Transact-SQL)](../../t-sql/statements/drop-sensitivity-classification-transact-sql.md)

[SQL 信息保护入门](https://aka.ms/sqlip)
