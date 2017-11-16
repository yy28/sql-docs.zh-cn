---
title: MSSQL_ENG020572 | Microsoft Docs
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: replication
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords: MSSQL_ENG020572 error
ms.assetid: 636566db-ffcf-4109-8c11-15b8c7cb9cd9
caps.latest.revision: "11"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 24b2c9ebf0a28902610a0c9884589dedc880ef05
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/09/2017
---
# <a name="mssqleng020572"></a>MSSQL_ENG020572
    
## <a name="message-details"></a>消息详细信息  
  
|||  
|-|-|  
|产品名称|SQL Server|  
|事件 ID|20572|  
|事件源|MSSQLSERVER|  
|组件|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|  
|符号名称||  
|消息正文|在验证失败之后，订阅服务器“%s”对发布“%s”中项目“%s”的订阅已被重新初始化。|  
  
## <a name="explanation"></a>解释  
 根据发布服务器上的数据对订阅服务器上的数据进行验证，数据不匹配；因此验证失败。 在指定应该执行的验证时，选择了如果验证失败则应重新初始化订阅的选项。 重新初始化订阅包括在订阅服务器上应用新的快照。 有关验证的详细信息，请参阅 [Validate Replicated Data](../../relational-databases/replication/validate-replicated-data.md)。  
  
## <a name="user-action"></a>用户操作  
 在订阅服务器上应用了新的快照后，发布服务器和订阅服务器上的数据将会匹配。  
  
## <a name="see-also"></a>另请参阅  
 [错误和事件参考（复制）](../../relational-databases/replication/errors-and-events-reference-replication.md)  
  
  
