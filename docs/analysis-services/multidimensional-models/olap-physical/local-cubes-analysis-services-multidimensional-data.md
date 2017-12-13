---
title: "本地多维数据集 (Analysis Services-多维数据) |Microsoft 文档"
ms.custom: 
ms.date: 03/16/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
applies_to: SQL Server 2016 Preview
helpviewer_keywords: cubes [Analysis Services], local
ms.assetid: e52e1515-35a7-4dc3-9bbf-736d176ba0c7
caps.latest.revision: "13"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 06178b8d1023a95433d76543ff05db4d9c654a27
ms.sourcegitcommit: f1a6944f95dd015d3774a25c14a919421b09151b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/08/2017
---
# <a name="local-cubes-analysis-services---multidimensional-data"></a>本地多维数据集（Analysis Services - 多维数据）
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]若要创建、 更新或删除本地多维数据集，你必须编写和执行 ASSL 脚本或 AMO 程序。  
  
 本地多维数据集和本地挖掘模型允许在客户端工作站与网络的连接断开时对该工作站进行分析。 例如，客户端应用程序可能调用 OLE DB for OLAP 9.0 访问接口 (MSOLAP.3)，该接口将加载本地多维数据集引擎以创建和查询本地多维数据集，如下图所示：  
  
 ![本地多维数据集和模型的客户端体系结构](../../../analysis-services/multidimensional-models/olap-physical/media/as-localcubearch9.gif "本地多维数据集和模型的客户端体系结构")  
  
 在与本地多维数据集进行交互时，ADMOD.NET 和 Analysis Management Objects (AMO) 也将加载本地多维数据集引擎。 只有一个进程可以访问本地多维数据集文件，这是因为本地多维数据集引擎建立到本地多维数据集的连接时将以独占方式锁定本地多维数据集文件。 对于一个进程，最多允许同时有五个连接。  
  
 一个 .cub 文件可以包含多个多维数据集或数据挖掘模型。 对本地多维数据集和数据挖掘模型的查询可通过本地多维数据集引擎处理，不需要连接到 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 实例。  
  
> [!NOTE]  
>  不支持使用 [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] 和 [!INCLUDE[ssBIDevStudioFull](../../../includes/ssbidevstudiofull-md.md)] 来管理本地多维数据集。  
  
## <a name="local-cubes"></a>本地多维数据集  
 可以创建本地多维数据集，并将其从任一现有多维数据集在填充[!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]实例或从关系数据源。  
  
|本地多维数据集的数据源|创建方法|  
|------------------------------------|---------------------|  
|基于服务器的多维数据集|你可以使用 CREATE GLOBAL CUBE 语句或[!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]脚本语言 (ASSL) 脚本，创建并填充多维数据集的基于服务器的多维数据集。 有关详细信息，请参阅[创建全局多维数据集语句 &#40;MDX &#41;](../../../mdx/mdx-data-definition-create-global-cube.md)或[Analysis Services 脚本语言 &#40;ASSL 为 XMLA &#41;](../../../analysis-services/scripting/analysis-services-scripting-language-assl-for-xmla.md).|  
|关系数据源|可以使用 ASSL 脚本从 OLE DB 关系数据库创建和填充多维数据集。 若要使用 ASSL 创建本地多维数据集，只需连接到本地多维数据集文件 (*.cub)，并以与针对 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 实例执行 ASSL 脚本创建服务器多维数据集的相同方式执行 ASSL 脚本。 有关详细信息，请参阅 [Analysis Services 脚本语言（支持 XMLA 的 ASSL）](../../../analysis-services/scripting/analysis-services-scripting-language-assl-for-xmla.md)。|  
  
 使用 REFRESH CUBE 语句可重新生成本地多维数据集并更新其数据。 有关详细信息，请参阅[刷新多维数据集语句 &#40;MDX &#41;](../../../mdx/mdx-data-definition-refresh-cube.md).  
  
### <a name="local-cubes-created-from-server-based-cubes"></a>从基于服务器的多维数据集创建的本地多维数据集  
 从基于服务器的多维数据集创建本地多维数据集时，应注意以下事项：  
  
-   不支持非重复计数度量值。  
  
-   添加度量值时，还必须至少包含一个与要添加的度量值相关的维度。 有关维度关系的度量值组的详细信息，请参阅[维度关系](../../../analysis-services/multidimensional-models-olap-logical-cube-objects/dimension-relationships.md)。  
  
-   添加父子层次结构时，将忽略父子层次结构的级别和筛选器，而将包括整个父子层次结构。  
  
-   不创建成员属性。  
  
-   包括半累加性度量值时，在帐户维度或时间维度上不允许进行切片。  
  
-   始终会具体化引用维度。  
  
-   包含多对多维度时，适用以下规则：  
  
    -   不能对多对多维度进行切片。  
  
    -   必须从中间度量值组添加度量值。  
  
    -   不能对任何对于多对多关系中涉及的两个度量值组通用的维度进行切片。  
  
-   只有那些依赖于添加到本地多维数据集中的度量值和维度的计算成员、命名集和分配会显示在本地多维数据集中。 将自动排除无效计算成员、命名集和分配。  
  
### <a name="security"></a>安全性  
 为了使用户从服务器多维数据集创建本地多维数据集，用户必须被授予**钻取和本地多维数据集**对服务器多维数据集的权限。 有关详细信息，请参阅[授予多维数据集或模型权限 &#40;Analysis Services &#41;](../../../analysis-services/multidimensional-models/grant-cube-or-model-permissions-analysis-services.md).  
  
 使用诸如服务器多维数据集之类的角色无法确保本地多维数据集的安全。 拥有对本地多维数据集文件的文件级访问权限的任何用户均可在此文件中查询多维数据集。 你可以使用**加密密码**上要在本地多维数据集文件设置的密码的本地多维数据集文件的连接属性。 如果为本地多维数据集文件设置密码，则与该本地多维数据集文件的所有连接都需要使用此密码才能查询该文件。  
  
## <a name="see-also"></a>另请参阅  
 [创建全局多维数据集语句 &#40;MDX &#41;](../../../mdx/mdx-data-definition-create-global-cube.md)   
 [使用 Analysis Services 脚本语言 &#40; 进行开发ASSL &#41;](../../../analysis-services/multidimensional-models/scripting-language-assl/developing-with-analysis-services-scripting-language-assl.md)   
 [刷新多维数据集语句 &#40;MDX &#41;](../../../mdx/mdx-data-definition-refresh-cube.md)  
  
  
