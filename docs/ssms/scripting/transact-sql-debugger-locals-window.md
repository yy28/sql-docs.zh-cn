---
title: “局部变量”窗口
titleSuffix: T-SQL debugger
ms.prod: sql
ms.technology: scripting
ms.topic: conceptual
helpviewer_keywords:
- Locals Window [Transact-SQL]
ms.assetid: 59bea640-7823-4b4d-832c-f384d83cca2f
author: markingmyname
ms.author: maghan
ms.reviewer: ''
ms.custom: seo-lt-2019
ms.date: 12/04/2019
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 70ee1eee120c94e7f851bc37c3becf1983a57d09
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/29/2020
ms.locfileid: "75253055"
---
# <a name="transact-sql-debugger---locals-window"></a>Transact-SQL 调试器 -“局部变量”窗口

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

**“局部变量”** 窗口显示有关 [!INCLUDE[tsql](../../includes/tsql-md.md)] 调试器的当前作用域中局部表达式的信息。 此作用域设定为在 **“调用堆栈”** 窗口中选择的当前调用堆栈帧。 只有在调试模式下才可以显示局部表达式。  

[!INCLUDE[ssms-old-versions](../../includes/ssms-old-versions.md)]

## <a name="task-list"></a>任务列表

**访问“局部变量”窗口**
  
-   在 **“调试”** 菜单上单击 **“窗口”** ，然后单击 **“局部变量”** 。  
  
 **更改表达式的值**  
  
-   右键单击表达式，然后选择“编辑值”  。  
  
## <a name="columns"></a>列  
 **名称**  
 局部表达式的名称。 [!INCLUDE[tsql](../../includes/tsql-md.md)] 调试器列出变量、参数以及名称以 @@ 开头的系统函数。  
  
 **值**  
 显示当前向该局部表达式分配的值。 如果尚未向该表达式分配任何值，则此列为空白。  
  
 如果表达式的长度超过了 **“值”** 列的宽度，则将指针移动到该表达式的 **“值”** 单元格上方可显示一条工具提示，指示该表达式的完整值。  
  
 **“值”** 单元格中的放大镜图标指示 [!INCLUDE[tsql](../../includes/tsql-md.md)] 调试器可视化工具可用。 在该列表中，可以指定 **“文本可视化工具”** 、 **“XML 可视化工具”** 或 **“HTML 可视化工具”** 。 若要启动调试器可视化工具，请单击此放大镜图标。 [!INCLUDE[tsql](../../includes/tsql-md.md)] 调试器将打开一个对话框，该对话框以适合相应数据类型的格式显示这些数据。  
  
 类型   
 显示表达式的数据类型。  
  
## <a name="see-also"></a>另请参阅  
 [Transact-SQL 调试器](../../relational-databases/scripting/transact-sql-debugger.md)   
 [Transact-SQL 调试器信息](../../relational-databases/scripting/transact-sql-debugger-information.md)   
 [“监视”窗口](../../relational-databases/scripting/transact-sql-debugger-watch-window.md)   
 [“调用堆栈”窗口](../../relational-databases/scripting/transact-sql-debugger-call-stack-window.md)   
 [“快速监视”对话框](../../relational-databases/scripting/transact-sql-debugger-quickwatch-dialog-box.md)   
 [表达式 (Transact-SQL)](../../t-sql/language-elements/expressions-transact-sql.md)  
