---
title: MSSQLSERVER_32044 | Microsoft Docs
ms.custom: ''
ms.date: 03/08/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- 32044 (Database Engine error)
ms.assetid: f2d073be-d9a1-4837-8a38-028d3e3403bd
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: d41e9cb873c2152aaab26e5c8f789391670b4305
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/18/2020
ms.locfileid: "85033907"
---
# <a name="mssqlserver_32044"></a>MSSQLSERVER_32044
    
## <a name="details"></a>详细信息  
  
|||  
|-|-|  
|产品名称|SQL Server|  
|事件 ID|32044|  
|事件源|MSSQLSERVER|  
|组件|SQLEngine|  
|符号名称|SQLErrorNum32044|  
|消息正文|引发了 '镜像提交开销' 警报。 '%d' 的当前值超出了阈值 '%d'。|  
  
## <a name="explanation"></a>说明  
 对主体服务器实例发出此数据库镜像事件，表明由于数据库镜像而使提交等待总时间达到或超出了用户指定的阈值。 等待时间是事务数与每个事务所执行时间的乘积。 例如，下列两种情况都产生 1000 毫秒的等待时间：1000 个事务 * 1 毫秒和 1 个事务 \* 1000 毫秒。 事务计数太大、发送日志延迟时间过长或刷新镜像服务器实例上的日志的延迟时间过长，都会延长提交等待时间。  
  
 镜像提交开销量是一个性能指标，可帮助您评估同步操作的当前性能影响。 此指标只适用于高安全模式。 高安全模式是同步模式，因此主体服务器实例将日志记录发送到镜像服务器实例之后将一直等待提交事务，直到收到镜像服务器实例已将日志记录写入磁盘的确认。 在日志记录等待还原到镜像数据库期间，它一直保留在镜像服务器实例的磁盘上。  
  
## <a name="user-action"></a>用户操作  
 检查主体服务器实例和镜像服务器实例上的负荷及其网络连接以查找原因。  
  
## <a name="see-also"></a>另请参阅  
 [数据库镜像 &#40;SQL Server&#41;](../../database-engine/database-mirroring/database-mirroring-sql-server.md)   
 [使用镜像性能度量的警告阈值和警报 (SQL Server)](../../database-engine/database-mirroring/use-warning-thresholds-and-alerts-on-mirroring-performance-metrics-sql-server.md)  
  
  
