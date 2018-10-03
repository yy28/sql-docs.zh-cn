---
title: Transact-SQL 断点 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
helpviewer_keywords:
- Transact-SQL debugger, breakpoints
ms.assetid: c234430f-bd94-4d0d-9e74-2bf11681fa50
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 06342291cc73951043c14c6f29539eaf9f1be689
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2018
ms.locfileid: "48119473"
---
# <a name="transact-sql-breakpoints"></a>Transact-SQL 断点
  断点指定 [!INCLUDE[tsql](../../includes/tsql-md.md)] 调试器在特定 [!INCLUDE[tsql](../../includes/tsql-md.md)] 语句处暂停执行，这样您就可以查看该点的代码元素状态。  
  
## <a name="breakpoints"></a>断点  
 在运行 [!INCLUDE[tsql](../../includes/tsql-md.md)] 调试器时，您可以切换特定语句上的断点。 在执行到达具有断点的语句时，调试器将暂停执行，以便您可以查看调试信息，例如在变量和参数中存在的值。  
  
 您可以在编辑器窗口中单独管理断点，也可以使用 **“断点”** 窗口统一进行管理。 您可以编辑断点以便指定项，例如执行应暂停的特定条件，或者在执行断点时要执行的操作。  
  
## <a name="breakpoint-tasks"></a>断点任务  
  
|任务说明|主题|  
|----------------------|-----------|  
|说明如何指定想要调试器在其上暂停的 [!INCLUDE[tsql](../../includes/tsql-md.md)] 语句。|[切换断点](../spatial/point.md)|  
|说明如何暂时停用一个断点，并在以后将其重新激活。 还介绍了如何删除断点。|[启用、禁用和删除断点](enable-disable-and-delete-breakpoints.md)|  
|说明如何指定一个条件，该条件定义断点是否基于指定 Transact-SQL 表达式的计算结果而中断。|[指定断点条件](specify-a-breakpoint-condition.md)|  
|说明如何指定一个命中计数，该命中计数仅在包含断点的语句已执行了指定次数时才会导致断点中断。|[指定命中计数](specify-a-hit-count.md)|  
|说明如何指定一个筛选器，该筛选器使断点仅对于指定的进程或线程才会中断。|[指定断点筛选器](specify-a-breakpoint-filter.md)|  
|说明如何指定一个“命中条件”操作，该“命中条件”  操作是一种在执行断点语句时执行的自定义操作。 示例将打印一条消息。|[指定断点操作](specify-a-breakpoint-action.md)|  
|说明如何编辑断点的位置。|[编辑断点位置](edit-a-breakpoint-location.md)|  
  
## <a name="see-also"></a>请参阅  
 [Transact-SQL 调试器信息](transact-sql-debugger-information.md)  
  
  
