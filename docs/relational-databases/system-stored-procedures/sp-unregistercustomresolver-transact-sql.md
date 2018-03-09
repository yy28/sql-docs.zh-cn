---
title: "sp_unregistercustomresolver (Transact SQL) |Microsoft 文档"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology:
- replication
ms.tgt_pltfrm: 
ms.topic: language-reference
applies_to:
- SQL Server
f1_keywords:
- sp_unregistercustomresolver_TSQL
- sp_unregistercustomresolver
helpviewer_keywords:
- sp_unregistercustomresolver
ms.assetid: 08bd20c8-c6be-4be2-be9f-2b5e1d7bee43
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 831b1004df2d4c62f81e051fb4cdb95e48a97d35
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/21/2017
---
# <a name="spunregistercustomresolver-transact-sql"></a>sp_unregistercustomresolver (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  撤消注册以前注册的业务逻辑模块。 业务逻辑的形式可以是 COM 组件或 [!INCLUDE[msCoName](../../includes/msconame-md.md)] .NET Framework 程序集。 此存储过程在注册自定义业务逻辑的分发服务器中执行。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
sp_unregistercustomresolver [ @article_resolver = ] 'article_resolver'   
```  
  
## <a name="arguments"></a>参数  
 [  **@article_resolver =** ] *article_resolver*  
 指定要注销的自定义业务逻辑的名称。 *article_resolver*是**nvarchar （255)**，无默认值。 如果要删除的业务逻辑是 COM 组件，则该参数是此组件的友好名称。 如果业务逻辑是 .NET Framework 程序集，则该参数是此程序集的名称。  
  
## <a name="return-code-values"></a>返回代码值  
 **0** （成功） 或**1** （失败）  
  
## <a name="remarks"></a>注释  
 **sp_unregistercustomresolver**合并复制中使用。  
  
 使用[sp_enumcustomresolvers](../../relational-databases/system-stored-procedures/sp-enumcustomresolvers-transact-sql.md)在复制拓扑，以将已注册的自定义业务逻辑模块或 COM 冲突解决程序可用的列表返回到拓扑中的任何服务器。  
  
## <a name="permissions"></a>Permissions  
 只有的成员**sysadmin**固定的服务器角色或**db_owner**固定的数据库角色可以执行**sp_unregistercustomresolver**。  
  
## <a name="see-also"></a>另请参阅  
 [sp_lookupcustomresolver &#40;Transact SQL &#41;](../../relational-databases/system-stored-procedures/sp-lookupcustomresolver-transact-sql.md)   
 [sp_registercustomresolver &#40;Transact SQL &#41;](../../relational-databases/system-stored-procedures/sp-registercustomresolver-transact-sql.md)   
 [系统存储过程 (Transact-SQL)](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
