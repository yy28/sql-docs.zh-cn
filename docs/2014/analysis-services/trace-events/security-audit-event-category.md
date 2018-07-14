---
title: Security Audit 事件类别 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- Security Audit event category [SQL Server]
- event classes [Analysis Services], security audit
- security events [Analysis Services]
ms.assetid: 9686a495-68d7-4137-8e30-2655aa519f6c
caps.latest.revision: 24
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 79141f6ed5c61e03b792875fbff2253f9e8bd0aa
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2018
ms.locfileid: "37180904"
---
# <a name="security-audit-event-category"></a>“安全审核”事件类别
  “安全审核”事件类别具有下表中说明的事件类。  
  
|Event Class|事件 ID|Description|  
|-----------------|--------------|-----------------|  
|审核登录|@shouldalert|记录跟踪启动后发生的所有新连接事件，如客户端请求与正在运行 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]实例的服务器进行连接。|  
|审核注销|2|记录从开始跟踪之后发生的所有新断开连接事件，如客户端发出一个断开连接命令即属于一个断开连接事件。|  
|Audit Server Starts and Stops|4|记录关闭、启动和暂停服务活动。|  
|审核对象权限事件|18|记录所有对象权限的更改。|  
|审核管理操作事件|19|记录用于备份、还原、同步、附加、分离、图像加载和图像保存的服务器操作。|  
  
 有关与每个安全审核事件类关联的列的信息，请参阅 [Security Audit Data Columns](security-audit-data-columns.md)。  
  
## <a name="see-also"></a>请参阅  
 [Analysis Services 跟踪事件](analysis-services-trace-events.md)  
  
  
