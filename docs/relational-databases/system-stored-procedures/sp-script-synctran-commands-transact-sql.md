---
title: sp_script_synctran_commands (Transact SQL) |Microsoft 文档
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology:
- replication
ms.tgt_pltfrm: ''
ms.topic: language-reference
applies_to:
- SQL Server
f1_keywords:
- sp_script_synctran_commands
- sp_script_synctran_commands_TSQL
helpviewer_keywords:
- sp_script_synctran_commands
ms.assetid: f132694a-dd05-405b-9d84-21acce9e564a
caps.latest.revision: 27
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: 3705a28d85c7375aad701d77a517719778954c25
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
ms.locfileid: "32997754"
---
# <a name="spscriptsynctrancommands-transact-sql"></a>sp_script_synctran_commands (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  生成脚本，其中包含**sp_addsynctrigger**调用在订阅服务器上应用于可更新订阅。 还有一个**sp_addsynctrigger**调用为每篇文章中发布。 生成的脚本还包含**sp_addqueued_artinfo**创建调用**MSsubsciption_articles**处理排队的发布所需的表。 在发布服务器的发布数据库上执行此存储的过程。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
sp_script_synctran_commands [@publication = ] 'publication'  
    [ , [@article = ] 'article']  
```  
  
## <a name="arguments"></a>参数  
 [ **@publication** = ] **'***publication***'**  
 要写入脚本的发布的名称。 *发布*是**sysname**，无默认值。  
  
 [ **@article** =] *****文章*****  
 要写入脚本的项目的名称。 *文章*是**sysname**，默认值为**所有**，它指定所有项目脚本。  
  
## <a name="return-code-values"></a>返回代码值  
 **0** （成功） 或**1** （失败）  
  
## <a name="results-set"></a>结果集  
 **sp_script_synctran_commands**返回一个结果集包含单个**nvarchar （4000)** 列。 结果设置窗体的完整脚本所必需的创建这两项**sp_addsynctrigger**和**sp_addqueued_artinfo**调用在订阅服务器上应用。  
  
## <a name="remarks"></a>注释  
 **sp_script_synctran_commands**快照和事务复制中使用。  
  
 **sp_addqueued_artinfo**用于排队更新订阅。  
  
## <a name="permissions"></a>权限  
 只有的成员**sysadmin**固定的服务器角色或**db_owner**固定的数据库角色可以执行**sp_script_synctran_commands**。  
  
## <a name="see-also"></a>另请参阅  
 [sp_addsynctriggers &#40;Transact SQL&#41;](../../relational-databases/system-stored-procedures/sp-addsynctriggers-transact-sql.md)   
 [sp_addqueued_artinfo &#40;Transact SQL&#41;](../../relational-databases/system-stored-procedures/sp-addqueued-artinfo-transact-sql.md)   
 [系统存储过程 (Transact-SQL)](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
