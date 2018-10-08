---
title: MSSQLSERVER_32044 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 32044 (Database Engine error)
ms.assetid: f2d073be-d9a1-4837-8a38-028d3e3403bd
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: b652864c93127281bacbc26ab5f5e251afea6bc2
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47613555"
---
# <a name="mssqlserver32044"></a>MSSQLSERVER_32044
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>详细信息  
  
|||  
|-|-|  
|产品名称|SQL Server|  
|事件 ID|32044|  
|事件源|MSSQLSERVER|  
|组件|SQLEngine|  
|符号名称|SQLErrorNum32044|  
|消息正文|引发了 '镜像提交开销' 警报。 '%d' 的当前值超出了阈值 '%d'。|  
  
## <a name="explanation"></a>解释  
对主体服务器实例发出此数据库镜像事件，表明由于数据库镜像而使提交等待总时间达到或超出了用户指定的阈值。 等待时间是事务数与每个事务所执行时间的乘积。 例如，下列两种情况都产生 1000 毫秒的等待时间：1000 个事务 * 1 毫秒和 1 个事务 \* 1000 毫秒。 事务计数太大、发送日志延迟时间过长或刷新镜像服务器实例上的日志的延迟时间过长，都会延长提交等待时间。  
  
镜像提交开销量是一个性能指标，可帮助您评估同步操作的当前性能影响。 此指标只适用于高安全模式。 高安全模式是同步模式，因此主体服务器实例将日志记录发送到镜像服务器实例之后将一直等待提交事务，直到收到镜像服务器实例已将日志记录写入磁盘的确认。 在日志记录等待还原到镜像数据库期间，它一直保留在镜像服务器实例的磁盘上。  
  
## <a name="user-action"></a>用户操作  
检查主体服务器实例和镜像服务器实例上的负荷及其网络连接以查找原因。  
  
## <a name="see-also"></a>另请参阅  
[数据库镜像 (SQL Server)](~/database-engine/database-mirroring/database-mirroring-sql-server.md)  
[使用镜像性能度量的警告阈值和警报 (SQL Server)](~/database-engine/database-mirroring/use-warning-thresholds-and-alerts-on-mirroring-performance-metrics-sql-server.md)  
  
