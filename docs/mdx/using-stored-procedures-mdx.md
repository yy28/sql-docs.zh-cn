---
title: 使用存储的过程 (MDX) |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 0d4d455ed7bd804f4c2d4ce036c00f85fd94629f
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63251582"
---
# <a name="using-stored-procedures-mdx"></a>使用存储过程 (MDX)


  可通过编写 .NET 存储过程或用户定义的函数来扩展 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 和多维表达式 (MDX) 功能。 有关详细信息，请参阅[ADOMD.NET 服务器编程](https://docs.microsoft.com/bi-reference/adomd/multidimensional-models-adomd-net-server/adomd-net-server-programming)  
  
 当引用或调用存储过程时，应在括号前面指定函数名称。 可以在括号内指定表达式（称为“参数”），以提供要传递给参数的数据。 调用函数时，必须为所有参数提供参数值，并且必须按照用户定义函数中定义的相同参数顺序指定参数值。  
  
 以下示例查询假设您有一个在 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 服务器上注册的名为 SampleAssembly 的程序集：  
  
```  
SELECT SampleAssembly.RandomSample([Geography].[State-Province].Members, 5) on ROWS,   
[Date].[Calendar].[Calendar Year] on COLUMNS  
FROM [Adventure Works]  
WHERE [Measures].[Reseller Freight Cost]  
```  
  
> [!NOTE]  
>  *存储过程*是中使用的术语[!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]对于这些类型的函数。 早期版本[!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]调用这些类型的函数*用户定义的函数*。  
  
## <a name="types-of-stored-procedures"></a>类型的存储过程  
 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 支持 COM 程序集和 CLR 程序集。 建议使用 CLR 程序集，因为 CLR 程序集具有增强的安全性。 如果服务器上安装了 Microsoft Office Excel，也可以使用 Excel 功能。  
  
> [!NOTE]  
>  Microsoft Visual Basic for Applications (VBA) COM 程序集是自动注册的。  
  
## <a name="see-also"></a>请参阅  
 [函数&#40;MDX 语法&#41;](../mdx/functions-mdx-syntax.md)  
  
  
