---
title: 设置 SQL Server 的实例为自动启动 （SQL Server 配置管理器） |Microsoft Docs
ms.custom: ''
ms.date: 01/07/2016
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- automatic SQL Server startup
- SQL Server, automatic startup
- starting SQL Server, automatically
ms.assetid: aa2b6bde-e76d-4fea-a560-54a63745d9b1
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 300b539e132b9bda9bc6540c0aadcac6ab9f11a1
ms.sourcegitcommit: 04dd0620202287869b23cc2fde998a18d3200c66
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/30/2018
ms.locfileid: "52640309"
---
# <a name="set-an-instance-of-sql-server-to-start-automatically-sql-server-configuration-manager"></a>将 SQL Server 实例设置为自动启动（SQL Server 配置管理器）
  本主题说明如何使用 SQL Server 配置管理器在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中将 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 实例设置为自动启动。 在安装过程中， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 通常配置为自动启动。 如果没有这样做，则可以随时更改该设置。  
  
##  <a name="SSMSProcedure"></a> 使用 SQL Server 配置管理器  
  
#### <a name="to-set-an-instance-of-sql-server-to-start-automatically"></a>将 SQL Server 实例设置为自动启动  
  
1.  在“开始”  菜单上，依次指向“所有程序” 、 [!INCLUDE[ssCurrentUI](../../includes/sscurrentui-md.md)]、“配置工具” ，然后单击“SQL Server 配置管理器” 。  
  
    > [!NOTE]  
    >  因为 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 配置管理器是 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 管理控制台程序的一个管理单元而不是单独的程序，所以 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 配置管理器在新版本的 Windows 中不显示为一个应用程序。  
    >   
    >  -   **Windows 10**：  
    >          若要打开[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]配置管理器，然后在**起始页**，键入 SQLServerManager12.msc (对于[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)])。 对于早期版本的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ，请将 12 替换为较小的数字。 单击 SQLServerManager12.msc 会打开配置管理器。 若要固定到起始页或任务栏配置管理器，右键单击 SQLServerManager12.msc，然后依次**打开文件位置**。 在 Windows 文件资源管理器中，右键单击 SQLServerManager12.msc，，然后单击**固定到开始屏幕**或**锁定到任务栏**。  
    > -   **Windows 8**：  
    >          若要打开[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]配置管理器，请在**搜索**超级按钮**应用**，类型**SQLServerManager\<版本 >.msc**如`SQLServerManager12.msc`，然后按**Enter**。  
  
2.  在 **“SQL Server 配置管理器”** 中，展开 **“服务”**，再单击 **SQL Server**。  
  
3.  在详细信息窗格中，右键单击要自动启动的实例的名称，然后单击“属性”。  
  
4.  在“SQL Server \<instancename> 属性”对话框中，将“启动模式”设置为“自动”。 ****  
  
5.  单击 **“确定”**，然后关闭 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 配置管理器。  
  
## <a name="see-also"></a>请参阅  
 [防止 SQL Server 实例自动启动（SQL Server 配置管理器）](scm-services-prevent-automatic-startup-of-an-instance.md)   
 [连接到其他计算机（SQL Server 配置管理器）](scm-services-connect-to-another-computer.md)   
 [在 SQL Server 工具中将 WMI 配置为显示服务器状态](../../ssms/configure-wmi-to-show-server-status-in-sql-server-tools.md)  
  
  
