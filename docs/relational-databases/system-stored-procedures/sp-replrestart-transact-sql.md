---
title: sp_replrestart (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_replrestart_TSQL
- sp_replrestart
helpviewer_keywords:
- sp_replrestart
ms.assetid: 111b3dbf-92f8-4670-b156-1468c63e4fc1
author: stevestein
ms.author: sstein
ms.openlocfilehash: fc15ed0b36738968a2b455157213a10dbceb2965
ms.sourcegitcommit: ef7834ed0f38c1712f45737018a0bfe892e894ee
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/17/2019
ms.locfileid: "68300449"
---
# <a name="spreplrestart-transact-sql"></a>sp_replrestart (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  由事务复制在备份和还原过程中使用，以使分发服务器上的复制数据与发布服务器上的数据同步。 此存储过程在发布服务器上对发布数据库执行。  
  
> [!IMPORTANT]  
>  **sp_replrestart**是一个内部复制存储过程, 仅应在还原事务复制拓扑中发布的数据库时使用, 如[有关备份和还原快照的策略中所述。事务复制](../../relational-databases/replication/administration/strategies-for-backing-up-and-restoring-snapshot-and-transactional-replication.md)。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
sp_replrestart  
```  
  
## <a name="return-code-values"></a>返回代码值  
 **0** (成功) 或**1** (失败)  
  
## <a name="remarks"></a>备注  
 当分发服务器上的最高日志序列号 (LSN) 值与发布服务器上的最高 LSN 值不匹配时, 将使用**sp_replrestart** 。  
  
## <a name="permissions"></a>权限  
 只有**sysadmin**固定服务器角色的成员或**db_owner**固定数据库角色的成员才能执行**sp_replrestart**。  
  
## <a name="see-also"></a>请参阅  
 [复制存储过程 (Transact-SQL)](../../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md)  
  
  
