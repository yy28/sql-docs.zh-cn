---
title: sp_scriptsubconflicttable （Transact-sql） |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_scriptsubconflicttable
- sp_scriptsubconflicttable_TSQL
helpviewer_keywords:
- sp_scriptsubconflicttable
ms.assetid: 13867145-3dad-47a4-8d50-a65175418479
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 32ff25b25b7bf5fb2056196bc91b558beb353f09
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/01/2020
ms.locfileid: "85645295"
---
# <a name="sp_scriptsubconflicttable-transact-sql"></a>sp_scriptsubconflicttable (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/applies-to-version/sqlserver.md)]

  为给定排队订阅项目生成用于在订阅服务器上创建冲突表的脚本。 生成的脚本在订阅服务器的订阅数据库上执行。 此存储过程在发布服务器上对发布数据库执行。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "“主题链接”图标") [Transact-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
sp_scriptsubconflicttable [@publication =] 'publication'    , [@article =] 'article'  
```  
  
## <a name="arguments"></a>自变量  
`[ @publication = ] 'publication'`包含项目的发布的名称。 名称在数据库中必须是唯一的。 *发布*为**sysname**，无默认值。  
  
`[ @article = ] 'article'`订阅项目的名称。 *项目*是**sysname**，无默认值。  
  
## <a name="return-code-values"></a>返回代码值  
 **0** （成功）或**1** （失败）  
  
## <a name="result-sets"></a>结果集  
  
|列名称|数据类型|说明|  
|-----------------|---------------|-----------------|  
|**cmdtext**|**nvarchar(4000)**|为排队订阅项目返回用于在订阅服务器上创建冲突表的 [!INCLUDE[tsql](../../includes/tsql-md.md)] 脚本。 该脚本在订阅服务器的订阅数据库上执行。|  
  
## <a name="remarks"></a>备注  
 **sp_scriptsubconflicttable**用于具有手动应用初始快照的订阅的订阅服务器。 冲突表为订阅服务器上的可选表。  
  
## <a name="permissions"></a>权限  
 只有**sysadmin**固定服务器角色的成员或**db_owner**固定数据库角色的成员才能执行**sp_scriptsubconflicttable**。  
  
## <a name="see-also"></a>另请参阅  
 [排队更新冲突的检测和解决](../../relational-databases/replication/transactional/updatable-subscriptions-queued-updating-conflict-resolution.md)   
 [系统存储过程 (Transact-SQL)](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
