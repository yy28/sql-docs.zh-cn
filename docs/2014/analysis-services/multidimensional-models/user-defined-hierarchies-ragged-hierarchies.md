---
title: 不规则层次结构 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
helpviewer_keywords:
- ragged hierarchies [Analysis Services]
ms.assetid: e40a5788-7ede-4b0f-93ab-46ca33d0cace
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 69c39bb516c198005246d7d3dde5c588fd68cef1
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2018
ms.locfileid: "48087887"
---
# <a name="ragged-hierarchies"></a>不规则层次结构
  不规则层次结构是一种具有不规则级别数目的用户定义层次结构。 常见示例包括高级别经理将部门经理人员和非经理人员作为直接下属的组织图或是由“国家-地区-城市”组成的地理层次结构（其中某些城市没有父级“州”或“省”，如“华盛顿特区”、“梵蒂冈城”或“新德里”）。  
  
 对于某一维度中的大多数层次结构，每个级别上面的成员数与同一级别中任何其他成员上面的成员数相同。 不规则层次结构的不同之处在于，至少一个成员的逻辑父级不在该成员的直接上一级别中。 如果出现这种情况，则层次结构会降至其他级别以寻找其他深化路径。 在客户端应用程序中，这会让深化路径变得异常复杂。  
  
 各种客户端应用程序处理不规则层次结构的方式良莠不齐。 如果您的模型中存在不规则层次结构，请准备完成一点额外工作来获取所希望的呈现行为。  
  
 第一步是要检查客户端应用程序，看其如何处理深化路径。 例如，Excel 对于缺失值将父级名称表示为占位符。 若要自行查看此行为，请使用 Adventure Works 多维模型中的“销售区域”维度生成一个数据透视表。 在具有“销售区域”属性“组”、“国家/地区”和“区域”的数据透视表中，您会看到缺少区域值的国家/地区会获得一个占位符，在这种情况下表示对其上面父级（国家/地区名称）的重复。 此行为派生自在 Excel 中固定的 MDX Compatibility=1 连接字符串属性。 如果客户端没有自然提供您正在寻找的深化行为，那么您可以在模型中设置属性以至少更改其中的某些行为。  
  
 本主题包含以下各节：  
  
-   [修改不规则层次结构中的深化导航的方法](#bkmk_approach)  
  
-   [设置 HideMemberIf 以隐藏规则层次结构中的成员](#bkmk_Hide)  
  
-   [设置 MDX 兼容性以确定如何在客户端应用程序中表示占位符](#bkmk_Mdx)  
  
##  <a name="bkmk_approach"></a> 修改不规则层次结构中的深化导航的方法  
 当深化导航不返回预期值或被视为难以使用时，不规则层次结构的存在将成为问题。 若要解决不规则层次结构产生的导航问题，请考虑下列选项：  
  
-   使用不规则层次结构，但在每个级别上设置 `HideMemberIf` 属性以指定是否对用户可视化缺失级别。 设置时`HideMemberIf`，还应设置`MDXCompatibility`上的连接字符串以覆盖默认导航行为。 本主题中提供用于设置这些属性的说明。  
  
-   创建显式管理级别成员的父子层次结构。 有关这种方法的说明，请参阅 [SSAS 中的不规则层次结构（博客文章）](http://dwbi1.wordpress.com/2011/03/30/ragged-hierarchy-in-ssas/)。 联机丛书中的详细信息，请参阅[父-子层次结构](parent-child-dimension.md)。 创建父子层次结构的缺点是每个维度只能有一个层次结构，并且在为中间成员计算聚合时通常会引发性能损失。  
  
 如果您的维度包含一个以上不规则层次结构，则应使用第一种方法，设置`HideMemberIf`。 拥有使用不规则层次结构方面实际经验的 BI 开发人员可以更进一步，在物理数据表中进行其他更改，从而为每个级别创建单独的表。 有关这种方法的详细信息，请参阅 [Martin Mason 的 SSAS 财务多维数据集 – 第 1a 部分 – 不规则层次结构（博客）](http://martinmason.wordpress.com/2012/03/03/the-ssas-financial-cubepart-1aragged-hierarchies-cont/) 。  
  
##  <a name="bkmk_Hide"></a> 设置 HideMemberIf 以隐藏规则层次结构中的成员  
 在不规则维度的表中，逻辑上缺少的成员可以用其他方式表示。 表单元可以为空或包含空字符串，也可以包含与它们父级相同的值作为占位符。 占位符的表示形式由子成员的占位符状态（由 `HideMemberIf` 属性确定）和客户端应用程序的 `MDX Compatibility` 连接字符串属性确定。  
  
 对于支持显示不规则层次结构的客户端应用程序，可以使用这些属性隐藏逻辑上缺少的成员。  
  
1.  在 SSDT 中，双击一个维度可在维度设计器中将其打开。 第一个选项卡“维度结构”在“层次结构”窗格中显示属性层次结构。  
  
2.  右键单击层次结构中的成员并选择“属性”。 将 `HideMemberIf` 设置为下面描述的值之一。  
  
    |HideMemberIf 设置|Description|  
    |--------------------------|-----------------|  
    |`Never`|级别成员从不隐藏。 这是默认值。|  
    |**OnlyChildWithNoName**|如果级别成员是其父级的唯一子级，并且名称为空或空字符串，则隐藏该级别成员。|  
    |**OnlyChildWithParentName**|如果级别成员是其父级的唯一子级，并且名称与其父级名称相同，则隐藏该级别成员。|  
    |**NoName**|如果级别成员的名称为空，则隐藏该级别成员。|  
    |**ParentName**|如果级别成员的名称与其父级的名称相同，则隐藏该级别成员。|  
  
##  <a name="bkmk_Mdx"></a> 设置 MDX 兼容性以确定如何在客户端应用程序中表示占位符  
 设置后`HideMemberIf`上的层次结构级别，您还应设置`MDX Compatibility`从客户端应用程序发送的连接字符串中的属性。 `MDX Compatibility` 设置确定是否使用 `HideMemberIf`。  
  
|MDX Compatibility 设置|Description|用法|  
|-------------------------------|-----------------|-----------|  
|**1**|显示占位符值。|这是 Excel、SSDT 和 SSMS 使用的默认值。 它指示服务器在深化不规则层次结构中的空级别时返回占位符值。 如果单击占位符值，则可继续深化直到到达子（叶）节点。<br /><br /> Excel 拥有用于连接到 Analysis Services 的连接字符串，并且它始终在每个新连接上将 `MDX Compatibility` 设置为 1。 此行为将保留向后兼容性。|  
|**2**|隐藏占位符值（null 值或父级别的重复项），但显示具有相关值的其他级别和节点。|`MDX Compatibility`=2 通常被视为与不规则层次结构相关的首选设置。 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 报表和一些第三方客户端应用程序可保留此设置。|  
  
## <a name="see-also"></a>请参阅  
 [创建用户定义的层次结构](user-defined-hierarchies-create.md)   
 [用户层次结构](../multidimensional-models-olap-logical-dimension-objects/user-hierarchies.md)   
 [父-子层次结构](parent-child-dimension.md)   
 [连接字符串属性 (Analysis Services)](../../analysis-services/instances/connection-string-properties-analysis-services.md)  
  
  
