---
title: "“局部变量”窗口 | Microsoft Docs"
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
- vs.debug.locals
helpviewer_keywords:
- Locals Window [Transact-SQL]
ms.assetid: 59bea640-7823-4b4d-832c-f384d83cca2f
caps.latest.revision: 16
author: BYHAM
ms.author: rickbyh
manager: jhubbard
translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 84668538d8c13c4317eec610afabcdf39d457899
ms.lasthandoff: 04/11/2017

---
# <a name="transact-sql-debugger---locals-window"></a>Transact-SQL 调试器 -“局部变量”窗口
  **“局部变量”** 窗口显示有关 [!INCLUDE[tsql](../../includes/tsql-md.md)] 调试器的当前作用域中局部表达式的信息。 此作用域设定为在 **“调用堆栈”** 窗口中选择的当前调用堆栈帧。 只有在调试模式下才可以显示局部表达式。  
  
## <a name="task-list"></a>任务列表  
 **访问“局部变量”窗口**  
  
-   在 **“调试”** 菜单上单击 **“窗口”**，然后单击 **“局部变量”**。  
  
 **更改表达式的值**  
  
-   右键单击表达式，然后选择“编辑值”。  
  
## <a name="columns"></a>列  
 **名称**  
 局部表达式的名称。 [!INCLUDE[tsql](../../includes/tsql-md.md)] 调试器列出变量、参数以及名称以 @@ 开头的系统函数。  
  
 **Value**  
 显示当前向该局部表达式分配的值。 如果尚未向该表达式分配任何值，则此列为空白。  
  
 如果表达式的长度超过了 **“值”** 列的宽度，则将指针移动到该表达式的 **“值”** 单元格上方可显示一条工具提示，指示该表达式的完整值。  
  
 **“值”** 单元格中的放大镜图标指示 [!INCLUDE[tsql](../../includes/tsql-md.md)] 调试器可视化工具可用。 在该列表中，可以指定 **“文本可视化工具”**、 **“XML 可视化工具”**或 **“HTML 可视化工具”**。 若要启动调试器可视化工具，请单击此放大镜图标。 [!INCLUDE[tsql](../../includes/tsql-md.md)] 调试器将打开一个对话框，该对话框以适合相应数据类型的格式显示这些数据。  
  
 **类型**  
 显示表达式的数据类型。  
  
## <a name="see-also"></a>另请参阅  
 [Transact-SQL 调试器](../../relational-databases/scripting/transact-sql-debugger.md)   
 [Transact-SQL 调试器信息](../../relational-databases/scripting/transact-sql-debugger-information.md)   
 [“监视”窗口](../../relational-databases/scripting/transact-sql-debugger-watch-window.md)   
 [“调用堆栈”窗口](../../relational-databases/scripting/transact-sql-debugger-call-stack-window.md)   
 [“快速监视”对话框](../../relational-databases/scripting/transact-sql-debugger-quickwatch-dialog-box.md)   
 [表达式 (Transact-SQL)](../../t-sql/language-elements/expressions-transact-sql.md)  
  
  
