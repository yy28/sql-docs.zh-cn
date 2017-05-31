---
title: MSSQL_ENG014157 | Microsoft Docs
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- replication
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- MSSQL_ENG014157 error
ms.assetid: 1a0890cf-d977-43e0-a2ba-9c5ff1a8f856
caps.latest.revision: 17
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 43d1554f54c46787bfff9dd4bd7c34d5d0410ba1
ms.contentlocale: zh-cn
ms.lasthandoff: 04/11/2017

---
# <a name="mssqleng014157"></a>MSSQL_ENG014157
    
## <a name="message-details"></a>消息详细信息  
  
|||  
|-|-|  
|产品名称|SQL Server|  
|事件 ID|14157|  
|事件源|MSSQLSERVER|  
|组件|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|  
|符号名称||  
|消息正文|由发布 '%s' 的订阅服务器 '%s' 创建的订阅已过期，且已停止。|  
  
## <a name="explanation"></a>解释  
 订阅服务器在指定的发布保持期内必须与发布服务器同步。 如果订阅服务器在此期间内没有同步，则该订阅将过期。 有关详细信息，请参阅 [Subscription Expiration and Deactivation](../../relational-databases/replication/subscription-expiration-and-deactivation.md)。  
  
## <a name="user-action"></a>用户操作  
 必须先重新创建和初始化订阅，订阅服务器才可以再次接收数据更改：  
  
-   有关创建订阅的信息，请参阅[订阅发布](../../relational-databases/replication/subscribe-to-publications.md)。  
  
-   有关初始化订阅的信息，请参阅[初始化订阅](../../relational-databases/replication/initialize-a-subscription.md)。  
  
 如果订阅数据库包含尚未与发布服务器同步的更改，则可以使用 [tablediff Utility](../../tools/tablediff-utility.md) 来确定发布和订阅数据库中的哪些行不同。  
  
 可以延长发布保持期来避免订阅过期。 请谨慎设置较高的值，因为这可能导致存储更多的数据和元数据，从而影响性能。 有关详细信息，请参阅 [Subscription Expiration and Deactivation](../../relational-databases/replication/subscription-expiration-and-deactivation.md)。  
  
## <a name="see-also"></a>另请参阅  
 [错误和事件参考（复制）](../../relational-databases/replication/errors-and-events-reference-replication.md)  
  
  
