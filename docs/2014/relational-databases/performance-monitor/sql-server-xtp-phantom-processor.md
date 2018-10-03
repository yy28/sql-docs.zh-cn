---
title: XTP 虚拟处理器 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
ms.assetid: 0f691b3d-a8fd-4459-ad21-2cfc8574a8c0
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: cdbf090eb53f9d67158b8c00ab86386c4a99a023
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2018
ms.locfileid: "48072537"
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
  
  
