---
title: sp_script_synctran_commands (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_script_synctran_commands
- sp_script_synctran_commands_TSQL
helpviewer_keywords:
- sp_script_synctran_commands
ms.assetid: f132694a-dd05-405b-9d84-21acce9e564a
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: a9ee35eb4c5d67ff50f4f08c1cfa29596e27aec2
ms.sourcegitcommit: c44014af4d3f821e5d7923c69e8b9fb27aeb1afd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/27/2019
ms.locfileid: "58536170"
---
# <a name="spscriptsynctrancommands-transact-sql"></a>sp_script_synctran_commands (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  生成一个包含脚本**sp_addsynctrigger**将应用于在订阅服务器上的可更新订阅的调用。 还有一个**sp_addsynctrigger**调用每篇文章中发布。 在生成的脚本还包含**sp_addqueued_artinfo**创建的调用**MSsubsciption_articles**处理排队的发布所需的表。 在发布服务器上对发布数据库执行此存储的过程。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
sp_script_synctran_commands [@publication = ] 'publication'  
    [ , [@article = ] 'article']  
```  
  
## <a name="arguments"></a>参数  
`[ @publication = ] 'publication'` 是要为其编写脚本的名称。 *发布*是**sysname**，无默认值。  
  
`[ @article = ] 'article'` 是要为其编写脚本的名称。 *文章*是**sysname**，默认值为**所有**，表示指定的所有项目都写入脚本。  
  
## <a name="return-code-values"></a>返回代码值  
 **0** （成功） 或**1** （失败）  
  
## <a name="results-set"></a>结果集  
 **sp_script_synctran_commands**返回一个结果集包含单个**nvarchar(4000)** 列。 该结果集构成的完整脚本创建这两项所需**sp_addsynctrigger**并**sp_addqueued_artinfo**调用要应用于订阅服务器。  
  
## <a name="remarks"></a>备注  
 **sp_script_synctran_commands**快照和事务复制中使用。  
  
 **sp_addqueued_artinfo**用于排队的可更新订阅。  
  
## <a name="permissions"></a>权限  
 只有的成员**sysadmin**固定的服务器角色或**db_owner**固定的数据库角色可以执行**sp_script_synctran_commands**。  
  
## <a name="see-also"></a>请参阅  
 [sp_addsynctriggers &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addsynctriggers-transact-sql.md)   
 [sp_addqueued_artinfo &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addqueued-artinfo-transact-sql.md)   
 [系统存储过程 (Transact-SQL)](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
