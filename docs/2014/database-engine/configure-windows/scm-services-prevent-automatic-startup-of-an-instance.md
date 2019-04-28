---
title: 防止自动启动实例的 SQL Server （SQL Server 配置管理器） |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- automatic SQL Server startup
- SQL Server, stopping
- SQL Server, automatic startup
- canceling automatic startup
- stopping SQL Server
- preventing automatic startups [SQL Server]
ms.assetid: 782663cf-f3d7-4cc6-b621-21e4550f0322
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 6af4597a4ddf802c80bc98cb38363d59348fa0bb
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62810043"
---
# <a name="prevent-automatic-startup-of-an-instance-of-sql-server-sql-server-configuration-manager"></a>防止 SQL Server 实例自动启动（SQL Server 配置管理器）
  本主题说明如何使用 SQL Server 配置管理器在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中禁止 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 实例自动启动。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 通常配置为自动启动。 您可以通过将实例的启动模式设置为手动来更改此默认设置。  
  
##  <a name="SSMSProcedure"></a> 使用 SQL Server 配置管理器  
  
#### <a name="to-prevent-automatic-startup-of-an-instance-of-sql-server"></a>防止自动启动 SQL Server 实例  
  
1.  在 **“开始”** 菜单中，依次指向 **“所有程序”**、 [!INCLUDE[ssCurrentUI](../../includes/sscurrentui-md.md)]、 **“配置工具”**，然后单击 **“SQL Server 配置管理器”**。  
  
2.  在 SQL Server 配置管理器中，展开 **“服务”**，再单击 **SQL Server**。  
  
3.  在“详细信息”窗格中，右键单击“” ，再单击“属性”   
  
4.  在“属性”框的“SQL Server \<实例名> 属性”对话框中，将“启动模式”的值设置为“手动”。  
  
5.  单击“确定”关闭“SQL Server \<实例名> 属性”对话框，然后再关闭 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 配置管理器。  
  
## <a name="see-also"></a>请参阅  
 [启动、停止、暂停、继续、重新启动数据库引擎、SQL Server 代理或 SQL Server Browser 服务](start-stop-pause-resume-restart-sql-server-services.md)  
  
  
