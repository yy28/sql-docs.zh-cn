---
title: sp_unregistercustomresolver （Transact-sql） |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_unregistercustomresolver_TSQL
- sp_unregistercustomresolver
helpviewer_keywords:
- sp_unregistercustomresolver
ms.assetid: 08bd20c8-c6be-4be2-be9f-2b5e1d7bee43
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 8a3d53367412251d553aa71a8085b50421624cc7
ms.sourcegitcommit: 4d3896882c5930248a6e441937c50e8e027d29fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/05/2020
ms.locfileid: "82820186"
---
# <a name="sp_unregistercustomresolver-transact-sql"></a>sp_unregistercustomresolver (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  撤消注册以前注册的业务逻辑模块。 业务逻辑的形式可以是 COM 组件或 [!INCLUDE[msCoName](../../includes/msconame-md.md)] .NET Framework 程序集。 此存储过程在注册自定义业务逻辑的分发服务器中执行。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "“主题链接”图标") [Transact-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
sp_unregistercustomresolver [ @article_resolver = ] 'article_resolver'   
```  
  
## <a name="arguments"></a>参数  
`[ @article_resolver = ] 'article_resolver'`指定正在注销的自定义业务逻辑的名称。 *article_resolver*为**nvarchar （255）**，无默认值。 如果要删除的业务逻辑是 COM 组件，则该参数是此组件的友好名称。 如果业务逻辑是 .NET Framework 程序集，则该参数是此程序集的名称。  
  
## <a name="return-code-values"></a>返回代码值  
 **0** （成功）或**1** （失败）  
  
## <a name="remarks"></a>备注  
 **sp_unregistercustomresolver**用于合并复制。  
  
 在复制拓扑中的任何服务器上使用[sp_enumcustomresolvers](../../relational-databases/system-stored-procedures/sp-enumcustomresolvers-transact-sql.md) ，以返回已注册的自定义业务逻辑模块或可用于拓扑的 COM 解析器的列表。  
  
## <a name="permissions"></a>权限  
 只有**sysadmin**固定服务器角色的成员或**db_owner**固定数据库角色的成员才能执行**sp_unregistercustomresolver**。  
  
## <a name="see-also"></a>另请参阅  
 [sp_lookupcustomresolver &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-lookupcustomresolver-transact-sql.md)   
 [sp_registercustomresolver &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-registercustomresolver-transact-sql.md)   
 [系统存储过程 (Transact-SQL)](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
