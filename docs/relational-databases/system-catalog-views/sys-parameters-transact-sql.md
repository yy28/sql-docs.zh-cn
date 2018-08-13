---
title: sys.parameters (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.component: system-catalog-views
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sys.parameters_TSQL
- sys.parameters
- parameters
- parameters_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.parameters catalog view
- table-valued parameters,sys.parameters
ms.assetid: 24e2764b-c8e5-4322-97a4-7407d8b8a92b
caps.latest.revision: 49
author: edmacauley
ms.author: edmaca
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017'
ms.openlocfilehash: da8d3e66ed1d6e835c6b4702fc7bbab31dd186f2
ms.sourcegitcommit: 4cd008a77f456b35204989bbdd31db352716bbe6
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/06/2018
ms.locfileid: "39535167"
---
# <a name="sysparameters-transact-sql"></a>sys.parameters (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  接受参数的对象的每个参数在表中对应一行。 如果对象是标量函数，则另有一行说明返回值。 该行将有**parameter_id**值为 0。  
  
|列名|数据类型|Description|  
|-----------------|---------------|-----------------|  
|**object_id**|**int**|此参数所属的对象的 ID。|  
|**名称**|**sysname**|参数的名称。 在对象中是唯一的。<br /><br /> 如果对象是标量函数，则参数名称为表示返回值的行中的空字符串。|  
|**parameter_id**|**int**|参数的 ID。 在对象中是唯一的。<br /><br /> 如果对象是标量函数， **parameter_id** = 0 表示返回值。|  
|**system_type_id**|**tinyint**|参数的系统类型的 ID。|  
|**user_type_id**|**int**|用户定义的参数类型的 ID。<br /><br /> 若要返回的类型名称，将联接到[sys.types](../../relational-databases/system-catalog-views/sys-types-transact-sql.md)目录对此列的视图。|  
|**max_length**|**smallint**|参数，以字节为单位的最大长度。<br /><br /> 值 =-1，当列数据类型为**varchar （max)**， **nvarchar （max)**， **varbinary （max)**，或者**xml**。|  
|**精度**|**tinyint**|如果参数是基于数值的，则表示参数的精度；否则为 0。|  
|**scale**|**tinyint**|如果参数是基于数值的，则表示参数的小数位数；否则为 0。|  
|**is_output**|**bit**|1 = 参数为 OUTPUT 或 RETURN；否则为 0。|  
|**is_cursor_ref**|**bit**|1 = 参数为游标引用参数。|  
|**has_default_value**|**bit**|1 = 参数具有默认值。<br /><br /> [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 只维护该目录视图中的 CLR 对象的默认值；因此，对于 [!INCLUDE[tsql](../../includes/tsql-md.md)] 对象，此列包含值 0。 若要查看中的参数的默认值[!INCLUDE[tsql](../../includes/tsql-md.md)]对象，请查询**定义**的列[sys.sql_modules](../../relational-databases/system-catalog-views/sys-sql-modules-transact-sql.md)目录视图，或使用[OBJECT_DEFINITION](../../t-sql/functions/object-definition-transact-sql.md)系统函数。|  
|**is_xml_document**|**bit**|1 = 内容为完整的 XML 文档。<br /><br /> 0 = 内容是文档片段或列的数据类型不是**xml**。|  
|**default_value**|**sql_variant**|如果**has_default_value**为 1，此列的值是为该参数的默认值; 否则为 NULL。|  
|**xml_collection_id**|**int**|非零参数的数据类型是否**xml**和类型化 XML。 此值为包含验证参数的 XML 架构命名空间的集合的 ID。<br /><br /> 0 = 没有 XML 架构集合。|  
|**is_readonly**|**bit**|1 = 参数为 READONLY；否则为 0。|  
|**is_nullable**|**bit**|1 = 参数不可为 Null。 （默认值）。<br /><br /> 0 = 参数不可为 Null，这样可更高效地执行本机编译存储过程。|  
  
## <a name="permissions"></a>Permissions  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] 有关详细信息，请参阅 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)。  
  
## <a name="see-also"></a>请参阅  
 [对象目录视图 (Transact-SQL)](../../relational-databases/system-catalog-views/object-catalog-views-transact-sql.md)   
 [目录视图 (Transact-SQL)](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [查询 SQL Server 系统目录常见问题](../../relational-databases/system-catalog-views/querying-the-sql-server-system-catalog-faq.md)   
 [sys.all_parameters &#40;TRANSACT-SQL&#41;](../../relational-databases/system-catalog-views/sys-all-parameters-transact-sql.md)   
 [sys.system_parameters &#40;TRANSACT-SQL&#41;](../../relational-databases/system-catalog-views/sys-system-parameters-transact-sql.md)  
  
  
