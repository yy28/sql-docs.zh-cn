---
title: "在分析中的表格对象模型 (TOM) 简介服务 AMO |Microsoft 文档"
ms.custom: 
ms.date: 03/07/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: tabular-models
ms.reviewer: 
ms.suite: sql
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
ms.assetid: 57a4a934-ecd0-4365-8147-d36899d86751
caps.latest.revision: 15
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 96ec352784f060f444b8adcae6005dd454b3b460
ms.openlocfilehash: ab4bfb890124538878fd4d618dee05d393a4864c
ms.contentlocale: zh-cn
ms.lasthandoff: 09/27/2017

---
# <a name="introduction-to-the-tabular-object-model-tom-in-analysis-services-amo"></a>Analysis Services AMO 中表格对象模型 (TOM) 简介

[!INCLUDE[ssas-appliesto-sql2016-later-aas](../../includes/ssas-appliesto-sql2016-later-aas.md)]

  表格对象模型 (TOM) 是为支持的兼容性级别 1200年或更高版本生成的表格模型的编程方案创建的 Analysis Services 管理对象 (AMO) 客户端库的扩展。 使用 AMO，如 TOM 提供以编程方式处理管理功能，例如，创建模型、 导入和刷新数据，以及分配角色和权限。  
  
TOM 公开本机表格元数据，如**模型**，**表**，**列**，和**关系**对象。  对象模型树中，下面提供的高级视图说明了如何关联组件的各部分。  
  
 TOM 是 AMO 的扩展，因为中新的 Microsoft.AnalysisServices.Tabular.dll 程序集实现表示 SQL Server 2016 中引入的新表格对象的所有类。 AMO 的通用类移到 Microsoft.AnalysisServices.Core 程序集。 你的代码需要引用两个程序集。
请参阅[安装，请将分发，并引用表格对象模型 &#40;Microsoft.AnalysisServices.Tabular &#41;](../../analysis-services/tabular-model-programming-compatibility-level-1200/install-distribute-and-reference-the-tabular-object-model.md)有关详细信息。  
  
 目前，API 通过.NET framework 是仅适用于托管代码。 若要查看的编程选项，包括脚本和查询语言支持的完整列表请参阅[的兼容性级别 1200年的表格模型编程](../../analysis-services/tabular-model-programming-compatibility-level-1200/tabular-model-programming-for-compatibility-level-1200.md)。  
  
## <a name="tabular-object-model-hierarchy"></a>表格对象模型层次结构  
 从逻辑的角度来看，所有的表格对象形成一个树的根是**模型**、 位于数据库。 **服务器**和**数据库**不被视为"表格"的因为这些对象还可以表示在多维模式下或在较低的兼容性表格模型中运行的服务器上托管的多维数据库级别，不为对象定义使用表格元数据。 
  
 除**AttributeHierarchy**， **KPI**，和**LinguisticMetadata**，每个子对象可以是集合的成员。 例如，**模型**对象包含一套**表**对象 (通过**表**属性)，与每个**表**对象包含集合**列**对象，依次类推。  
  
 此层次结构中的任何父对象的最低级别后代是**批注**可以用于选择性地将架构扩展，只要你提供代码来处理它的对象。  
  
 ![对象层次结构关系图](../../analysis-services/tabular-model-programming-compatibility-level-1200/media/ssastomobjectmodeldiagram.png "对象层次结构关系图")  
  
## <a name="tom-and-other-related-technologies"></a>TOM 和其他相关的技术

TOM 是基础 AMO 基础结构，其中还可容纳多维和表格数据库兼容性级别 1200年以下生成的。

这具有一些实际含义。
所有，当你管理未在表格元数据中指定的对象的第一个 (如**服务器**或**数据库**)，你将需要利用现有的 AMO 堆栈的描述这些对象的部分。 旧的 API 以及为提供的对象状态服务器，或保存到服务器时在发现的精确说明的主版本号和次对象的概念。 Microsoft.AnalysisServices 命名空间下的 MajorObject 类公开的方法**刷新**和**更新**。 次要对象仅刷新或保存通过主要对象包含它们。

与此相反，当你管理属于表格元数据的对象 (如**模型**或**表**)，利用全新的表格堆栈。 在此堆栈中，更新都细化，这意味着每个元数据对象 (派生自**MetadataObject** Microsoft.AnalysisServices.Tabular 命名空间下的类) 可以单独保存到服务器。 通常情况下，你将发现整个**模型**，然后对其下的各个元数据对象进行更改 (如**表**或**列**)，然后调用**Model.SaveChanges()**方法 （这理解细粒度级别所做的更改），将命令发送到服务器以更新这些更改的对象。

### <a name="tom-and-xmla"></a>TOM 和 XMLA

在网络上 TOM 使用 XMLA 协议，与 Analysis Services 服务器进行通信并管理对象。 在管理非表格对象时，使用 TOM [ASSL](../scripting/analysis-services-scripting-language-assl-for-xmla.md)，XMLA Analysis Services 脚本语言扩展。 在管理表格对象时，TOM 使用 SSAS 表格协议，还 XMLA 的扩展。 请参阅[MS SSAS T SQL Server Analysis Services 表格协议文档](https://msdn.microsoft.com/library/mt719260.aspx)有关详细信息。

### <a name="tom-and-json"></a>TOM 和 JSON

表格元数据，在结构上作为 JSON 文档，都有新命令和对象模型定义的语法通过表格模型脚本语言[TMSL](../tabular-model-scripting-language-tmsl-reference.md)。 脚本语言 JSON 用于请求和响应的正文。

尽管 TMSL 和 TOM 公开相同的对象 (**表**，**列**，依此类推) 和相同的操作 (**创建**，**删除**， **刷新**)，TOM （它使用 MS SSAS 表格协议相反，按照前面的说明） 在网络上不使用 TMSL。

作为用户，你可以选择是否可管理通过 TOM 库从你的 C# 程序或 PowerShell 脚本，或通过 PowerShell、 SQL Server Management Studio (SSMS) 或 SQL Server 代理作业执行的 TMSL 脚本的表格数据库。

决定使用一个或另一个归结为你的要求的详细信息。 TOM 库提供了更丰富的功能相比 TMSL。 具体而言，TMSL 仅提供了在数据库、 表、 分区或角色级别粗粒度的操作，而 TOM 多更细颗粒度在允许的操作。 若要生成或以编程方式更新模型，你将需要 TOM 库中的 API 的完全程度。
  
## <a name="see-also"></a>另请参阅  
 [兼容级别 1200年的表格模型编程](../../analysis-services/tabular-model-programming-compatibility-level-1200/tabular-model-programming-for-compatibility-level-1200.md)   
 [Analysis Services 中表格模型的兼容级别](../../analysis-services/tabular-models/compatibility-level-for-tabular-models-in-analysis-services.md)  
[Analysis Services PowerShell](../../analysis-services/powershell/analysis-services-powershell-reference.md)
  

