---
title: 将 SQL Server 的实例设置为自动启动（SQL Server 配置管理器） |Microsoft Docs
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
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "62809987"
---
# <a name="set-an-instance-of-sql-server-to-start-automatically-sql-server-configuration-manager"></a>将 SQL Server 实例设置为自动启动（SQL Server 配置管理器）
  本主题说明如何使用 SQL Server 配置管理器在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中将 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 实例设置为自动启动。 在安装过程中， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 通常配置为自动启动。 如果没有这样做，则可以随时更改该设置。  
  
##  <a name="SSMSProcedure"></a> 使用 SQL Server 配置管理器  
  
#### <a name="to-set-an-instance-of-sql-server-to-start-automatically"></a>将 SQL Server 实例设置为自动启动  
  
1.  在 **“开始”** 菜单中，依次指向 **“所有程序”** 、 [!INCLUDE[ssCurrentUI](../../includes/sscurrentui-md.md)]、 **“配置工具”** ，然后单击 **“SQL Server 配置管理器”** 。  
  
    > [!NOTE]  
    >  因为 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 配置管理器是 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 管理控制台程序的一个管理单元而不是单独的程序，所以 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 配置管理器在新版本的 Windows 中不显示为一个应用程序。  
    >   
    >  -   **Windows 10**：  
    >          若要[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]打开 Configuration Manager，请在 "**开始" 页**上键入 sqlservermanager12.msc （ [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]对于）。 对于早期版本的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ，请将 12 替换为较小的数字。 单击 SQLServerManager12.msc 可打开“配置管理器”。 若要将 Configuration Manager 固定到 "起始页" 或 "任务栏"，请右键单击 "Sqlservermanager12.msc"，然后单击 "**打开文件位置**"。 在 Windows 文件资源管理器中，右键单击 "Sqlservermanager12.msc"，然后单击 "**固定到****任务栏**"。  
    > -   **Windows 8**：  
    >          若要[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]打开 Configuration Manager，请在 "**搜索**" 超级按钮中的 "**应用**" 下，键入`SQLServerManager12.msc` **Sqlservermanager version>.msc\<version>** （如），然后按**enter**。  
  
2.  在 **“SQL Server 配置管理器”** 中，展开 **“服务”** ，再单击 **SQL Server**。  
  
3.  在详细信息窗格中，右键单击要自动启动的实例的名称，然后单击“属性”  。  
  
4.  在 **“SQL Server”\< ***“实例名” ***>“属性”** 对话框中，将 **“启动模式”** 设置为 **“自动”** 。  
  
5.  单击 **“确定”** ，然后关闭 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 配置管理器。  
  
## <a name="see-also"></a>另请参阅  
 [防止 SQL Server 实例自动启动（SQL Server 配置管理器）](scm-services-prevent-automatic-startup-of-an-instance.md)   
 [连接到其他计算机（SQL Server 配置管理器）](scm-services-connect-to-another-computer.md)   
 [在 SQL Server 工具中将 WMI 配置为显示服务器状态](../../ssms/configure-wmi-to-show-server-status-in-sql-server-tools.md)  
  
  
