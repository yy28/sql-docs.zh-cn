---
title: MSSQLSERVER_32040 | Microsoft Docs
ms.custom: ''
ms.date: 03/08/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- 32040 (Database Engine error)
ms.assetid: 709219b1-f8b2-4696-8923-dd2e91492eb8
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 198a58816388a1f5c80b45b776548508f01a1c73
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "62914265"
---
# <a name="mssqlserver32040"></a>MSSQLSERVER_32040
    
## <a name="details"></a>详细信息  
  
|||  
|-|-|  
|产品名称|SQL Server|  
|事件 ID|32040|  
|事件源|MSSQLSERVER|  
|组件|SQLEngine|  
|符号名称|SQLErrorNum32040|  
|消息正文|引发了 '最早的未发送事务' 警报。 '%d' 的当前值超出了阈值 '%d'。|  
  
## <a name="explanation"></a>解释  
 此数据库镜像事件是对主体服务器实例发出的，指示最早的未发送事务的保留时间已达到了用户指定的阈值。 通常，发生该事件是由于系统的性能已发生变化。 两个系统间的带宽减小或负载增加。  
  
 最早的未发送事务的保留时间是一种性能指标，有助于您估算数据丢失的可能性（以未发送事务的分钟数来衡量）。 此指标特别适用于高性能模式会话。 但是，当镜像因伙伴断开连接而暂停或挂起时，该指标也适用于高安全模式会话。  
  
## <a name="user-action"></a>用户操作  
 检查主体服务器实例和镜像服务器实例上的负荷及其网络连接以查找原因。  
  
## <a name="see-also"></a>请参阅  
 [数据库镜像 (SQL Server)](../../database-engine/database-mirroring/database-mirroring-sql-server.md)   
 [使用镜像性能度量的警告阈值和警报 (SQL Server)](../../database-engine/database-mirroring/use-warning-thresholds-and-alerts-on-mirroring-performance-metrics-sql-server.md)  
  
  
