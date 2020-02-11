---
title: MSSQL_ENG014160 | Microsoft Docs
ms.custom: ''
ms.date: 03/08/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- MSSQL_ENG014160 error
ms.assetid: d0f3855e-d095-4a81-a5bd-9d7ad51f2c77
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 42f0b6894bac639d287eb62f9870d7bfd6daba3a
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "62864842"
---
# <a name="mssql_eng014160"></a>MSSQL_ENG014160
    
## <a name="message-details"></a>消息详细信息  
  
|||  
|-|-|  
|产品名称|SQL Server|  
|事件 ID|14160|  
|事件源|MSSQLSERVER|  
|组件|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|  
|符号名称||  
|消息正文|已设置发布 [%s] 的阈值 [%s:%s]。 此发布的一个或多个订阅已过期。|  
  
## <a name="explanation"></a>说明  
 使用复制可以对一些情况启用警告。 例如，订阅即将过期时，即可以发出此警告。 如果在指定的“保持期”  内未同步订阅，则订阅会过期。 有关详细信息，请参阅 [Subscription Expiration and Deactivation](subscription-expiration-and-deactivation.md)。  
  
 使用复制监视器或 [sp_replmonitorchangepublicationthreshold](/sql/relational-databases/system-stored-procedures/sp-replmonitorchangepublicationthreshold-transact-sql)启用警告时，请指定阈值以确定何时触发警告。 达到或超过该阈值时，复制监视器中将显示警告，并且将一个事件写入 Windows 事件日志。 达到阈值还会触发 SQL Server 代理警报。 有关详细信息，请参阅[在复制监视器中设置阈值和警告](monitor/set-thresholds-and-warnings-in-replication-monitor.md)和[以编程方式监视复制](monitoring-replication.md)。  
  
## <a name="user-action"></a>用户操作  
 对此问题的解决依赖于引起警告的原因：  
  
-   如果已超过阈值，但订阅尚未过期，则同步订阅。 有关详细信息，请参阅 [同步数据](synchronize-data.md)。  
  
-   如果代理已经运行，但尚未正确复制更改，则会导致订阅过期。 对于事务复制，请确保分发代理和日志读取器代理正在运行。 对于合并复制，请确保合并代理正在运行。 有关如何启动这些代理的信息，请参阅[启动和停止复制代理 (SQL Server Management Studio)](agents/start-and-stop-a-replication-agent-sql-server-management-studio.md) 和[复制代理可执行文件概念](concepts/replication-agent-executables-concepts.md)。  
  
-   如果订阅已过期，则必须重新初始化订阅或删除然后重新创建订阅，具体取决于订阅的类型和已过期多长时间。 有关详细信息，请参阅 [Subscription Expiration and Deactivation](subscription-expiration-and-deactivation.md)。  
  
## <a name="see-also"></a>另请参阅  
 [错误和事件参考（复制）](errors-and-events-reference-replication.md)  
  
  
