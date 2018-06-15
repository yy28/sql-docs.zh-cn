---
title: sys.sql_dependencies (Transact SQL) |Microsoft 文档
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.component: system-catalog-views
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sql_dependencies
- sql_dependencies_TSQL
- sys.sql_dependencies_TSQL
- sys.sql_dependencies
dev_langs:
- TSQL
helpviewer_keywords:
- sys.sql_dependencies catalog view
ms.assetid: 1779aa87-a0b8-470a-a286-d7cc0b93ad2e
caps.latest.revision: 31
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: b458e22f8b0b803dcd359b870af6f14b85a95f48
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/04/2018
ms.locfileid: "33221378"
---
# <a name="syssqldependencies-transact-sql"></a>sys.sql_dependencies (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  对在定义另一引用对象的 [!INCLUDE[tsql](../../includes/tsql-md.md)] 表达式或语句中引用的被引用的实体的每一依赖关系，均存在对应的一行。  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)] 使用[sys.sql_expression_dependencies](../../relational-databases/system-catalog-views/sys-sql-expression-dependencies-transact-sql.md)相反。  

  
|列名|数据类型|Description|  
|-----------------|---------------|-----------------|  
|class|**tinyint**|标识被引用的实体的类：<br /><br /> 0 = 对象或列名 （仅适用于非绑定到架构的引用）<br /><br /> 1 = 对象或列（架构绑定引用）<br /><br /> 2 = 类型（架构绑定引用）<br /><br /> 3 = XML 架构集合（架构绑定引用）<br /><br /> 4 = 分区函数（架构绑定引用）|  
|**class_desc**|**nvarchar(60)**|被引用的实体的类的说明：<br /><br /> **OBJECT_OR_COLUMN_REFERENCE_NON_SCHEMA_BOUND**<br /><br /> **OBJECT_OR_COLUMN_REFERENCE_SCHEMA_BOUND**<br /><br /> **TYPE_REFERENCE**<br /><br /> **XML_SCHEMA_COLLECTION_REFERENCE**<br /><br /> **PARTITION_FUNCTION_REFERENCE**|  
|**object_id**|**int**|引用对象的 ID。|  
|**column_id**|**int**|如果引用 ID 是一列，则为引用列的 ID；否则为 0。|  
|**referenced_major_id**|**int**|被引用的实体的 ID，由类的值解释，具体如下：<br /><br /> 0、1 = 对象或列的对象 ID。<br /><br /> 2 = 类型 ID。<br /><br /> 3 = XML 架构集合 ID。|  
|**referenced_minor_id**|**int**|被引用实体的 Minor-ID，由类的值解释，如下所示：<br /><br /> 当 class =:<br /><br /> 0， **referenced_minor_id**的列 id; 或如果不是列，则为 0。<br /><br /> 1， **referenced_minor_id**的列 id; 或如果不是列，则为 0。<br /><br /> 否则为**referenced_minor_id** = 0。|  
|**is_selected**|**bit**|选中了对象或列。|  
|**is_updated**|**bit**|更新了对象或列。|  
|**is_select_all**|**bit**|对象用在了 SELECT * 子句中（仅限对象级）。|  
  
## <a name="permissions"></a>权限  
 要求 **公共** 角色具有成员身份。 有关详细信息，请参阅 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)。  
  
## <a name="see-also"></a>另请参阅  
 [目录视图 (Transact-SQL)](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [对象目录视图 (Transact-SQL)](../../relational-databases/system-catalog-views/object-catalog-views-transact-sql.md)   
 [查询 SQL Server 系统目录常见问题解答](../../relational-databases/system-catalog-views/querying-the-sql-server-system-catalog-faq.md)  
  
  
