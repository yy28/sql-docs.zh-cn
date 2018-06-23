---
title: XTP 存储 |Microsoft 文档
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- dbe-cross-instance
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 4070580b-880d-4f4c-abcc-626a4fe0c9a2
caps.latest.revision: 3
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 897a3a2e9e3cc592281be87593aa6356ce474c56
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36124074"
---
# <a name="xtp-storage"></a>XTP 存储
  XTP 存储性能对象包含中的 XTP 存储相关的计数器[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。  
  
 下表介绍**XTP 存储**计数器。  
  
|计数器|Description|  
|-------------|-----------------|  
|**Checkpoints Closed**|联机代理执行的已关闭检查点的计数。|  
|**Checkpoints Completed**|脱机检查点线程处理的检查点计数。|  
|**Core Merges Completed**|合并工作线程完成的核心合并数。 仍需要安装这些合并。|  
|**Merge Policy Evaluations**|自服务器启动以来的合并策略评估数。|  
|**Merge Requests Outstanding**|自服务器启动以来未完成的合并请求数。|  
|**Merges Abandoned**|因失败而放弃的合并数。|  
|**Merges Installed**|成功安装的合并数。|  
|**Total Files Merged**|已合并的源文件总数。 此计数可用于查找合并中源文件的平均数目。|  
  
## <a name="see-also"></a>请参阅  
 [XTP&#40;内存中 OLTP&#41;性能计数器](../../integration-services/performance/performance-counters.md)  
  
  