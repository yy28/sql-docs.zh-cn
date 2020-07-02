---
title: sp_validatemergesubscription （Transact-sql） |Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_validatemergesubscription
- sp_validatemergesubscription_TSQL
helpviewer_keywords:
- sp_validatemergesubscription
ms.assetid: d73ad03c-e5b3-4606-a0ee-7d75e12762a6
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 4dff385d9ada2d403979a4f605b86d0bfd4a3166
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/01/2020
ms.locfileid: "85722998"
---
# <a name="sp_validatemergesubscription-transact-sql"></a>sp_validatemergesubscription (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/applies-to-version/sqlserver.md)]

  执行对指定订阅的验证。 此存储过程在发布服务器上对发布数据库执行。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "“主题链接”图标") [Transact-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
sp_validatemergesubscription [@publication=] 'publication'  
        , [ @subscriber = ] 'subscriber'  
        , [ @subscriber_db = ] 'subscriber_db'  
        , [ @level = ] level  
```  
  
## <a name="arguments"></a>自变量  
`[ @publication = ] 'publication'`发布的名称。 *发布*为**sysname**，无默认值。  
  
`[ @subscriber = ] 'subscriber'`订阅服务器的名称。 *订阅服务器*的**sysname**，无默认值。  
  
`[ @subscriber_db = ] 'subscriber_db'`订阅数据库的名称。 *subscriber_db* **sysname**，无默认值。  
  
`[ @level = ] 'level'`要执行的验证的类型。 *级别*为**tinyint**，无默认值。 级别可以为下列值之一：  
  
|级别值|说明|  
|-----------------|-----------------|  
|**1**|只验证行计数。|  
|**2**|验证行计数和校验和。|  
|**3**|验证行计数和二进制校验值。|  
  
## <a name="return-code-values"></a>返回代码值  
 **0** （成功）或**1** （失败）  
  
## <a name="remarks"></a>备注  
 **sp_validatemergesubscription**用于合并复制。  
  
## <a name="permissions"></a>权限  
 只有**sysadmin**固定服务器角色的成员或**db_owner**固定数据库角色的成员才能执行**sp_validatemergesubscription**。  
  
## <a name="see-also"></a>另请参阅  
 [复制存储过程 &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md)   
 [验证复制的数据](../../relational-databases/replication/validate-data-at-the-subscriber.md)   
 [sp_validatemergepublication &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-validatemergepublication-transact-sql.md)  
  
  
