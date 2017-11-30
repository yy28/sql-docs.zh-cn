---
title: "sp_bindsession (TRANSACT-SQL) |Microsoft 文档"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sp_bindsession
- sp_bindsession_TSQL
dev_langs: TSQL
helpviewer_keywords: sp_bindsession
ms.assetid: 1436fe21-ad00-4a98-aca1-1451a5e571d2
caps.latest.revision: "38"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 28023afe6fa8440764bacab40ad3bca49b54611a
ms.sourcegitcommit: 9fbe5403e902eb996bab0b1285cdade281c1cb16
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/27/2017
---
# <a name="spbindsession-transact-sql"></a>sp_bindsession (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  绑定或取消绑定到同一实例中的其他会话的会话[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssDE](../../includes/ssde-md.md)]。 绑定会话允许两个或更多的会话参与同一事务并共享锁，直到发出 ROLLBACK TRANSACTION 或 COMMIT TRANSACTION 命令。  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)] 请改用多个活动结果集 (MARS) 或分布式事务。 有关详细信息，请参阅[使用多个活动结果集 &#40;MARS &#41;](../../relational-databases/native-client/features/using-multiple-active-result-sets-mars.md).  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
sp_bindsession { 'bind_token' | NULL }  
```  
  
## <a name="arguments"></a>参数  
  *bind_token*   
 标记，用于标识该事务最初使用获取**sp_getbindtoken**或开放式数据服务**srv_getbindtoken**函数。 *bind_token*是**varchar(255)**。  
  
## <a name="return-code-values"></a>返回代码值  
 0（成功）或 1（失败）  
  
## <a name="remarks"></a>注释  
 绑定的两个会话只共享事务和锁。 每个会话均保留自身的隔离级别，在一个会话上设置新的隔离级别不会影响另一个会话的隔离级别。 每个会话仍由其安全帐户标识，且只能访问已授权该帐户访问的数据库资源。  
  
 **sp_bindsession**使用的绑定令牌来将两个或多个现有的客户端会话的绑定。 这些客户端会话必须位于获得绑定令牌的同一[!INCLUDE[ssDE](../../includes/ssde-md.md)]实例中。 会话是执行命令的客户端。 绑定数据库会话共享事务和锁空间。  
  
 从一个[!INCLUDE[ssDE](../../includes/ssde-md.md)]实例获得的绑定令牌不能用于连接到另一实例的客户端会话，甚至对 DTC 事务也是如此。 绑定令牌仅在每个实例的本地有效，不能由多个实例共享。 若要将客户端会话绑定上的另一个实例[!INCLUDE[ssDE](../../includes/ssde-md.md)]，你必须执行以获取不同的绑定令牌**sp_getbindtoken**。  
  
 **sp_bindsession**如果它使用处于非活动状态的令牌将失败并出错。  
  
 从会话可通过使用取消绑定**sp_bindsession**而无需指定*bind_token*或通过传递 NULL *bind_token*。  
  
## <a name="permissions"></a>Permissions  
 要求 **公共** 角色具有成员身份。  
  
## <a name="examples"></a>示例  
 以下示例将指定的绑定令牌绑定到当前会话。  
  
> [!NOTE]  
>  示例所示的绑定令牌获取通过执行**sp_getbindtoken**之前执行**sp_bindsession**。  
  
```  
USE master;  
GO  
EXEC sp_bindsession 'BP9---5---->KB?-V'<>1E:H-7U-]ANZ';  
GO  
```  
  
## <a name="see-also"></a>另请参阅  
 [sp_getbindtoken &#40;Transact SQL &#41;](../../relational-databases/system-stored-procedures/sp-getbindtoken-transact-sql.md)   
 [srv_getbindtoken &#40;扩展存储的过程 API &#41;](../../relational-databases/extended-stored-procedures-reference/srv-getbindtoken-extended-stored-procedure-api.md)   
 [系统存储过程 (Transact-SQL)](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
