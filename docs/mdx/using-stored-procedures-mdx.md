---
title: "使用存储的过程 (MDX) |Microsoft 文档"
ms.custom: 
ms.date: 03/02/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: analysis-services
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs: kbMDX
helpviewer_keywords:
- user-defined functions [MDX]
- stored procedures [MDX]
ms.assetid: 818fb2ad-f88b-4d0c-9f70-f378aed42e8e
caps.latest.revision: "27"
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.openlocfilehash: 187b71551aa1001a777486da08f3f10e171f2302
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/09/2017
---
# <a name="using-stored-procedures-mdx"></a>使用存储过程 (MDX)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  可通过编写 .NET 存储过程或用户定义的函数来扩展 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 和多维表达式 (MDX) 功能。 有关详细信息，请参阅[ADOMD.NET Server 编程](../analysis-services/multidimensional-models-adomd-net-server/adomd-net-server-programming.md)  
  
 当引用或调用存储过程时，应在括号前面指定函数名称。 可以在括号内指定表达式（称为“参数”），以提供要传递给参数的数据。 调用函数时，必须为所有参数提供参数值，并且必须按照用户定义函数中定义的相同参数顺序指定参数值。  
  
 以下示例查询假设您有一个在 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 服务器上注册的名为 SampleAssembly 的程序集：  
  
```  
SELECT SampleAssembly.RandomSample([Geography].[State-Province].Members, 5) on ROWS,   
[Date].[Calendar].[Calendar Year] on COLUMNS  
FROM [Adventure Works]  
WHERE [Measures].[Reseller Freight Cost]  
```  
  
> [!NOTE]  
>  *存储过程*是中使用的术语[!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]为这些类型的函数。 早期版本的[!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]调用这些类型的函数作为*用户定义函数*。  
  
## <a name="types-of-stored-procedures"></a>存储过程的类型  
 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 支持 COM 程序集和 CLR 程序集。 建议使用 CLR 程序集，因为 CLR 程序集具有增强的安全性。 如果服务器上安装了 Microsoft Office Excel，也可以使用 Excel 功能。  
  
> [!NOTE]  
>  Microsoft Visual Basic for Applications (VBA) COM 程序集是自动注册的。  
  
## <a name="see-also"></a>另请参阅  
 [函数 &#40;MDX 语法 &#41;](../mdx/functions-mdx-syntax.md)  
  
  
