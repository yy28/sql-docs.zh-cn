---
title: "使用性能对象 | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- tools-ssms
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- SQL Server Agent, monitoring
- SQL Server Agent service, monitoring
- SQL Server Agent service, performance objects
- SQL Server Agent, performance objects
- performance objects [SQL Server Agent]
- monitoring [SQL Server], SQL Server Agent
- monitoring [SQL Server Agent]
- performance counters [SQL Server], SQL Server Agent
- counters [SQL Server], SQL Server Agent
ms.assetid: 830b843a-6b2a-4620-a51b-98358e9fc54b
caps.latest.revision: 5
author: stevestein
ms.author: sstein
manager: jhubbard
translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 5197a38da57e041039dab93d037064bba79db7ff
ms.lasthandoff: 04/11/2017

---
# <a name="use-performance-objects"></a>使用性能对象
[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 代理包括用于监视服务执行情况的性能对象和计数器。 这些性能对象使您可以使用性能监视器（一个 Windows 工具）来识别 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 代理服务在后台的运行情况。 例如，您可以通过识别 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 代理服务当前运行的活动作业数量来找出那些锁定的作业。  
  
计算机上安装的每个 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 实例都拥有 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 代理服务性能对象和计数器。 性能对象是根据每个对象所代表的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 实例来命名的。  
  
下表显示了 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 代理服务性能对象的命名方式：  
  
|实例类型|对象名称|  
|-----------------|---------------|  
|默认|**SQLAgent：**对象**：计数器**|  
|已命名|**SQLAgent$**<br /> **&#42;instance_name&#42; ：**对象**：计数器**|  
  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 包括 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 代理的下列性能对象。  
  
|对象名称|Description|  
|---------------|---------------|  
|[SQLAgent:Jobs](http://msdn.microsoft.com/en-us/225b5e2d-4a78-4178-b2b6-b419df83c4aa)|已启动作业的相关性能信息、成功率和当前状态|  
|[SQLAgent:JobSteps](http://msdn.microsoft.com/en-us/44f9983c-1753-4fe0-8475-973aa2460b3a)|作业步骤的相关状态信息|  
|[SQLAgent:Alerts](http://msdn.microsoft.com/en-us/e5e37f74-ee88-46d0-ad8f-71fd1b1fa64a)|警报和通知数的相关信息|  
|[SQLAgent:Statistics](http://msdn.microsoft.com/en-us/ebe92bfa-0721-48aa-9ba6-e7904ad265a1)|常规性能信息|  
  
## <a name="see-also"></a>另请参阅  
[监视和优化性能](http://msdn.microsoft.com/en-us/87f23f03-0f19-4b2e-bfae-efa378f7a0d4)  
[如何启动系统监视器 (Windows)](http://msdn.microsoft.com/en-us/5e51bb79-5737-470b-9c47-fac330c001c5)  
  

