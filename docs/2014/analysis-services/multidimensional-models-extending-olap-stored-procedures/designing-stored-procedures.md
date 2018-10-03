---
title: 设计存储的过程 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
helpviewer_keywords:
- stored procedures [Analysis Services], designing
- dependent assemblies [Analysis Services]
- assemblies [Analysis Services]
ms.assetid: af4e7bd5-041b-4a40-9942-0ef6a3af46c6
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: b05a4b7b1fe1c8ee70692472dc69105f01a275e0
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2018
ms.locfileid: "48164427"
---
# <a name="designing-stored-procedures"></a>设计存储过程
  管理对象模型 Analysis Management Objects (AMO) 和面向客户端的对象模型 [!INCLUDE[msCoName](../../includes/msconame-md.md)] ActiveX® 数据对象（多维）(ADO MD) 在存储过程中都可用。  
  
 存储过程必须在作用域（服务器或数据库）内，才可以在要调用的多维表达式 (MDX) 级别中可见。 但是，调用存储过程后，它的作用域将不再限于其父级下的操作。 存储过程可能会在服务器的任何位置进行更改或修改，并且只有调用它的用户进程的安全性会对其进行限制，或者只有它所操作的事务对其进行限制。  
  
 在服务器的所有上下文中，服务器作用域过程都是可用的。 数据库作用域存储过程只在定义它们的数据库的数据库上下文中是可见的。  
  
 与任何 MDX 函数一样，必须先解析存储过程，然后 MDX 会话才能继续；存储过程在执行时将锁定 MDX 会话。 除非出于特定的原因要停止 MDX 会话，以挂起用户交互，否则禁止进行用户交互（例如，对话框）。  
  
## <a name="dependent-assemblies"></a>依赖程序集  
 必须将所有依赖程序集加载到公共语言运行时 (CLR) 要查找的 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 实例中。 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 将依赖程序集存储在与主程序集相同的文件夹中，因此 CLR 将自动解析针对这些程序集中函数的所有函数引用。  
  
## <a name="see-also"></a>请参阅  
 [多维模型程序集管理](../multidimensional-models/multidimensional-model-assemblies-management.md)   
 [定义存储过程](../multidimensional-models-extending-olap-stored-procedures/defining-stored-procedures.md)  
  
  
