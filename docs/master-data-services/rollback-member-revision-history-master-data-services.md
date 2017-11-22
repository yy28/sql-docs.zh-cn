---
title: "回退成员修订历史记录 (Master Data Services) | Microsoft Docs"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-non-specified
ms.prod_service: mds
ms.service: 
ms.component: master-data-services
ms.reviewer: 
ms.suite: sql
ms.technology: master-data-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: d39d3474-20e7-429f-9c8d-fcc4eb0854fc
caps.latest.revision: "5"
author: smartysanthosh
ms.author: nagavo
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 7d361d60514bcd3e63a79c03da52281bd02fcedb
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/20/2017
---
# <a name="rollback-member-revision-history-master-data-services"></a>回退成员修订历史记录 (Master Data Services)
  每当成员发生变化时，系统都会记录成员修订历史记录。 你可以将成员修订历史记录回退到旧版记录。  
  
## <a name="prerequisites"></a>先决条件  
  
-   你必须有权更新选定成员的至少一个属性。 当你回退修订历史记录时，可以更新的所有属性值都会回退到旧版值。  
  
-   仅当实体的事务日志类型是成员时，才会生成修订历史记录。  
  
 **回退成员修订历史记录**  
  
1.  在“主数据管理器”中，单击“资源管理器”。  
  
2.  选择要回退的实体和成员。  
  
3.  单击“查看历史记录”   
  
4.  选择要回退的修订，然后单击“回退” 。  
  
## <a name="see-also"></a>另请参阅  
 [成员修订历史记录 (Master Data Services)](../master-data-services/member-revision-history-master-data-services.md)   
 [更改实体事务日志类型 &#40;Master Data Services&#41;](../master-data-services/change-the-entity-transaction-log-type-master-data-services.md)  
  
  
