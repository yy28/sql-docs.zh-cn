---
title: "参数信息 (IntelliSense) | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "database-engine"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "参数信息选项 [IntelliSense]"
  - "存储函数参数完成 [Intellisense]"
  - "语言参考 [SQL Server]"
  - "IntelliSense [IntelliSense], 参数信息选项"
ms.assetid: 56c2aac9-c65c-4679-b62c-d9f689876dde
caps.latest.revision: 33
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 33
---
# 参数信息 (IntelliSense)
  使用 [!INCLUDE[msCoName](../../includes/msconame-md.md)] IntelliSense 的 **“参数信息”** 选项可打开一个参数列表，其中提供了有关函数或存储过程所需的参数数目、参数名称和参数类型的信息。 以粗体显示的参数指示键入某个函数或存储过程时所需的下一个参数。  
  
 对于嵌套函数，也会显示这一参数列表。 如果将一个函数键入为另一个函数的参数，则参数列表将显示内部函数的参数。 内部函数参数列表完成后，参数列表会还原为显示外部函数参数。  
  
#### 查看函数或存储过程的参数信息  
  
1.  在函数名称后面，以常用方式键入左括号，以打开参数列表。 键入存储过程的名称后，照常键入空格以获取有关该过程参数的信息。  
  
     IntelliSense 将在插入点下方的弹出窗口中显示存储过程的函数或参数的完整声明。 列表中的第一个参数以粗体显示。  
  
2.  键入参数时，粗体会更改以反映您要输入的下一个参数。  
  
3.  按 ESC 随时关闭列表，或继续键入直到函数键入完成。  
  
     对于函数，如果键入右括号，还会关闭参数列表。  
  
#### 手动引导参数信息  
  
1.  在 **“编辑”** 菜单上，选择 **IntelliSense** ，再选择 **“参数信息”**。  
  
2.  按键盘快捷键 Ctrl+Shift+空格键。  
  
 有关详细信息，请参阅[配置 IntelliSense (SQL Server Management Studio)](../../relational-databases/scripting/configure-intellisense-sql-server-management-studio.md)。  
  
> [!NOTE]  
>  “参数信息”**选项仅可用于 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 查询编辑器和 XML 查询编辑器。  
  
  