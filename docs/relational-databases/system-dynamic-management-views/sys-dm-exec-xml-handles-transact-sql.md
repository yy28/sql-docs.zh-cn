---
title: sys.dm_exec_xml_handles (TRANSACT-SQL) |Microsoft 文档
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine, sql-data-warehouse
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- dm_exec_xml_handles
- dm_exec_xml_handles_TSQL
- sys.dm_exec_xml_handles_TSQL
- sys.dm_exec_xml_handles
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_exec_xml_handles dynamic management function
ms.assetid: a873ce0f-6955-417a-96a1-b2ef11a83633
caps.latest.revision: 12
author: douglaslMS
ms.author: douglasl
manager: craigg
monikerRange: = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 66702418faae18f1c4582a28353e2f5ae7c156bc
ms.sourcegitcommit: e77197ec6935e15e2260a7a44587e8054745d5c2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/11/2018
ms.locfileid: "38046105"
---
# <a name="sysdmexecxmlhandles-transact-sql"></a>sys.dm_exec_xml_handles (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-asdw-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-asdw-xxx-md.md)]

  返回有关活动已经通过打开的句柄的信息**sp_xml_preparedocument**。  
  
## <a name="syntax"></a>语法  
  
```  
  
dm_exec_xml_handles (session_id | 0 )  
```  
  
## <a name="arguments"></a>参数  
 *session_id* | 0，  
 会话的 ID。 如果*session_id*指定，则此函数返回有关 XML 句柄的信息中指定的会话。  
  
 如果指定 0，该函数将返回所有会话中的所有 XML 句柄的信息。  
  
## <a name="table-returned"></a>返回的表  
  
|列名|数据类型|Description|  
|-----------------|---------------|-----------------|  
|**session_id**|**int**|持有 XML 文档句柄的会话的会话 ID。|  
|**document_id**|**int**|返回 XML 文档句柄 ID **sp_xml_preparedocument**。|  
|**namespace_document_id**|**int**|用于已作为第三个参数传递的关联的命名空间文档的内部句柄 ID **sp_xml_preparedocument**。 如果没有命名空间文档，则为 NULL。|  
|**sql_handle**|**varbinary(64)**|定义句柄所在的 SQL 代码的文本句柄。|  
|**statement_start_offset**|**int**|在当前正在执行的字符数批处理或存储的过程从该处**sp_xml_preparedocument**调用时发生。 可以使用连同**sql_handle**，则**statement_end_offset**，和**sys.dm_exec_sql_text**动态管理函数以检索当前执行请求的语句。|  
|**statement_end_offset**|**int**|在当前正在执行的字符数批处理或存储的过程从该处**sp_xml_preparedocument**调用时发生。 可以使用连同**sql_handle**，则**statement_start_offset**，和**sys.dm_exec_sql_text**动态管理函数以检索当前执行请求的语句。|  
|**creation_time**|**datetime**|时间戳时**sp_xml_preparedocument**调用。|  
|**original_document_size_bytes**|**bigint**|未分析的 XML 文档的大小（字节）。|  
|**original_namespace_document_size_bytes**|**bigint**|未分析的 XML 命名空间文档的大小（字节）。 如果没有命名空间文档，则为 NULL。|  
|**num_openxml_calls**|**bigint**|具有该文档句柄的 OPENXML 调用数。|  
|**row_count**|**bigint**|该文档句柄以前的所有 OPENXML 调用返回的行数。|  
|**dormant_duration_ms**|**bigint**|自上次 OPENXML 调用以来经过的时间（毫秒）。 如果未调用 OPENXML，则返回起经过的毫秒**sp_xml_preparedocumen**t 调用。|  
  
## <a name="remarks"></a>Remarks  
 生存期**sql_handle**用来检索执行调用的 SQL 文本**sp_xml_preparedocument**长于缓存用来执行查询的计划。 如果查询文本在缓存中不可用，则无法使用函数结果中提供的信息来检索数据。 如果您正在运行多个大型批处理，则可能出现上述情况。  
  
## <a name="permissions"></a>权限  
 要求对服务器拥有 VIEW SERVER STATE 权限，以查看不归调用者所有的全部会话或会话 ID。 调用者始终可以查看自己的当前会话 ID 的数据。      
  
## <a name="examples"></a>示例  
 以下示例将选择所有活动句柄。  
  
```  
SELECT * FROM sys.dm_exec_xml_handles(0);  
```  
  
## <a name="see-also"></a>请参阅  
 <br>[动态管理视图和函数 (Transact SQL)](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)
 <br>[与执行相关的动态管理视图和函数 (Transact SQL)](../../relational-databases/system-dynamic-management-views/execution-related-dynamic-management-views-and-functions-transact-sql.md)
 <br>[sp_xml_preparedocument (TRANSACT-SQL)](../system-stored-procedures/sp-xml-preparedocument-transact-sql.md)
 <br>[sp_xml_removedocument (TRANSACT-SQL)](../system-stored-procedures/sp-xml-removedocument-transact-sql.md)


 
  
  
