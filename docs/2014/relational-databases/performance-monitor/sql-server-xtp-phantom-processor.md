---
title: XTP 虚拟处理器 |Microsoft 文档
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- dbe-cross-instance
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 0f691b3d-a8fd-4459-ad21-2cfc8574a8c0
caps.latest.revision: 4
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: bc489c0fc5be77e8dfaf2d2ea11a10515ec460e8
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36029000"
---
# <a name="xtp-phantom-processor"></a>XTP 虚拟处理器
  XTP 虚拟处理器性能对象包含与 XTP 引擎的虚拟处理子系统相关的计数器。 此组件用于检测在 SERIALIZABLE 隔离级别运行的事务中的虚拟行。  
  
 下表介绍**XTP 虚拟处理器**计数器。  
  
|计数器|Description|  
|-------------|-----------------|  
|**灰尘角扫描重试次数/秒（虚拟发出）**|在虚拟处理器发出的灰尘角扫描期间，由于写冲突而进行的每秒扫描重试次数（平均值）。 此为非常低级的计数器，不适合客户使用。|  
|**删除的虚拟过期行数/秒**|虚拟扫描每秒删除的过期行数（平均值）。|  
|**接触的虚拟过期行数/秒**|虚拟扫描每秒接触的过期行数（平均值）。|  
|**接触的即将到期的虚拟行数/秒**|虚拟扫描每秒接触的即将到期的行数（平均值）。|  
|**接触的虚拟行数/秒**|虚拟扫描每秒接触的行数（平均值）。|  
|**启动的虚拟扫描数/秒**|每秒启动的虚拟扫描数（平均值）。|  
  
## <a name="see-also"></a>请参阅  
 [XTP&#40;内存中 OLTP&#41;性能计数器](../../integration-services/performance/performance-counters.md)  
  
  