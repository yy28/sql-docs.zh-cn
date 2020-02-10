---
title: MSSQLSERVER_32042 | Microsoft Docs
ms.custom: ''
ms.date: 03/08/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- 32042 (Database Engine error)
ms.assetid: 53a51c7a-dcd4-4c15-b4d2-6aaa9dce76da
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: b28d7b461d73cb6b65678b385e1572e717420854
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "62914769"
---
# <a name="mssqlserver_32042"></a>MSSQLSERVER_32042
    
## <a name="details"></a>详细信息  
  
|||  
|-|-|  
|产品名称|SQL Server|  
|事件 ID|32042|  
|事件源|MSSQLSERVER|  
|组件|SQLEngine|  
|符号名称|SQLErrorNum32042|  
|消息正文|引发了 '未发送日志' 警报。 '%d' 的当前值超出了阈值 '%d'。|  
  
## <a name="explanation"></a>说明  
 对主体服务器实例发出此数据库镜像事件，表明未发送日志的量达到了用户指定的阈值。 通常，发生该事件是由于系统的性能已发生变化。 两个系统间的带宽减小或负载增加。  
  
 未发送日志的量（以 KB 计）是一个性能指标，可帮助您计算数据丢失的可能性。 此指标尤其适用于高性能模式会话。 但是，当镜像因伙伴断开连接而暂停或挂起时，此指标也适用于高安全模式会话。  
  
## <a name="user-action"></a>用户操作  
 检查主体服务器实例和镜像服务器实例上的负荷及其网络连接以查找原因。  
  
## <a name="see-also"></a>另请参阅  
 [数据库镜像 (SQL Server)](../../database-engine/database-mirroring/database-mirroring-sql-server.md)   
 [使用镜像性能度量的警告阈值和警报 (SQL Server)](../../database-engine/database-mirroring/use-warning-thresholds-and-alerts-on-mirroring-performance-metrics-sql-server.md)  
  
  
