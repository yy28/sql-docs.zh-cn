---
title: "完成 Transact-SQL 代码段 | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- IntelliSense [SQL Server], completing snippets
- snippets [Transact-SQL], completing
- Transact-SQL snippets, completing
ms.assetid: a8316a58-bb57-485e-845f-84c23360314c
caps.latest.revision: 6
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 3cdeaf7c4fa9a002b25f0732f446d8e813234164
ms.contentlocale: zh-cn
ms.lasthandoff: 04/11/2017

---
# <a name="complete-transact-sql-snippets"></a>完成 Transact-SQL 代码段
  将 [!INCLUDE[tsql](../../includes/tsql-md.md)] 代码段插入脚本后，可以编辑代码段的内容以生成完整的 [!INCLUDE[tsql](../../includes/tsql-md.md)] 语句。  
  
## <a name="completing-snippets"></a>完成代码段  
 将 [!INCLUDE[tsql](../../includes/tsql-md.md)] 代码段添加到脚本时，插入的代码段语句具有一个或多个替换点，这些替换点会突出显示。 如果您将鼠标指针放在替换点上，会出现一个工具提示，其中包含您可以指定的语法元素的说明。 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 查询编辑器会将代码段与周围的脚本区分开，直到您关闭源文件。 替换点将保持活动状态，直到您关闭源文件。  
  
 您还可以向代码段所插入的模板代码中添加其他语法元素。 例如，创建表代码段模板生成两个列定义；您必须添加其他列定义才能创建具有两个以上列的表格。  
  
#### <a name="completing-the-snippet-statement"></a>完成代码段语句  
  
1.  使用 Tab 键从一个替换点移到下一个替换点。 使用 Shift+Tab 移到前一个替换点。  
  
2.  按 Ctrl+空格键以调用 IntelliSense。  
  
3.  从列表中选择一个项目，或键入您选择的替换内容。  
  
## <a name="see-also"></a>另请参阅  
 [插入 Transact-SQL 代码段](../../relational-databases/scripting/insert-transact-sql-snippets.md)   
 [插入外侧 Transact-SQL 代码段](../../relational-databases/scripting/insert-surround-with-transact-sql-snippets.md)  
  
  
