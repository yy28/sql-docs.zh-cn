---
title: "禁用轻型池 | Microsoft Docs"
ms.custom: 
ms.date: 08/09/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: performance-monitor
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords: Best Practices [Database Engine]
ms.assetid: 481bb43d-6fe5-497c-9096-971fb6bf733b
caps.latest.revision: "13"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 641090022517c5bae1cb0a3040de9216c9dd36a1
ms.sourcegitcommit: 2208a909ab09af3b79c62e04d3360d4d9ed970a7
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/02/2018
---
# <a name="disable-lightweight-pooling"></a>禁用轻型池
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]此规则检查服务器上是否已禁用轻型池。 将 lightweightpooling 设置为 1 将使 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 切换到纤程模式计划。 纤程模式专用于 UMS 工作线程的上下文切换是性能的主要瓶颈的某些情况。 由于这种情况很少出现，所以纤程模式很少提高典型系统上的性能或可伸缩性。  
  
## <a name="best-practices-recommendations"></a>最佳做法建议  
 lightweightpooling 选项应仅在以下情况下启用：进行彻底的测试之后、评估所有其他性能优化机会之后，以及上下文切换在您的环境中是已知问题时。  
  
 建议您不要使用纤程模式计划日常操作，这是因为它会抑制上下文切换优势的正常发挥，并且使用线程本地存储区 (TLS) 或线程所有的对象（如互斥体，一种 Win32 内核对象）的某些 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 组件在纤程模式下无法正常工作  
  
 若要删除轻型池，请执行下面的语句，然后重新启动 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]。  
  
```sql  
sp_configure 'show advanced options', 1;  
GO  
sp_configure 'lightweight pooling', 0;  
GO  
RECONFIGURE;  
GO  
```  
  
## <a name="for-more-information"></a>有关详细信息  
 [lightweight pooling 服务器配置选项](../../database-engine/configure-windows/lightweight-pooling-server-configuration-option.md)  
  
## <a name="see-also"></a>另请参阅  
 [使用基于策略的管理来监视和强制执行最佳实践](../../relational-databases/policy-based-management/monitor-and-enforce-best-practices-by-using-policy-based-management.md)  
  
  
