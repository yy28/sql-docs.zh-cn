---
title: 操作 (Analysis Services-多维数据) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- actions [Analysis Services]
- actions [Analysis Services], about actions
- MDX [Analysis Services], actions
- cubes [Analysis Services], actions
- OLAP objects [Analysis Services], actions
ms.assetid: 07229bb2-805c-427e-8455-69c9ca5d01e0
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 3ff4e330950a3fca54ba8ab08456157156836c0f
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/23/2019
ms.locfileid: "66077591"
---
# <a name="actions-analysis-services---multidimensional-data"></a>操作（Analysis Services - 多维数据）
  操作可以具有不同的类型，因而必须相应地进行创建。 操作可为：  
  
-   钻取操作，对于在其上执行了该操作的多维数据，该操作将返回表示其所选单元的基础数据的行集。  
  
-   报告操作，对于在其上执行了该操作的多维数据，该操作将从 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 返回一个与其所选部分关联的报表。  
  
-   标准操作，对于在其上执行了该操作的多维数据，该操作将返回与其所选部分关联的操作元素（URL、HTML、DataSet、RowSet 及其他元素）。  
  
 客户端应用程序可以使用查询接口（如 ADOMD.NET）来检索操作并向最终用户公开它们。 有关详细信息，请参阅 [使用 ADOMD.NET 进行开发](https://docs.microsoft.com/bi-reference/adomd/developing-with-adomd-net)。  
  
 简单 <xref:Microsoft.AnalysisServices.Action> 对象由基本信息、操作目标、用于限制操作范围的条件以及类型组成。 基本信息包括操作名称、操作说明、操作的建议标题等。  
  
 目标指操作在多维数据集中的实际执行位置。 目标由目标类型和目标对象组成。 目标类型表示要在其中启用操作的多维数据集中的对象的类型。 目标类型可为级别成员、单元、层次结构、层次结构成员等。 目标对象是目标类型的特定对象；如果目标类型为层次结构，则目标对象将为多维数据集中定义的任一层次结构。  
  
 条件是操作事件发生时计算的 `Boolean` MDX 表达式。 如果条件的计算结果为 `true` 时，则将执行操作。 否则，不执行操作。  
  
 类型是要执行的操作的类型。 <xref:Microsoft.AnalysisServices.Action> 是一个抽象类；因此，若要使用该类，你必须使用任一派生类。 预定义了两种类型的操作：钻取和报告。 这两种类型的操作具有相应的派生类： <xref:Microsoft.AnalysisServices.DrillThroughAction> 和 <xref:Microsoft.AnalysisServices.ReportAction>。 其他操作包含在 <xref:Microsoft.AnalysisServices.StandardAction> 类中。  
  
 在 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]中，操作指可提供给客户端应用程序并可由客户端应用程序使用的已存储 MDX 语句。 换言之，操作是指在服务器中定义并存储的客户端命令。 操作还包含了指定客户端应用程序应当何时以及如何显示和处理 MDX 语句的信息。 由操作指定的动作可以通过将操作中的信息用作参数来启动应用程序，也可以基于操作所提供的条件来检索信息。  
  
 通过操作，业务用户可以根据分析结果进行操作。 通过保存和重用操作，最终用户可以超越以提供数据为目的的传统分析，针对已发现的问题和缺点启动解决方案，从而扩展了商业智能应用程序，使之超越了多维数据集。 操作可以将客户端应用程序从复杂的数据呈现工具变为企业运营系统的组成部分。 最终用户不必将注意力集中在如何将数据作为输入发送到运营状况应用程序，他们可以在决策过程中“关闭循环”。 对于成功的商业智能应用程序来说，这种将分析数据转换为决定的功能是至关紧要的。  
  
 例如，浏览多维数据集的业务用户会注意到某个特定产品的当前股票值很低。 客户端应用程序为业务用户提供了一个操作列表，它们全部都与从 Analysis Services 数据库检索到的较低的产品股票值相关。业务用户将为表示产品的多维数据集的成员选择 Order 操作。 Order 操作通过调用运营数据库中的存储过程启动新的订单。 此存储过程会生成相应信息，以发送到订单输入系统。  
  
 创建操作时可以充分运用它的灵活性：例如，操作可以启动应用程序，也可以从数据库检索信息。 可以将操作配置为可由多维数据集的几乎所有部分（包括维度、级别、成员和单元）所触发，还将为多维数据集的同一部分创建多个操作。 还可以将字符串参数传送到已启动的应用程序，并指定在操作运行时显示给最终用户的标题。  
  
> [!IMPORTANT]  
>  为使业务用户使用操作，业务用户所使用的客户端应用程序必须支持这些操作。  
  
## <a name="types-of-actions"></a>操作的类型  
 下表列出了 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]中包含的操作类型：  
  
|操作类型|Description|  
|-----------------|-----------------|  
|CommandLine|在命令提示符下执行命令|  
|数据集|将数据集返回到客户端应用程序。|  
|钻取|将钻取语句作为表达式返回，客户端将执行此语句以返回行集|  
|Html|在 Internet 浏览器中执行 HTML 脚本|  
|专有|使用除此表列出的这些类型以外的其他接口执行操作。|  
|报告|将基于参数化 URL 的请求提交到报表服务器，并将报表返回到客户端应用程序。|  
|行集|将行集返回到客户端应用程序。|  
|声明专用纸|运行 OLE DB 命令。|  
|URL|在 Internet 浏览器中显示动态网页。|  
  
## <a name="resolving-and-executing-actions"></a>解析并执行操作  
 当业务用户在访问已为其定义了命令对象的对象时，系统将自动解析与操作关联的语句，以使它对客户端应用程序可用，但操作不会自动执行。 操作只在业务用户执行启动它的客户端特定操作时才被执行。 例如，当业务用户右键单击特定的成员或单元时，客户端应用程序可能以弹出菜单的形式显示一组操作。  
  
## <a name="see-also"></a>请参阅  
 [多维模型中的操作](actions-in-multidimensional-models.md)  
  
  
