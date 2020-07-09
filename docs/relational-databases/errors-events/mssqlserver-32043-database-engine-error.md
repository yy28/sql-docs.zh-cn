---
title: MSSQLSERVER_32043 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 32043 (Database Engine error)
ms.assetid: a0c48ae3-4c8c-419c-afb5-579fcefac01d
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 13ef94422e280cce2d32368d8294f8c437f48c88
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/01/2020
ms.locfileid: "85723651"
---
# <a name="mssqlserver_32043"></a>MSSQLSERVER_32043
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  
## <a name="details"></a>详细信息  
  
| Attribute | 值 |  
| :-------- | :---- |  
|产品名称|SQL Server|  
|事件 ID|32043|  
|事件源|MSSQLSERVER|  
|组件|SQLEngine|  
|符号名称|SQLErrorNum32043|  
|消息正文|引发了 '未还原日志' 警报。 '%d' 的当前值超出了阈值 '%d'。|  
  
## <a name="explanation"></a>说明  
此数据库镜像事件是对镜像服务器实例发出的，指示未还原日志量已达到了用户指定的阈值。 通常，发生该事件是由于系统的性能已发生变化。 两个系统间的带宽减小或负载增加。  
  
未还原日志是镜像服务器实例已接收并已写入磁盘但等待还原到镜像数据库的日志。 未还原日志量（以 KB 为单位）是一种性能指标，有助于您计算当前故障转移时间。 应用未还原日志所需的时间是构成故障转移时间的主要部分，另外还包括恢复数据库并使之在线所需的额外短暂时间。  
  
> [!NOTE]  
> 对于自动故障转移，系统识别故障所需的时间与故障转移时间无关。  
  
## <a name="user-action"></a>用户操作  
检查主体服务器实例和镜像服务器实例上的负荷及其网络连接以查找原因。  
  
## <a name="see-also"></a>另请参阅  
[数据库镜像 (SQL Server)](~/database-engine/database-mirroring/database-mirroring-sql-server.md)  
[使用镜像性能度量的警告阈值和警报 (SQL Server)](~/database-engine/database-mirroring/use-warning-thresholds-and-alerts-on-mirroring-performance-metrics-sql-server.md)  
  
