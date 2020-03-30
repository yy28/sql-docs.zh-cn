---
title: 指定断点条件
titleSuffix: T-SQL debugger
ms.prod: sql
ms.technology: scripting
ms.topic: conceptual
helpviewer_keywords:
- Transact-SQL debugger, breakpoint conditions
ms.assetid: b43d8a2b-99a3-4fb7-8848-99c042ea7ef7
author: markingmyname
ms.author: maghan
ms.custom: seo-lt-2019
ms.reviewer: ''
ms.date: 12/04/2019
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 3fafd999d5e144c8e71364c952ca8047411a3aaf
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/29/2020
ms.locfileid: "75253640"
---
# <a name="specify-a-breakpoint-condition"></a>指定断点条件

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

断点条件是当到达断点时，由调试器计算的 [!INCLUDE[tsql](../../includes/tsql-md.md)] 表达式。 如果满足条件，并且达到任何指定的命中计数，则调试器或者中断，或者执行为断点指定的操作。  

[!INCLUDE[ssms-old-versions](../../includes/ssms-old-versions.md)]

## <a name="specifying-conditions"></a>指定条件

指定的表达式必须是计算结果为布尔值的有效 Transact-SQL 表达式。 有关详细信息，请参阅[表达式 (Transact-SQL)](../../t-sql/language-elements/expressions-transact-sql.md)。  
  
 如果用于指定断点条件的语法无效，则会立即出现一条警告消息。 如果用于指定条件的语法有效但语义无效，则会在第一次命中断点时显示一条警告消息。 在这两种情况下，当命中无效断点时，调试器都将中断执行。  
  
#### <a name="to-specify-a-condition"></a>指定条件
  
1. 在编辑器窗口中，右键单击断点符号，然后单击快捷菜单上的“条件”  。  
  
     -或-  
  
     在“断点”  窗口中，右键单击断点符号，然后单击快捷菜单上的“条件”  。  
  
2. 在 **“断点条件”** 对话框中，在 **“条件”** 框中输入一个有效的布尔表达式。  
  
3. 如果希望在表达式的计算结果为 **true** 时断开，则选择 **“为 true”** ，如果希望在表达式的值发生更改时断开，则选择 **“已更改”** 。  
  
    > [!NOTE]  
    >  在第一次到达断点之前，调试器不会计算布尔表达式。 如果选择 **“已更改”** ，则调试器不会将第一次计算视为一项更改，因此不会在第一次计算时中断。  
  
## <a name="see-also"></a>另请参阅

- [指定命中计数](../../relational-databases/scripting/specify-a-hit-count.md)
- [指定断点操作](../../relational-databases/scripting/specify-a-breakpoint-action.md)
