---
title: "从 SQL Server Management Studio 运行 Windows PowerShell | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: ssms
ms.service: 
ms.component: scripting
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 1f841825-da1f-4062-9a81-3cdbab03845b
caps.latest.revision: "11"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: 2f3f405a8a0a64d1202918154a163bf9b397ab93
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/17/2017
---
# <a name="run-windows-powershell-from-sql-server-management-studio"></a>从 SQL Server Management Studio 中运行 Windows PowerShell
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]可以在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 中从“对象资源管理器”启动 Windows PowerShell 会话。 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] 启动 Windows PowerShell，加载 **sqlps** 模块，并将路径上下文设置为 “对象资源管理器”树中的相关节点。  
  
## <a name="before-you-begin"></a>开始之前  
 在“对象资源管理器”中为某个对象指定正在运行的 PowerShell 时，[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 将启动其中已经加载和注册了[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] PowerShell 管理单元的 Windows PowerShell 会话。 该会话的路径预设为您在对象资源管理器中右键单击的对象位置。 例如，如果在对象资源管理器中右键单击[!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] 数据库对象并选择“启动 PowerShell”，则 Windows PowerShell 路径将设置为：  
  
```  
SQLSERVER:\SQL\MyComputer\MyInstance\Databases\AdventureWorks2012>  
```  
  
## <a name="run-powershell"></a>运行 PowerShell  
 **从 SQL Server Management Studio 运行 PowerShell**  
  
1.  打开 **“对象资源管理器”**。  
  
2.  导航到要进行处理的对象的节点。  
  
3.  右键单击该对象，然后选择“启动 PowerShell”。  
  
## <a name="permissions"></a>权限  
 在从 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]打开 PowerShell 时，它不会使用管理员权限运行，这可能会阻止某些活动（如调用 WMI）。  
  
## <a name="see-also"></a>另请参阅  
 [SQL Server PowerShell](../../relational-databases/scripting/sql-server-powershell.md)  
  
  
