---
title: "“安全审核”事件类别 | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "analysis-services"
ms.tgt_pltfrm: ""
ms.topic: "reference"
helpviewer_keywords: 
  - "Security Audit 事件类别 [SQL Server]"
  - "事件类 [Analysis Services], 安全审核"
  - "安全事件 [Analysis Services]"
ms.assetid: 9686a495-68d7-4137-8e30-2655aa519f6c
caps.latest.revision: 25
author: "Minewiskan"
ms.author: "owend"
manager: "erikre"
caps.handback.revision: 25
---
# “安全审核”事件类别
  “安全审核”事件类别具有下表中说明的事件类。  
  
|Event Class|事件 ID|Description|  
|-----------------|--------------|-----------------|  
|审核登录|1|记录跟踪启动后发生的所有新连接事件，如客户端请求与正在运行 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]实例的服务器进行连接。|  
|审核注销|2|记录从开始跟踪之后发生的所有新断开连接事件，如客户端发出一个断开连接命令即属于一个断开连接事件。|  
|Audit Server Starts and Stops|4|记录关闭、启动和暂停服务活动。|  
|审核对象权限事件|18|记录所有对象权限的更改。|  
|审核管理操作事件|19|记录用于备份、还原、同步、附加、分离、图像加载和图像保存的服务器操作。|  
  
 有关与每个安全审核事件类关联的列的信息，请参阅 [Security Audit Data Columns](../../analysis-services/trace-events/security-audit-data-columns.md)。  
  
## 另请参阅  
 [Analysis Services 跟踪事件](../../analysis-services/trace-events/analysis-services-trace-events.md)  
  
  