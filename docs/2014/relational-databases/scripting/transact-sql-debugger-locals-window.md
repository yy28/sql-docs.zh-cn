---
title: “局部变量”窗口 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- Locals Window [Transact-SQL]
ms.assetid: 59bea640-7823-4b4d-832c-f384d83cca2f
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 503a92349f7b7cfecdd4bd72de507da0a5835f7d
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "66063383"
---
# <a name="locals-window"></a>“局部变量”窗口
  **“局部变量”** 窗口显示有关 [!INCLUDE[tsql](../../includes/tsql-md.md)] 调试器的当前作用域中局部表达式的信息。 此作用域设定为在 **“调用堆栈”** 窗口中选择的当前调用堆栈帧。 只有在调试模式下才可以显示局部表达式。  
  
## <a name="task-list"></a>任务列表  
 **访问“局部变量”窗口**  
  
-   在 **“调试”** 菜单上单击 **“窗口”**，然后单击 **“局部变量”**。  
  
 **更改表达式的值**  
  
-   右键单击表达式，然后选择“编辑值”。  
  
## <a name="columns"></a>“列”  
 **名称**  
 局部表达式的名称。 [!INCLUDE[tsql](../../includes/tsql-md.md)] 调试器列出变量、参数以及名称以 @@ 开头的系统函数。  
  
 **Value**  
 显示当前向该局部表达式分配的值。 如果尚未向该表达式分配任何值，则此列为空白。  
  
 如果表达式的长度超过了 **“值”** 列的宽度，则将指针移动到该表达式的 **“值”** 单元格上方可显示一条工具提示，指示该表达式的完整值。  
  
 **“值”** 单元格中的放大镜图标指示 [!INCLUDE[tsql](../../includes/tsql-md.md)] 调试器可视化工具可用。 在该列表中，可以指定 **“文本可视化工具”**、 **“XML 可视化工具”** 或 **“HTML 可视化工具”**。 若要启动调试器可视化工具，请单击此放大镜图标。 [!INCLUDE[tsql](../../includes/tsql-md.md)] 调试器将打开一个对话框，该对话框以适合相应数据类型的格式显示这些数据。  
  
 **类型**  
 显示表达式的数据类型。  
  
## <a name="see-also"></a>请参阅  
 [Transact-SQL 调试器](transact-sql-debugger.md)   
 [Transact-SQL 调试器信息](transact-sql-debugger-information.md)   
 [“监视”窗口](transact-sql-debugger-watch-window.md)   
 [“调用堆栈”窗口](transact-sql-debugger-call-stack-window.md)   
 [“快速监视”对话框](transact-sql-debugger-quickwatch-dialog-box.md)   
 [表达式 (Transact-SQL)](/sql/t-sql/language-elements/expressions-transact-sql)  
