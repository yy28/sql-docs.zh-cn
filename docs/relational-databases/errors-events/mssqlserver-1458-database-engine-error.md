---
title: MSSQLSERVER_1458 | Microsoft Docs
ms.custom: 
ms.date: 04/04/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
helpviewer_keywords: 1458 (Database Engine error)
ms.assetid: adc78c59-a6f2-432b-9a07-fdd1dc2b9026
caps.latest.revision: "16"
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: Inactive
ms.openlocfilehash: 249182dd83285da77677ca9411aa83bc1b92e1e2
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/09/2017
---
# <a name="mssqlserver1458"></a>MSSQLSERVER_1458
  
## <a name="details"></a>详细信息  
  
|||  
|-|-|  
|产品名称|SQL Server|  
|事件 ID|1458|  
|事件源|MSSQLSERVER|  
|组件|SQLEngine|  
|符号名称|DBM_FAILREDO_ON_PRIMARY|  
|消息正文|'%.*ls' 数据库的主体副本遇到错误 %d，状态 %d，严重性 %d。 数据库镜像已挂起。 请尝试纠正错误条件，然后继续镜像。|  
  
## <a name="explanation"></a>解释  
该消息指出主体数据库遇到了导致数据库镜像被挂起的错误。  
  
## <a name="user-action"></a>用户操作  
导致此错误的大多数原因可以自我更正。 如果该问题仍然存在，重新启动数据库或服务器实例通常可以更正该问题。 有关详细信息，请查看每个伙伴中的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 错误日志以获得出现在此消息之前的关联错误。  
  
## <a name="see-also"></a>另请参阅  
[监视数据库镜像 (SQL Server)](~/database-engine/database-mirroring/monitoring-database-mirroring-sql-server.md)  
  
