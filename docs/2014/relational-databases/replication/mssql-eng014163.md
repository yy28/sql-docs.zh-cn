---
title: MSSQL_ENG014163 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- MSSQL_ENG014163 error
ms.assetid: b53dd463-ba36-421e-9745-67c7387e68dd
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: bab625541bbd4f3051ef73a49548f032b3465691
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62864875"
---
# <a name="mssqleng014163"></a>MSSQL_ENG014163
    
## <a name="message-details"></a>消息详细信息  
  
|||  
|-|-|  
|产品名称|SQL Server|  
|事件 ID|14163|  
|事件源|MSSQLSERVER|  
|组件|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|  
|符号名称||  
|消息正文|已设置发布 [%s] 的阈值 [%s:%s]。 请确保合并代理正在运行且符合要求。|  
  
## <a name="explanation"></a>解释  
 使用复制可以对一些情况启用警告。 这包括超出了为同步合并发布服务器和订阅服务器间的更改所指定的时间长度。 可以为 LAN 连接和拨号连接指定不同的连接次数。  
  
 使用复制监视器或 [sp_replmonitorchangepublicationthreshold](/sql/relational-databases/system-stored-procedures/sp-replmonitorchangepublicationthreshold-transact-sql)启用警告时，请指定阈值以确定何时触发警告。 达到或超过该阈值时，复制监视器中将显示警告，并且将一个事件写入 Windows 事件日志。 达到阈值还会触发 SQL Server 代理警报。 有关详细信息，请参阅[在复制监视器中设置阈值和警告](monitor/set-thresholds-and-warnings-in-replication-monitor.md)和[以编程方式监视复制](monitoring-replication.md)。  
  
## <a name="user-action"></a>用户操作  
 如果订阅超过持续时间阈值，则必须确定系统是否存在性能问题，或是否应调整阈值。 配置复制后，请确立一个性能基准，以便于确定复制在通常用于应用程序和拓扑的常见工作负荷中的行为方式。 将同步持续时间包括在该基准中，以便可以为阈值设置合适的值。  
  
 如果阈值适当，但超过了该阈值，则必须确定系统何处存在性能瓶颈。 有关如何监视复制性能和对其进行故障排除的详细信息，请参阅[用复制监视器监视性能](monitor/monitor-performance-with-replication-monitor.md)。  
  
## <a name="see-also"></a>请参阅  
 [错误和事件参考（复制）](errors-and-events-reference-replication.md)  
  
  
