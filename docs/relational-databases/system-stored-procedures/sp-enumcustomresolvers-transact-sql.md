---
title: sp_enumcustomresolvers (Transact SQL) |Microsoft 文档
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
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
- sp_enumcustomresolvers
- sp_enumcustomresolvers_TSQL
helpviewer_keywords:
- sp_enumcustomresolvers
ms.assetid: 81bd0d3a-48dc-42b1-b662-c630f61fc630
caps.latest.revision: 22
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 6dc8d6e66218bac271f5475d27e24e529efc92dd
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/16/2018
---
# <a name="spenumcustomresolvers-transact-sql"></a>sp_enumcustomresolvers (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  返回所有可用的业务逻辑处理程序以及在分发服务器上注册的自定义冲突解决程序的列表。 此存储过程在发布服务器的任何数据库中执行。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
sp_enumcustomresolvers [ [ @distributor =] 'distributor']  
```  
  
## <a name="arguments"></a>参数  
 [  **@distributor =**] *****分发服务器*****  
 自定义冲突解决程序所在的分发服务器的名称。 *分发服务器*是**sysname**，默认值为 NULL。 *此参数已弃用，将从未来版本中删除。*  
  
## <a name="result-sets"></a>结果集  
  
|列名|数据类型|Description|  
|-----------------|---------------|-----------------|  
|**article_resolver**|**nvarchar(255)**|业务逻辑处理程序或冲突解决程序的友好名称。|  
|**resolver_clsid**|**nvarchar(50)**|基于 COM 的冲突解决程序的类 ID (CLSID)。 对于业务逻辑处理程序，此列返回 CLSID 值 0。|  
|**is_dotnet_assembly**|**bit**|指示注册是否针对业务逻辑处理程序。<br /><br /> **0** = 基于 COM 的冲突解决程序<br /><br /> **1** = 业务逻辑处理程序|  
|**dotnet_assembly_name**|**nvarchar(255)**|实现业务逻辑处理程序的 [!INCLUDE[msCoName](../../includes/msconame-md.md)] .NET Framework 程序集的名称。|  
|**dotnet_class_name**|**nvarchar(255)**|实现业务逻辑处理程序时优先级高于 <xref:Microsoft.SqlServer.Replication.BusinessLogicSupport.BusinessLogicModule> 的类的名称。|  
  
## <a name="return-code-values"></a>返回代码值  
 **0** （成功） 或**1** （失败）  
  
## <a name="remarks"></a>注释  
 **sp_enumcustomresolvers**合并复制中使用。  
  
## <a name="permissions"></a>权限  
 只有的成员**sysadmin**固定的服务器角色和**db_owner**固定的数据库角色可以执行**sp_enumcustomresolvers**。  
  
## <a name="see-also"></a>另请参阅  
 [为合并项目实现业务逻辑处理程序](../../relational-databases/replication/implement-a-business-logic-handler-for-a-merge-article.md)   
 [为合并项目实现自定义冲突解决程序](../../relational-databases/replication/implement-a-custom-conflict-resolver-for-a-merge-article.md)   
 [sp_lookupcustomresolver &#40;Transact SQL&#41;](../../relational-databases/system-stored-procedures/sp-lookupcustomresolver-transact-sql.md)   
 [sp_unregistercustomresolver &#40;Transact SQL&#41;](../../relational-databases/system-stored-procedures/sp-unregistercustomresolver-transact-sql.md)   
 [系统存储过程 (Transact-SQL)](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
