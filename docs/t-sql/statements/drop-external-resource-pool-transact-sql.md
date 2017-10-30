---
title: "删除外部资源池 (Transact SQL) |Microsoft 文档"
ms.custom: 
ms.date: 03/17/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- DROP EXTERNAL RESOURCE POOL
- DROP_EXTERNAL_RESOURCE_POOL_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- DROP EXTERNAL RESOURCE POOL statement
ms.assetid: e2fa01bd-96ff-4ea9-bb08-6cb6b6adf68c
caps.latest.revision: 6
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: a0aae6de75280fb0e32879ece5acea6d0fd94f3c
ms.contentlocale: zh-cn
ms.lasthandoff: 09/01/2017

---
# <a name="drop-external-resource-pool-transact-sql"></a>删除外部资源池 (Transact SQL)
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

  删除用于定义外部进程的资源的资源调控器外部资源池。 R Services 的外部池控制`rterm.exe`， `BxlServer.exe`，与它们生成的其他进程。 通过使用创建外部资源池[CREATE EXTERNAL RESOURCE POOL &#40;Transact SQL &#41;](../../t-sql/statements/create-external-resource-pool-transact-sql.md)和可通过修改[ALTER EXTERNAL RESOURCE POOL &#40;Transact SQL &#41;](../../t-sql/statements/alter-external-resource-pool-transact-sql.md).  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)。  
  
## <a name="syntax"></a>语法  
  
```  
DROP EXTERNAL RESOURCE POOL pool_name  
```  
  
## <a name="arguments"></a>参数  
 *pool_name*  
 要删除的外部资源池的名称。  
  
## <a name="remarks"></a>注释  
 如果它包含工作负荷组，无法删除外部资源池。  
  
 不能删除资源调控器默认池或内部池。  
  
 重新配置未 n  
  
 建议您在熟悉资源调控器状态之后再执行 DDL 语句。 有关详细信息，请参阅[资源调控器](../../relational-databases/resource-governor/resource-governor.md)。  
  
## <a name="permissions"></a>Permissions  
 需要 `CONTROL SERVER` 权限。  
  
## <a name="examples"></a>示例  
 下面的示例删除名为的外部资源池`ex_pool`。  
  
```  
DROP EXTERNAL RESOURCE POOL ex_pool;  
GO  
ALTER RESOURCE GOVERNOR RECONFIGURE;  
GO  
```  
  
## <a name="see-also"></a>另请参阅  
 [启用了外部脚本的服务器配置选项](../../database-engine/configure-windows/external-scripts-enabled-server-configuration-option.md)   
 [SQL Server R Services](../../advanced-analytics/r-services/sql-server-r-services.md)   
 [SQL Server R Services 的已知的问题](../../advanced-analytics/r-services/known-issues-for-sql-server-r-services.md)   
 [CREATE EXTERNAL RESOURCE POOL (Transact-SQL)](../../t-sql/statements/create-external-resource-pool-transact-sql.md)   
 [ALTER 外部资源池 &#40;Transact SQL &#41;](../../t-sql/statements/alter-external-resource-pool-transact-sql.md)   
 [DROP WORKLOAD GROUP (Transact-SQL)](../../t-sql/statements/drop-workload-group-transact-sql.md)   
 [删除资源池 &#40;Transact SQL &#41;](../../t-sql/statements/drop-resource-pool-transact-sql.md)  
  
  

