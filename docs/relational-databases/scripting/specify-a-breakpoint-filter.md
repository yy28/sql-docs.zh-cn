---
title: "指定断点筛选器 | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- vs.debug.breakpt.contraints
helpviewer_keywords:
- Transact-SQL debugger, breakpoint filter
ms.assetid: 7bf1dddd-7b0b-4c47-8a7b-28a5569b4fa5
caps.latest.revision: 6
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 52893c5409981b492e10ff1706def0257367c494
ms.contentlocale: zh-cn
ms.lasthandoff: 04/11/2017

---
# <a name="specify-a-breakpoint-filter"></a>指定断点筛选器
  断点筛选器对断点进行限制，使其仅对指定的计算机、操作系统进程和线程执行操作。 断点筛选器通常在调试并行应用程序时使用。  
  
##  <a name="BKMK_ActionConsiderations"></a> 筛选器注意事项  
 断点筛选器通常不与 [!INCLUDE[tsql](../../includes/tsql-md.md)] 调试器结合使用，因为 [!INCLUDE[tsql](../../includes/tsql-md.md)] 脚本和存储过程不是并行应用程序。  
  
#### <a name="to-specify-a-breakpoint-filter"></a>指定断点筛选器  
  
1.  在“编辑器”窗口中，右键单击断点符号，然后单击快捷菜单上的“筛选器”。  
  
     - 或 -  
  
     在“断点”窗口中，右键单击断点符号，然后单击快捷菜单上的“筛选器”。  
  
2.  在 **“断点筛选器”** 对话框中，使用 **“筛选器”** 框按名称指定计算机，或者按名称或 ID 编号指定操作系统进程和线程：  
  
    -   **MachineName** 是运行数据库引擎实例的计算机。  
  
    -   **ProcessID**和 **ProcessName** 是运行数据库引擎实例的操作系统进程。  
  
    -   **ThreadID** 和 **ThreadName** 是在数据库引擎实例中运行 [!INCLUDE[tsql](../../includes/tsql-md.md)] 批处理、过程或功能的操作系统线程。  
  
3.  单击 **“确定”** 实施更改，或单击 **“取消”** 退出而不应用更改。  
  
## <a name="see-also"></a>另请参阅  
 [指定断点条件](../../relational-databases/scripting/specify-a-breakpoint-condition.md)   
 [指定命中计数](../../relational-databases/scripting/specify-a-hit-count.md)   
 [指定断点操作](../../relational-databases/scripting/specify-a-breakpoint-action.md)  
  
  
