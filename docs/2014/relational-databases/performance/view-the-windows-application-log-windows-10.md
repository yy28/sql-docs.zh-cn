---
title: 查看 Windows 应用程序日志 (Windows) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- viewing logs
- application logs [SQL Server]
- logs [SQL Server], application
- monitoring Windows NT application log [SQL Server]
- Windows NT application logs [SQL Server]
- displaying logs
- monitoring [SQL Server], events
- logs [SQL Server], viewing
ms.assetid: 168a6c6e-12df-46a9-9904-55d63ca8fe14
caps.latest.revision: 23
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 541bbb31e853e604bc56d707d74cc77a02f89753
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2018
ms.locfileid: "37307339"
---
# <a name="view-the-windows-application-log-windows"></a>查看 Windows 应用程序日志 (Windows)
  将 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 配置为使用 Windows 应用程序日志后，每个 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 会话都将新事件写入该日志。 与 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 错误日志不同，不是每次启动 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]实例时都创建新的应用程序日志。  
  
### <a name="to-view-the-windows-application-log"></a>查看 Windows 应用程序日志  
  
1.  在 **“开始”** 菜单上，依次指向 **“所有程序”**、 **“管理工具”**，然后单击 **“事件查看器”**。  
  
2.  在事件查看器中，单击 **“应用程序”**。  
  
3.  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 事件由“源”列中的 MSSQLSERVER 项（命名实例以 MSSQL$<instance_name> 标识）标识。 SQL Server 代理事件由 SQLSERVERAGENT 项标识（对于已命名的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 代理事件由 **SQLAgent$**\<*instance_name*> 标识）。 Microsoft Search 服务事件由 **Microsoft Search**项标识。  
  
4.  若要查看另一台计算机的日志，请右键单击“事件查看器”，再单击“连接到另一台计算机”，并完成“选择计算机”对话框。  
  
5.  另外，若要仅显示 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 事件，请在 **“查看”** 菜单上单击 **“筛选器”**，并在 **“事件源”** 列表中，选择 **MSSQLSERVER**。 若要仅查看 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 代理事件，请在 **“事件源”** 列表中选择 **SQLSERVERAGENT** 。  
  
6.  若要查看有关某事件的详细信息，请双击该事件。  
  
## <a name="see-also"></a>请参阅  
 [查看 SQL Server 错误日志 (SQL Server Management Studio)](../../ssms/sql-server-management-studio-ssms.md)  
  
  
