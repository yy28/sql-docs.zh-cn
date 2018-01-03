---
title: "“命令”窗口 | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: sql-tools
ms.service: 
ms.component: ssms-scripting
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords: VS.CommandWindow
helpviewer_keywords: Command Window [Transact-SQL]
ms.assetid: e567ebf9-0793-451b-92c7-26193a02d9da
caps.latest.revision: "14"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: c3eaff3d1dde482beb19c2cb0e03942bbaefcd83
ms.sourcegitcommit: b603dcac7326bba387befe68544619e026e6a15e
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/21/2017
---
# <a name="transact-sql-debugger---command-window"></a>Transact-SQL 调试器 -“命令”窗口
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]使用“命令窗口”可以对 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 查询编辑器窗口中当前所调试的代码运行命令，例如调试和编辑命令。 只有在调试模式下才可以使用 **“命令窗口”**。 [!INCLUDE[tsql](../../includes/tsql-md.md)] 调试器支持许多在 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)]“命令”窗口中支持的命令。 有关详细信息，请参阅 [Visual Studio“命令”窗口](http://go.microsoft.com/fwlink/?LinkId=112007)。  
  
## <a name="task-list"></a>任务列表  
 **访问“命令”窗口**  
  
-   在 **“调试”** 菜单中，单击 **“启动调试”**。  
  
 **打印变量的值**  
  
-   在“命令窗口”中，键入 **Debug.Print \<VariableName>**，然后按 Enter 键。  
  
 **列出有关当前线程的信息**  
  
-   在“命令窗口”中，键入 **Debug.ListThread**，然后按 Enter 键。  
  
 **将变量添加到“快速监视”窗口**  
  
-   在“命令窗口”中，键入 **Debug.QuickWatch \<VariableName>**，然后按 Enter 键。  
  
## <a name="see-also"></a>另请参阅  
 [Transact-SQL 调试器](../../relational-databases/scripting/transact-sql-debugger.md)  
  
  
