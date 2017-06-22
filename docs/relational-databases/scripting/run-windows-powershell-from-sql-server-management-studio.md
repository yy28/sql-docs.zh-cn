---
title: "从 SQL Server Management Studio 运行 Windows PowerShell | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 1f841825-da1f-4062-9a81-3cdbab03845b
caps.latest.revision: 11
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: ec4be68684d53bc8252c0c08e51a47eccb0cc05d
ms.contentlocale: zh-cn
ms.lasthandoff: 06/22/2017

---
# <a name="run-windows-powershell-from-sql-server-management-studio"></a>从 SQL Server Management Studio 中运行 Windows PowerShell
  您可以在 **中从** “对象资源管理器” [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]启动 Windows PowerShell 会话。 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] 启动 Windows PowerShell，加载 **sqlps** 模块，并将路径上下文设置为 “对象资源管理器”树中的相关节点。  
  
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
  
  
