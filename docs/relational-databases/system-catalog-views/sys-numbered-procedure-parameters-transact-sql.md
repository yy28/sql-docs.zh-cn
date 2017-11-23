---
title: "sys.numbered_procedure_parameters (Transact SQL) |Microsoft 文档"
ms.custom: 
ms.date: 06/10/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-catalog-views
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- numbered_procedure_parameters_TSQL
- sys.numbered_procedure_parameters_TSQL
- numbered_procedure_parameters
- sys.numbered_procedure_parameters
dev_langs: TSQL
helpviewer_keywords: sys.numbered_procedure_parameters catalog view
ms.assetid: a441d46d-1f30-41c2-8d94-e9442f59786e
caps.latest.revision: "20"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 8d2eee8a375dc7b2705b69b93a99f6ce2d8eae4b
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/21/2017
---
# <a name="sysnumberedprocedureparameters-transact-sql"></a>sys.numbered_procedure_parameters (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  带编号过程的每个参数都在表中对应一行。 当您创建带编号的存储过程时，基过程的编号为 1。 所有后续过程的编号依次为 2、3 等。 **sys.numbered_procedure_parameters**包含编号为 2 的所有后续的过程的参数定义和更高版本。 该视图不显示基存储过程（编号 = 1）的参数。 基存储过程类似于无编号的存储过程。 因此，在中表示其参数[sys.parameters (TRANSACT-SQL)](../../relational-databases/system-catalog-views/sys-parameters-transact-sql.md)。  
  
> [!IMPORTANT]  
>  不推荐使用带编号的过程。 建议您不要使用带编号过程。 当编译使用此目录视图的查询时，将会激发 DEPRECATION_ANNOUNCEMENT 事件。  
  
> [!NOTE]  
>  带编号的过程不支持 XML 和 CLR 参数。  
  
||  
|-|  
|**适用范围**： [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] （[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 到 [当前版本](http://go.microsoft.com/fwlink/p/?LinkId=299658)）。|  
  
|列名|数据类型|Description|  
|-----------------|---------------|-----------------|  
|**object_id**|**int**|此参数所属的对象 ID。|  
|**procedure_number**|**int**|对象中这种过程的数目（2 或更多）。|  
|**名称**|**sysname**|参数的名称。 在中是唯一**procedure_number**。|  
|**parameter_id**|**int**|参数的 ID。 在中是唯一**procedure_number**。|  
|**system_type_id**|**tinyint**|参数的系统类型的 ID。|  
|**user_type_id**|**int**|为用户的参数定义的类型的 ID。|  
|**max_length**|**int**|参数的最大长度（字节）。<br /><br /> -1 = 列数据类型为 varchar(max)、nvarchar(max) 或 varbinary(max)。|  
|**精度**|**tinyint**|如果参数是基于数值的，则表示参数的精度；否则为 0。|  
|**缩放**|**tinyint**|如果参数是基于数值的，则表示参数的小数位数；否则为 0。|  
|**is_output**|**bit**|1 = 输出或返回参数；否则为 0|  
|**is_cursor_ref**|**bit**|1 = 参数是一个光标引用参数。|  
  
> [!NOTE]  
>  带编号的过程不支持 XML 和 CLR 参数。  
  
## <a name="permissions"></a>Permissions  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] 有关详细信息，请参阅 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)。  
  
## <a name="see-also"></a>另请参阅  
 [对象目录视图 &#40;Transact SQL &#41;](../../relational-databases/system-catalog-views/object-catalog-views-transact-sql.md)   
 [目录视图 (Transact-SQL)](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)  
  
  
