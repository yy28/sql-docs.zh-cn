---
title: "选择冲突解决程序 | Microsoft Docs"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: replication
ms.reviewer: 
ms.suite: sql
ms.technology: replication
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- default conflict resolver
- articles [SQL Server replication], conflict resolution
- conflict resolution [SQL Server replication], merge replication
ms.assetid: b7dec3fa-d9d9-409d-b946-f9b9a3202829
caps.latest.revision: "33"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 02e8f1043c8b3337953dd300c67ad0d94343eb88
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/17/2017
---
# <a name="advanced-merge-replication-conflict---choose-a-resolver"></a>高级合并复制冲突 - 选择解决程序
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]在选择冲突解决程序时，请考虑冲突解决在应用程序中的重要性，以及是否可以使用基于优先级的默认冲突解决程序或是否需要使用项目冲突解决程序。  
  
 如果数据是分区的，没有多用户写入相同的分区，并且复制拓扑也相对简单（一个发布服务器和几个订阅服务器），则冲突将极少发生或根本不存在冲突。 在这些环境中，可能不需要复杂的冲突解决策略。 推荐使用默认冲突解决设置，即使用客户端订阅和首次更改入选的策略。 如果拓扑较复杂（例如，使用重新发布订阅服务器），则具有特定优先级的服务器订阅可能比较合适。  
  
 如果业务需求所要求比默认冲突解决程序更精细优化的解决方案，则建议使用项目冲突解决程序。 如果选择使用项目冲突解决程序，则建议使用业务逻辑处理程序。 有关详细信息，请参阅[合并同步期间执行业务逻辑](../../../relational-databases/replication/merge/execute-business-logic-during-merge-synchronization.md)。  
  
 总之，要根据数据和应用程序的业务逻辑需要来选择使用默认冲突解决程序还是使用项目冲突解决程序。 例如，假设雇员向不同订阅服务器上的一组未分区表输入客户排名数据，雇员跨多个工作类别（分公司经理、产品经理、销售人员），并且工作类别决定谁的数据具有优先级。 这种情况下，可以生成一个项目冲突解决程序，使用项目的工作类别数据确定发生冲突时的入选方。  
  
 如果冲突有可能频繁发生，下面列出了实施冲突解决策略时应考虑的最重要的决定。  
  
|冲突解决问题|建议|  
|-------------------------------|--------------------|  
|不同类别的用户要求不同的优先级值。|使用默认冲突解决程序并创建具有不同优先级值的服务器订阅。<br /><br /> 或<br /><br /> 使用可以识别项目中授权值列的项目冲突解决程序帮助解决冲突。|  
|要求首次更改入选冲突解决方案。|使用默认冲突解决程序并创建客户端订阅。|  
|允许多个用户更改同一数据行，条件是不对同一列进行有冲突的更改。|使用启用了列级跟踪的默认冲突解决程序或项目冲突解决程序。|  
|将对行内任意值的多次更改标记为冲突。|使用具有行级跟踪的默认冲突解决程序或项目冲突解决程序。|  
|将对逻辑记录中任意值的多次更改标记为冲突。|使用具有逻辑记录级跟踪的默认冲突解决程序（逻辑记录功能不支持自定义冲突解决程序或业务逻辑处理程序）。|  
|冲突解决结果数据应该与原始冲突数据不同。|使用计算新值的项目冲突解决程序。|  
  
## <a name="see-also"></a>另请参阅  
 [检测并解决逻辑记录中的冲突](../../../relational-databases/replication/merge/advanced-merge-replication-conflict-resolving-in-logical-record.md)   
 [高级合并复制冲突检测和解决](../../../relational-databases/replication/merge/advanced-merge-replication-conflict-detection-and-resolution.md)   
 [重新发布数据](../../../relational-databases/replication/republish-data.md)  
  
  
