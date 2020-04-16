---
title: ADOMD.NET服务器对象体系结构 |微软文档
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: reference
helpviewer_keywords:
- ADOMD.NET, object model
- object model [ADOMD.NET]
ms.assetid: bdc81de9-b390-4654-b62a-cd6c0c9ca10d
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 9b57155285b4758e37af43b0fb4f079d660b97fa
ms.sourcegitcommit: a3f5c3742d85d21f6bde7c6ae133060dcf1ddd44
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/15/2020
ms.locfileid: "81387917"
---
# <a name="adomdnet-server-object-architecture"></a>ADOMD.NET 服务器对象体系结构
  ADOMD.NET服务器对象是帮助对象，可用于在 中[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)][!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]创建用户定义的函数 （UF） 或存储过程。  
  
> [!NOTE]  
>  若要使用 `Microsoft.AnalysisServices.AdomdServer` 命名空间（以及这些对象），必须将对 msmgdsrv.dll 的引用添加到 UDF 项目或存储过程。  
  
 ![显示 ADOMD.NET 服务器的对象关系](../../analysis-services/dev-guide/media/adomdnetserverobjectmodel.gif "显示 ADOMD.NET 服务器的对象关系")  
ADOMD.NET 对象模型  
  
 与 ADOMD.NET 对象层次结构的交互通常从最顶层的一个或多个对象开始（如下表所述）。  
  
|目标|使用此对象|  
|--------|---------------------|  
|计算多维表达式 (MDX)|<xref:Microsoft.AnalysisServices.AdomdServer.Expression><br /> <xref:Microsoft.AnalysisServices.AdomdServer.Expression> 对象提供一种用于运行 MDX 表达式并在指定元组下计算该表达式的方法。|  
|提供对在不构造完整 MDX 语句的情况下执行 MDX 函数的支持|<xref:Microsoft.AnalysisServices.AdomdServer.MDX><br /> 在不使用 <xref:Microsoft.AnalysisServices.AdomdServer.MDX> 对象的情况下，<xref:Microsoft.AnalysisServices.AdomdServer.Expression> 对象很方便用于调用预定义的 MDX 函数。 在未来版本中应该会提供用于 <xref:Microsoft.AnalysisServices.AdomdServer.MDX> 对象的其他函数。|  
|表示 UDF 的当前执行上下文|<xref:Microsoft.AnalysisServices.AdomdServer.Context><br /> <xref:Microsoft.AnalysisServices.AdomdServer.Context> 对象会公开一些信息，例如，当前的多维数据集或挖掘模型以及各种元数据集合。 <xref:Microsoft.AnalysisServices.AdomdServer.Context> 对象的关键用法是 <xref:Microsoft.AnalysisServices.AdomdServer.Hierarchy.CurrentMember%2A> 对象的 <xref:Microsoft.AnalysisServices.AdomdServer.Hierarchy> 属性。 UDF 或存储过程作者可通过这种关键用法，根据查询针对的特定维度的成员做出决定。|  
|创建集和元组|<xref:Microsoft.AnalysisServices.AdomdServer.SetBuilder>, <xref:Microsoft.AnalysisServices.AdomdServer.TupleBuilder><br /> <xref:Microsoft.AnalysisServices.AdomdServer.SetBuilder> 提供一种创建不可变集的方法，而 <xref:Microsoft.AnalysisServices.AdomdServer.TupleBuilder> 提供一种创建不可变元组的方法。|  
|支持 MDX 语言的六种基本类型间的隐式转换和强制转换|<xref:Microsoft.AnalysisServices.AdomdServer.MDXValue><br /> <xref:Microsoft.AnalysisServices.AdomdServer.MDXValue> 对象提供下列类型间的隐式转换和强制转换：<br /><br /> -   <xref:Microsoft.AnalysisServices.AdomdServer.Hierarchy><br />-   <xref:Microsoft.AnalysisServices.AdomdServer.Level><br />-   <xref:Microsoft.AnalysisServices.AdomdServer.Member><br />-   <xref:Microsoft.AnalysisServices.AdomdServer.Tuple><br />-   <xref:Microsoft.AnalysisServices.AdomdServer.Set><br />- 标或值类型|  
  
## <a name="see-also"></a>另请参阅  
 [ADOMD.NET 服务器编程](https://docs.microsoft.com/bi-reference/adomd/multidimensional-models-adomd-net-server/adomd-net-server-programming)  
  
  
