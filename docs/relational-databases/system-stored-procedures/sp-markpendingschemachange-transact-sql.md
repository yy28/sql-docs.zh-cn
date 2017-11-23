---
title: "sp_markpendingschemachange (Transact SQL) |Microsoft 文档"
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
- sp_markpendingschemachange
- sp_markpendingschemachange_TSQL
helpviewer_keywords: sp_markpendingschemachange
ms.assetid: 01100309-7bef-4154-85bf-f18489577e37
caps.latest.revision: "12"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: fc1712e646a8efda1fdc4f06d912a1021a0beaff
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/21/2017
---
# <a name="spmarkpendingschemachange-transact-sql"></a>sp_markpendingschemachange (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  用于合并发布的可支持性，它通过让管理员跳过所选的挂起架构更改，不复制这些更改。 在发布服务器的发布数据库上执行此存储的过程。  
  
> [!CAUTION]  
>  此存储过程可以导致架构更改不被复制。 只有在尝试了其他方法（例如，重新初始化）之后，或者这些方法的性能开销太大，才用此过程来解决问题。  
  
## <a name="syntax"></a>语法  
  
```  
  
sp_markpendingschemachange [@publication = ] 'publication'  
    [ , [ @schemaversion = ] schemaversion ]  
    [ , [ @status = ] 'status' ]  
```  
  
## <a name="arguments"></a>参数  
 [**@publication=** ] *发布*  
 发布的名称。 *发布*是**sysname**，无默认值。  
  
 [  **@schemaversion=** ] *schemaversion*  
 标识挂起的架构更改。 *schemaversion*是**int**，默认值为**0**。 使用[sp_enumeratependingschemachanges &#40;Transact SQL &#41;](../../relational-databases/system-stored-procedures/sp-enumeratependingschemachanges-transact-sql.md)以列出了对该发布的挂起的架构更改。  
  
 [  **@status=** ] *状态*  
 是否将跳过挂起的架构更改。 *状态*是**nvarchar(10)**默认值为**active**。 如果值*状态*是**跳过**，则将不会复制所选的架构更改。  
  
## <a name="return-code-values"></a>返回代码值  
 **0** （成功） 或**1** （失败）  
  
## <a name="remarks"></a>注释  
 **sp_markpendingschemachange**与合并复制一起使用。  
  
 **sp_markpendingschemachange**是存储的过程适用于合并复制可支持性，并仅当其他纠正措施，例如重新初始化，无法纠正这种情况或过于昂贵中时，才应使用性能的条款。  
  
## <a name="permissions"></a>Permissions  
 只有的成员**sysadmin**固定的服务器角色或**db_owner**固定的数据库角色可以执行**sp_markpendingschemachange**。  
  
## <a name="see-also"></a>另请参阅  
 [sysmergeschemachange &#40;Transact SQL &#41;](../../relational-databases/system-tables/sysmergeschemachange-transact-sql.md)  
  
  
