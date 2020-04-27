---
title: XTP 存储 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
ms.assetid: 4070580b-880d-4f4c-abcc-626a4fe0c9a2
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 50e62a9232690deb368096723f428118e9de7aa2
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/26/2020
ms.locfileid: "63151156"
---
# <a name="xtp-storage"></a>XTP 存储
  XTP 存储性能对象包含与 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中的 XTP 存储相关的计数器。  
  
 下表介绍了**XTP 存储**计数器。  
  
|计数器|说明|  
|-------------|-----------------|  
|**Checkpoints Closed**|联机代理执行的已关闭检查点的计数。|  
|**Checkpoints Completed**|脱机检查点线程处理的检查点计数。|  
|**Core Merges Completed**|合并工作线程完成的核心合并数。 仍需要安装这些合并。|  
|**Merge Policy Evaluations**|自服务器启动以来的合并策略评估数。|  
|**Merge Requests Outstanding**|自服务器启动以来未完成的合并请求数。|  
|**Merges Abandoned**|因失败而放弃的合并数。|  
|**Merges Installed**|成功安装的合并数。|  
|**Total Files Merged**|已合并的源文件总数。 此计数可用于查找合并中源文件的平均数目。|  
  
## <a name="see-also"></a>另请参阅  
 [XTP &#40;内存中 OLTP&#41; 性能计数器](../../integration-services/performance/performance-counters.md)  
  
  
