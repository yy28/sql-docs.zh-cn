---
title: MSSQLSERVER_1458 | Microsoft Docs
ms.custom: 
ms.date: 04/04/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: errors-events
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
helpviewer_keywords:
- 1458 (Database Engine error)
ms.assetid: adc78c59-a6f2-432b-9a07-fdd1dc2b9026
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 64e6c7221c95e0e7ad5622a896d113d779ad4538
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/21/2017
---
# <a name="mssqlserver1458"></a>MSSQLSERVER_1458
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
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
  
