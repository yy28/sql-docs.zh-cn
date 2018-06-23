---
title: 连接到 SQL Server 实用工具 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- dbe-cross-instance
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: b9b90b8d-241f-4b74-ac14-de7b10ea1821
caps.latest.revision: 6
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: e63feca9bd2cb813da7924d96677f5dcb35ee8eb
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36127523"
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
  
  