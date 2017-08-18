---
title: "SCM 服务 - 将实例设置为自动启动 | Microsoft Docs"
ms.custom:
- SQL2016_New_Updated
ms.date: 01/06/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- automatic SQL Server startup
- SQL Server, automatic startup
- starting SQL Server, automatically
ms.assetid: aa2b6bde-e76d-4fea-a560-54a63745d9b1
caps.latest.revision: 35
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: HT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 63598cfe81abc270430638d9d45a812ab2207815
ms.contentlocale: zh-cn
ms.lasthandoff: 08/02/2017

---
# <a name="scm-services---set-an-instance-to-start-automatically"></a>SCM 服务 - 将实例设置为自动启动
  本主题说明如何使用 SQL Server 配置管理器在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中将 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 实例设置为自动启动。 在安装过程中， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 通常配置为自动启动。 如果没有这样做，则可以随时更改该设置。  
  
##  <a name="SSMSProcedure"></a> 使用 SQL Server 配置管理器  
  
#### <a name="to-set-an-instance-of-sql-server-to-start-automatically"></a>将 SQL Server 实例设置为自动启动  
  
1.  在“开始”  菜单上，依次指向“所有程序” 、 [!INCLUDE[ssCurrentUI](../../includes/sscurrentui-md.md)]、“配置工具” ，然后单击“SQL Server 配置管理器” 。  
  
    > [!NOTE]  
    >  因为 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 配置管理器是 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 管理控制台程序的一个管理单元而不是单独的程序，所以 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 配置管理器在新版本的 Windows 中不显示为一个应用程序。  
    >   
    >  -   **Windows 10**：  
    >          要打开 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 配置管理器，请在“起始页” 中键入 SQLServerManager13.msc（适用于 [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]）。 对于早期版本的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ，请将 13 替换为较小的数字。 单击“SQLServerManager13.msc”可打开配置管理器。 要将配置管理器固定到“起始页”或“任务栏”，请右键单击“SQLServerManager13.msc”，然后单击“打开文件位置” 。 在“Windows 文件资源管理器”中，右键单击“SQLServerManager13.msc”，然后单击“固定到‘开始’屏幕”  或“固定到任务栏” 。  
    > -   **Windows 8**：  
    >          若要打开 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 配置管理器，请在“搜索”超级按钮中的“应用”下，键入 SQLServerManager\<version>.msc（例如 SQLServerManager13.msc），然后按“Enter”。  
  
2.  在 **“SQL Server 配置管理器”**中，展开 **“服务”**，再单击 **SQL Server**。  
  
3.  在详细信息窗格中，右键单击要自动启动的实例的名称，然后单击“属性”。  
  
4.  在“SQL Server \<实例名> 属性”对话框中，将“启动模式”设置为“自动”********。  
  
5.  单击 **“确定”**，然后关闭 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 配置管理器。  
  
## <a name="see-also"></a>另请参阅  
 [防止 SQL Server 实例自动启动（SQL Server 配置管理器）](../../database-engine/configure-windows/scm-services-prevent-automatic-startup-of-an-instance.md)   
 [连接到其他计算机（SQL Server 配置管理器）](../../database-engine/configure-windows/scm-services-connect-to-another-computer.md)   
 [在 SQL Server 工具中将 WMI 配置为显示服务器状态](http://msdn.microsoft.com/library/7e97197b-ed4d-40d1-9a52-9ab1d92401d7)  
  
  

