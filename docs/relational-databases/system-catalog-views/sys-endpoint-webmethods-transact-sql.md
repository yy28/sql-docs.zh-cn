---
title: sys.endpoint_webmethods (Transact SQL) |Microsoft 文档
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: system-catalog-views
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sys.endpoint_webmethods_TSQL
- sys.endpoint_webmethods
- endpoint_webmethods_TSQL
- sys.http_soap_methods_TSQL
- endpoint_webmethods
- sys.http_soap_methods
dev_langs:
- TSQL
helpviewer_keywords:
- sys.endpoint_webmethods catalog view
ms.assetid: 7dad0cf6-eafa-47cf-98cc-75ba8d3c7959
caps.latest.revision: 37
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 039f084d20aa1b64bdd841b9279be5a065e4a9f6
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/16/2018
---
# <a name="sysendpointwebmethods-transact-sql"></a>sys.endpoint_webmethods (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)]  
  
 在启用了 SOAP 的 HTTP 端点上定义的每个 SOAP 方法各占一行。 Endpoint_id 和命名空间列的组合是唯一的。  
  
|列名|数据类型|Description|  
|-----------------|---------------|-----------------|  
|endpoint_id|**int**|定义了 Web 方法的端点的 ID。|  
|namespace|**nvarchar(384)**|Web 方法的命名空间。|  
|method_alias|**nvarchar(64)**|方法的别名。<br /><br /> 注意：[!INCLUDE[tsql](../../includes/tsql-md.md)]标识符允许不在中是合法 WSDL 方法名称的字符。<br /><br /> 别名用于将端点 WSDL 说明中公开的名称映射到调用 Web 方法时调用的实际基本 [!INCLUDE[tsql](../../includes/tsql-md.md)] 可执行对象。|  
|object_name|**nvarchar(776)**|Web 方法重定向到的对象名称，在 NAME = 选项中指定。 名称部分由句点 （.） 分隔的分隔使用方括号， `[``]`。<br /><br /> 对象名称必须由三个部分组成，在 WSDL 选项中指定。|  
|result_schema|**tinyint**|确定将哪个 XSD（如果有）与响应一起发回的选项。<br /><br /> 0 = 无<br /><br /> 1 = Standard<br /><br /> 2 = Default|  
|result_schema_desc|**nvarchar(60)**|确定将哪个 XSD（如果有）与响应一起发回的选项的说明。<br /><br /> 无<br /><br /> STANDARD<br /><br /> DEFAULT|  
|result_format|**tinyint**|确定如何在响应中设置结果格式的选项。<br /><br /> 1 = ALL_RESULTS<br /><br /> 2 = ROWSETS_ONLY<br /><br /> 3 = NONE|  
|result_format_desc|**nvarchar(60)**|确定如何在响应中设置结果格式的选项的说明。<br /><br /> ALL_RESULTS<br /><br /> ROWSETS_ONLY<br /><br /> 无|  
  
## <a name="permissions"></a>权限  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] 有关详细信息，请参阅 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)。  
  
## <a name="see-also"></a>另请参阅  
 [终结点目录视图 (Transact-SQL)](../../relational-databases/system-catalog-views/endpoints-catalog-views-transact-sql.md)   
 [目录视图 (Transact-SQL)](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)  
  
  
