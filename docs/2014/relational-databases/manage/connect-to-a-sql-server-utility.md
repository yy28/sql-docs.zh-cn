---
title: 连接到 SQL Server 实用工具 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
ms.assetid: b9b90b8d-241f-4b74-ac14-de7b10ea1821
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 1c23f91f24f2da173280e54a544b00a1b4a6fd09
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62806149"
---
# <a name="connect-to-a-sql-server-utility"></a>连接到 SQL Server 实用工具
  必须先创建实用工具控制点 (UCP)，然后才能连接到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实用工具。 有关详细信息，请参阅 [SQL Server 实用工具功能和任务](sql-server-utility-features-and-tasks.md)。  
  
 若要查看和管理 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 资源运行状况，请使用 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] (SSMS) 连接到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实用工具。  
  
 通过 SSMS 连接到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实用工具：  
  
1.  启动 SSMS。  
  
2.  在 SSMS 中，连接到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]的某一实例。  
  
3.  单击 **“视图”** ，然后单击 **“实用工具资源管理器”**。  
  
4.  在“实用工具资源管理器”导航窗格中，单击 ![](../../database-engine/media/connect-to-utility.gif "Connect_to_Utility")“连接到实用工具”。  
  
5.  在 **“连接到服务器”** 对话框中，指定 UCP 实例名称，再单击 **“连接”**。  
  
6.  查看实用工具资源管理器导航窗格，以便查看 UCP 中 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 资源的树视图。  
  
 创建一个新的 UCP 也将您连接到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实用工具。 有关详细信息，请参阅[创建 SQL Server 实用工具控制点（SQL Server 实用工具）](create-a-sql-server-utility-control-point-sql-server-utility.md)。  
  
## <a name="see-also"></a>请参阅  
 [SQL Server 实用工具的功能和任务](sql-server-utility-features-and-tasks.md)   
 [查看资源运行状况策略结果（SQL Server 实用工具）](view-resource-health-policy-results-sql-server-utility.md)  
  
  
