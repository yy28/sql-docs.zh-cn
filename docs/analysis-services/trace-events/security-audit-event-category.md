---
title: "Security Audit 事件类别 |Microsoft 文档"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: trace-events
ms.reviewer: 
ms.suite: sql
ms.technology:
- analysis-services
ms.tgt_pltfrm: 
ms.topic: reference
helpviewer_keywords:
- Security Audit event category [SQL Server]
- event classes [Analysis Services], security audit
- security events [Analysis Services]
ms.assetid: 9686a495-68d7-4137-8e30-2655aa519f6c
caps.latest.revision: 25
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: bb384601c49088675c25547b3ae7dc21b4510380
ms.contentlocale: zh-cn
ms.lasthandoff: 09/01/2017

---
# <a name="security-audit-event-category"></a>“安全审核”事件类别
  “安全审核”事件类别具有下表中说明的事件类。  
  
|Event Class|事件 ID|Description|  
|-----------------|--------------|-----------------|  
|审核登录|1|记录跟踪启动后发生的所有新连接事件，如客户端请求与正在运行 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]实例的服务器进行连接。|  
|审核注销|2|记录从开始跟踪之后发生的所有新断开连接事件，如客户端发出一个断开连接命令即属于一个断开连接事件。|  
|Audit Server Starts and Stops|4|记录关闭、启动和暂停服务活动。|  
|审核对象权限事件|18|记录所有对象权限的更改。|  
|审核管理操作事件|19|记录用于备份、还原、同步、附加、分离、图像加载和图像保存的服务器操作。|  
  
 有关与每个安全审核事件类关联的列的信息，请参阅 [Security Audit Data Columns](../../analysis-services/trace-events/security-audit-data-columns.md)。  
  
## <a name="see-also"></a>另请参阅  
 [Analysis Services 跟踪事件](../../analysis-services/trace-events/analysis-services-trace-events.md)  
  
  

