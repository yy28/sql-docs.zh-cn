---
title: "终止查询通知订阅 (Transact SQL) |Microsoft 文档"
ms.custom: 
ms.date: 07/27/2017
ms.prod: sql-non-specified
ms.prod_service: sql-database
ms.service: 
ms.component: t-sql|language-elements
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- KILL QUERY NOTIFICATION SUBSCRIPTION
- KILL_QUERY_NOTIFICATION_SUBSCRIPTION_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- KILL QUERY NOTIFICATION SUBSCRIPTION statement
- removing subscriptions
- subscriptions [SQL Server query notifications], stopping
- query notifications [SQL Server], subscriptions
ms.assetid: 8aeadf51-286c-4748-bef2-d25858b250bf
caps.latest.revision: 17
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 3c6937424d2cd68095952c3faba2a446488e9122
ms.contentlocale: zh-cn
ms.lasthandoff: 09/01/2017

---
# <a name="kill-query-notification-subscription-transact-sql"></a>KILL QUERY NOTIFICATION SUBSCRIPTION (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  从实例中删除查询通知订阅。 该语句可以删除特定订阅或所有订阅。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
KILL QUERY NOTIFICATION SUBSCRIPTION   
   { ALL | subscription_id }  
```  
  
## <a name="arguments"></a>参数  
 ALL  
 删除实例中的所有订阅。  
  
 *subscription_id*  
 删除订阅的订阅 id *subscription_id*。  
  
## <a name="remarks"></a>注释  
 KILL QUERY NOTIFICATION SUBSCRIPTION 语句删除查询通知订阅，而不生成通知消息。  
  
 *subscription_id*是订阅的 id，如动态管理视图中所示[sys.dm_qn_subscriptions &#40;Transact SQL &#41;](../../relational-databases/system-dynamic-management-views/query-notifications-sys-dm-qn-subscriptions.md).  
  
 如果指定的订阅 ID 不存在，该语句将生成错误。  
  
## <a name="permissions"></a>Permissions  
 执行此语句的权限被限制为成员的**sysadmin**固定的服务器角色。  
  
## <a name="examples"></a>示例  
  
### <a name="a-removing-all-query-notification-subscriptions-in-the-instance"></a>A. 删除实例中的所有查询通知订阅  
 下例将删除实例中的所有查询通知订阅。  
  
```  
KILL QUERY NOTIFICATION SUBSCRIPTION ALL ;  
```  
  
### <a name="b-removing-a-single-query-notification-subscription"></a>B. 删除单个查询通知订阅  
 下例将删除 ID 为 `73` 的查询通知订阅。  
  
```  
KILL QUERY NOTIFICATION SUBSCRIPTION 73 ;  
```  
  
## <a name="see-also"></a>另请参阅  
 [sys.dm_qn_subscriptions &#40;Transact SQL &#41;](../../relational-databases/system-dynamic-management-views/query-notifications-sys-dm-qn-subscriptions.md)  
  
  

