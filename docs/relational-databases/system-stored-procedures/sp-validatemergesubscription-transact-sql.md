---
title: sp_validatemergesubscription (TRANSACT-SQL) |Microsoft Docs
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
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 8ddf4c57901682cb099dc0e92c09b763651e32f6
ms.sourcegitcommit: 7aa6beaaf64daf01b0e98e6c63cc22906a77ed04
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/09/2019
ms.locfileid: "54131707"
---
# <a name="spvalidatemergesubscription-transact-sql"></a>sp_validatemergesubscription (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  执行对指定订阅的验证。 在发布服务器上对发布数据库执行此存储的过程。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
sp_validatemergesubscription [@publication=] 'publication'  
        , [ @subscriber = ] 'subscriber'  
        , [ @subscriber_db = ] 'subscriber_db'  
        , [ @level = ] level  
```  
  
## <a name="arguments"></a>参数  
 [**@publication=**] **'***发布***’**  
 发布的名称。 *发布*是**sysname**，无默认值。  
  
 [  **@subscriber=** ] **'***订阅服务器***’**  
 订阅服务器的名称。 *订阅服务器上*是**sysname**，无默认值。  
  
 [  **@subscriber_db=** ] **'***subscriber_db***’**  
 是订阅数据库的名称。 *subscriber_db*是**sysname**，无默认值。  
  
 [  **@level=** ]*级别*  
 要执行的验证类型。 *级别*是**tinyint**，无默认值。 级别可以为下列值之一：  
  
|级别值|Description|  
|-----------------|-----------------|  
|**1**|只验证行计数。|  
|**2**|验证行计数和校验和。|  
|**3**|验证行计数和二进制校验值。|  
  
## <a name="return-code-values"></a>返回代码值  
 **0** （成功） 或**1** （失败）  
  
## <a name="remarks"></a>备注  
 **sp_validatemergesubscription**合并复制中使用。  
  
## <a name="permissions"></a>权限  
 只有的成员**sysadmin**固定的服务器角色或**db_owner**固定的数据库角色可以执行**sp_validatemergesubscription**。  
  
## <a name="see-also"></a>请参阅  
 [复制存储过程 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md)   
 [验证复制的数据](../../relational-databases/replication/validate-data-at-the-subscriber.md)   
 [sp_validatemergepublication &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-validatemergepublication-transact-sql.md)  
  
  
