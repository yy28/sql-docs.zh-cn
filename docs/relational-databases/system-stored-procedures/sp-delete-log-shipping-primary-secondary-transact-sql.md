---
title: "sp_delete_log_shipping_primary_secondary (Transact SQL) |Microsoft 文档"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sp_delete_log_shipping_primary_secondary_TSQL
- sp_delete_log_shipping_primary_secondary
dev_langs:
- TSQL
helpviewer_keywords:
- sp_delete_log_shipping_primary_secondary
ms.assetid: d6f71a12-f7b1-4a1c-9639-a533b8287b0c
caps.latest.revision: 
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 3e8946935b8f3f81e4d59c90724807862e0ccca7
ms.sourcegitcommit: c556eaf60a49af7025db35b7aa14beb76a8158c5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/03/2018
---
# <a name="spdeletelogshippingprimarysecondary-transact-sql"></a>sp_delete_log_shipping_primary_secondary (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  删除主服务器上的辅助数据库项。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
sp_delete_log_shipping_primary_secondary  
    [ @primary_database = ] 'primary_database',   
    [ @secondary_server = ] 'secondary_server',   
    [ @secondary_database = ] 'secondary_database'  
```  
  
## <a name="arguments"></a>参数  
 [ **@primary_database =** ] **'***primary_database***'**  
 主服务器上的数据库的名称。 *primary_database*是**sysname**，无默认值。  
  
 [ **@secondary_server =** ] **'***secondary_server***'**  
 辅助服务器的名称。 *secondary_server*是**sysname**，无默认值。  
  
 [ **@secondary_database =** ] **'***secondary_database***'**  
 辅助数据库的名称。 *secondary_database*是**sysname**，无默认值。  
  
## <a name="return-code-values"></a>返回代码值  
 0（成功）或 1（失败）  
  
## <a name="result-sets"></a>结果集  
 无。  
  
## <a name="remarks"></a>注释  
 **sp_delete_log_shipping_primary_secondary**必须从运行**master**主服务器上的数据库。 此存储的过程将删除从辅助数据库的条目**log_shipping_primary_secondaries**主服务器上。  
  
## <a name="permissions"></a>权限  
 要求具有 **sysadmin** 固定服务器角色的成员身份。  
  
## <a name="examples"></a>示例  
 以下示例中，使用 `sp_delete_log_shipping_primary_secondary` 从辅助服务器 `LogShipAdventureWorks` 上删除辅助数据库 `FLATIRON`。  
  
```  
EXEC master.dbo.sp_delete_log_shipping_primary_secondary  
@primary_database = N'AdventureWorks'  
,@secondary_server = N'FLATIRON'  
,@secondary_database = N'LogShipAdventureWorks';  
GO  
```  
  
## <a name="see-also"></a>另请参阅  
 [有关日志传送 &#40;SQL server&#41;](../../database-engine/log-shipping/about-log-shipping-sql-server.md)   
 [系统存储过程 (Transact-SQL)](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
