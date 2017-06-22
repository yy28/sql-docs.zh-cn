---
title: "快速信息 (IntelliSense) | Microsoft Docs"
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
- Quick Info option [IntelliSense]
- declarations [IntelliSense]
- IntelliSense [SQL Server], Quick Info
- identifier declarations [IntelliSense]
ms.assetid: 3c8b59f4-1922-4bde-844f-5f2306514d96
caps.latest.revision: 33
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: b572aa4d72059f78a191e0045d3061f084a556e3
ms.contentlocale: zh-cn
ms.lasthandoff: 06/22/2017

---
# <a name="quick-info-intellisense"></a>快速信息 (IntelliSense)
  [!INCLUDE[msCoName](../../includes/msconame-md.md)] IntelliSense **“快速信息”** 选项可显示代码中任何标识符的完整声明。 将鼠标指针移到标识符上时，该标识符的声明便会显示在一个黄色的弹出窗口中。 在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]中，数据库引擎和 XML 查询编辑器中都提供 **“快速信息”** 。  
  
## <a name="transact-sql-quick-info"></a>Transact-SQL 快速信息  
 **“快速信息”** 在 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 查询编辑器中显示两类信息。 如果未处于调试模式， **“快速信息”** 显示表达式声明。 如果处于调试模式， **“快速信息”** 则会显示表达式的名称及其当前值。  
  
 在 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 查询编辑器中，只有 IntelliSense 支持的那些 **语法部分才能使用** “快速信息” [!INCLUDE[tsql](../../includes/tsql-md.md)] 。 例如，如果将鼠标指针移到某个对象的标识符上，但 IntelliSense 不支持该对象的数据类型，则“快速信息”弹出窗口会包含一条消息，说明不支持该数据类型。  
  
## <a name="see-also"></a>另请参阅  
 [IntelliSense 支持的 Transact-SQL 语法](../../relational-databases/scripting/transact-sql-syntax-supported-by-intellisense.md)  
  
  
