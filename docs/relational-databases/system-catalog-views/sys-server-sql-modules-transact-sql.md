---
title: sys.server_sql_modules (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.server_sql_modules
- sys.server_sql_modules_TSQL
- server_sql_modules_TSQL
- server_sql_modules
dev_langs:
- TSQL
helpviewer_keywords:
- sys.server_sql_modules catalog view
ms.assetid: 9ef9a8b9-c470-4a61-b0c4-ee24ad871d63
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 95583de206841bb3ed3ccff42809c028443c63ab
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62743949"
---
# <a name="sysserversqlmodules-transact-sql"></a>sys.server_sql_modules (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  包含类型为 TR 的服务器级别触发器的 SQL 模块设置。 可将此关系与 sys.server_triggers 联接。 元组 (object_id) 是关系键。  
  
|列名|数据类型|Description|  
|-----------------|---------------|-----------------|  
|**object_id**|**int**|这是返回给定义该模块的服务器级别触发器的 FOREIGN KEY 引用。|  
|**definition**|**nvarchar(max)**|定义此模块的 SQL 文本。<br /><br /> NULL = 加密。|  
|**uses_ansi_nulls**|**bit**|模块是通过将 ANSI NULLS 设置选项设置为 ON 而创建的。|  
|**uses_quoted_identifier**|**bit**|模块是通过将 QUOTED IDENTIFIER 设置选项设置为 ON 而创建的。|  
|**execute_as_principal_id**|**int**|EXECUTE AS 服务器主体的 ID。<br /><br /> 默认情况下或在 EXECUTE AS CALLER 情况下，值为 NULL。<br /><br /> 指定主体 if 的 ID 执行 AS SELF EXECUTE AS 主体-2 = EXECUTE AS OWNER。|  
  
## <a name="permissions"></a>权限  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] 有关详细信息，请参阅 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)。  
  
## <a name="see-also"></a>请参阅  
 [目录视图 (Transact-SQL)](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)  
  
  
