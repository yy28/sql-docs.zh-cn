---
title: ADOMD.NET 服务器对象体系结构 |Microsoft Docs
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
ms.openlocfilehash: 33a8f420f985c9e62c7d7f275e7de370a6988e8d
ms.sourcegitcommit: 04ba0ed3d860db038078609d6e348b0650739f55
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/27/2020
ms.locfileid: "85469052"
---
# <a name="adomdnet-server-object-architecture"></a>ADOMD.NET 服务器对象体系结构
  ADOMD.NET 服务器对象是 helper 对象，可用于在中创建用户定义的函数（Udf）或存储过程 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 。  
  
> [!NOTE]  
>  若要使用 `Microsoft.AnalysisServices.AdomdServer` 命名空间（以及这些对象），必须将对 msmgdsrv.dll 的引用添加到 UDF 项目或存储过程。  
  
 ![显示 ADOMD.NET 服务器的对象关系](../../analysis-services/dev-guide/media/adomdnetserverobjectmodel.gif "显示 ADOMD.NET 服务器的对象关系")  
ADOMD.NET 对象模型  
  
 与 ADOMD.NET 对象层次结构的交互通常从最顶层的一个或多个对象开始（如下表所述）。  
  
|功能|使用此对象|  
|--------|---------------------|  
|计算多维表达式 (MDX)|[Microsoft.analysisservices.sharepoint.integration.dll. AdomdServer](/previous-versions/sql/sql-server-2014/ms143609(v=sql.120))<br /> [Microsoft.analysisservices.sharepoint.integration.dll](/previous-versions/sql/sql-server-2014/ms143609(v=sql.120))对象提供一种方法来运行 MDX 表达式，并在指定的元组下计算该表达式。|  
|提供对在不构造完整 MDX 语句的情况下执行 MDX 函数的支持|[Microsoft.analysisservices.sharepoint.integration.dll. AdomdServer](/previous-versions/sql/sql-server-2014/ms143616(v=sql.120))<br /> 在不使用 Microsoft.analysisservices.sharepoint.integration.dll 对象的情况下调用预定义的 MDX 函数， [AdomdServer](/previous-versions/sql/sql-server-2014/ms143616(v=sql.120))对象非常方便[。](/previous-versions/sql/sql-server-2014/ms143609(v=sql.120)) [Microsoft.analysisservices.sharepoint.integration.dll. AdomdServer](/previous-versions/sql/sql-server-2014/ms143616(v=sql.120))对象的其他函数应在未来版本中可用。|  
|表示 UDF 的当前执行上下文|[Microsoft.analysisservices.sharepoint.integration.dll. AdomdServer](/previous-versions/sql/sql-server-2014/ms143353(v=sql.120))<br /> [Microsoft.analysisservices.sharepoint.integration.dll](/previous-versions/sql/sql-server-2014/ms143353(v=sql.120))对象公开当前多维数据集、挖掘模型和各种元数据集合等信息。 Microsoft.analysisservices.sharepoint.integration.dll 对象的一项关键用途是 AdomdServer[对象的 microsoft.analysisservices.sharepoint.integration.dll。 CurrentMember](/previous-versions/sql/sql-server-2014/ms143578(v=sql.120)) * 属性的[Microsoft.AnalysisServices.AdomdServer.Context](/previous-versions/sql/sql-server-2014/ms143353(v=sql.120))对象的. microsoft.analysisservices.sharepoint.integration.dll [*](/previous-versions/sql/sql-server-2014/ms137044(v=sql.120))属性。 UDF 或存储过程作者可通过这种关键用法，根据查询针对的特定维度的成员做出决定。|  
|创建集和元组|[Microsoft.analysisservices.sharepoint.integration.dll. AdomdServer. SetBuilder](/previous-versions/sql/sql-server-2014/ms144510(v=sql.120))， [microsoft.analysisservices.sharepoint.integration.dll](/previous-versions/sql/sql-server-2014/ms145407(v=sql.120)) . AdomdServer<br /> [Microsoft.analysisservices.sharepoint.integration.dll. AdomdServer. SetBuilder](/previous-versions/sql/sql-server-2014/ms144510(v=sql.120))提供了一种创建不可变集的方式，而[则提供](/previous-versions/sql/sql-server-2014/ms145407(v=sql.120))了一种创建不可变元组的方式。|  
|支持 MDX 语言的六种基本类型间的隐式转换和强制转换|[Microsoft.analysisservices.sharepoint.integration.dll. AdomdServer. MDXValue](/previous-versions/sql/sql-server-2014/ms143573(v=sql.120))<br /> [Microsoft.analysisservices.sharepoint.integration.dll. AdomdServer. MDXValue](/previous-versions/sql/sql-server-2014/ms143573(v=sql.120))对象提供以下类型之间的隐式转换和强制转换：<br /><br /> -   [Microsoft.analysisservices.sharepoint.integration.dll. AdomdServer](/previous-versions/sql/sql-server-2014/ms143578(v=sql.120))<br />-   [Microsoft.analysisservices.sharepoint.integration.dll. AdomdServer](/previous-versions/sql/sql-server-2014/ms143581(v=sql.120))<br />-   [Microsoft.analysisservices.sharepoint.integration.dll. AdomdServer](/previous-versions/sql/sql-server-2014/ms143820(v=sql.120))<br />-   [Microsoft.analysisservices.sharepoint.integration.dll. AdomdServer](/previous-versions/sql/sql-server-2014/ms145330(v=sql.120))<br />-   [Microsoft.analysisservices.sharepoint.integration.dll. AdomdServer。](/previous-versions/sql/sql-server-2014/ms144530(v=sql.120))<br />-标量或值类型|  
  
## <a name="see-also"></a>另请参阅  
 [ADOMD.NET 服务器编程](https://docs.microsoft.com/bi-reference/adomd/multidimensional-models-adomd-net-server/adomd-net-server-programming)  
  
  
