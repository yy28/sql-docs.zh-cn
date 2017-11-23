---
title: "sp_adjustpublisheridentityrange (Transact SQL) |Microsoft 文档"
ms.custom: 
ms.date: 03/04/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology: replication
ms.tgt_pltfrm: 
ms.topic: language-reference
applies_to: SQL Server
f1_keywords:
- sp_adjustpublisheridentityrange_TSQL
- sp_adjustpublisheridentityrange
helpviewer_keywords: sp_adjustpublisheridentityrange
ms.assetid: 64f111fd-fb7d-4459-93f7-65f0f8dd7efe
caps.latest.revision: "28"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: c2f0214309eb060bbc02c7c05bf5243444ed5796
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/21/2017
---
# <a name="spadjustpublisheridentityrange-transact-sql"></a>sp_adjustpublisheridentityrange (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  调整发布上的标识范围，并根据发布上的阈值重新分配新的范围。 在发布服务器的发布数据库上执行此存储的过程。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
sp_adjustpublisheridentityrange [ [ @publication = ] 'publication' ]  
    [ , [ @table_name = ] 'table_name' ]  
    [ , [ @table_owner= ] 'table_owner' ]  
```  
  
## <a name="arguments"></a>参数  
 [  **@publication=**] *发布*  
 重新分配新标识范围的发布的名称。 *发布*是**sysname**，默认值为 NULL。  
  
 [  **@table_name=**] *table_name*  
 重新分配新标识范围的表的名称。 *table_name*是**sysname**，默认值为 NULL。  
  
 [  **@table_owner=**] *table_owner*  
 发布服务器上表的所有者。 *table_owner*是**sysname**，默认值为 NULL。 如果*table_owner*未指定，则使用当前用户的名称。  
  
## <a name="return-code-values"></a>返回代码值  
 **0** （成功） 或**1** （失败）  
  
## <a name="remarks"></a>注释  
 **sp_adjustpublisheridentityrange**在所有类型的复制中使用。  
  
 对于已启用自动标识范围的发布，分发代理或合并代理负责基于发布的阈值自动调整发布的标识范围。 但是，如果出于某种原因分发代理或合并代理未运行的一段时间，并且标识范围资源具有已消耗很大程度的阈值的点，则用户可以调用**sp_adjustpublisheridentityrange**若要为发布服务器分配新范围的值。  
  
 在执行时**sp_adjustpublisheridentityrange**，*发布*或*table_name*必须指定。 如果同时指定了这两个参数或二者都未指定，则将返回错误。  
  
## <a name="permissions"></a>Permissions  
 只有的成员**sysadmin**固定的服务器角色或**db_owner**固定的数据库角色可以执行**sp_adjustpublisheridentityrange**。  
  
## <a name="see-also"></a>另请参阅  
 [复制标识列](../../relational-databases/replication/publish/replicate-identity-columns.md)   
 [系统存储过程 (Transact-SQL)](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
