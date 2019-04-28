---
title: 链接度量值组 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
helpviewer_keywords:
- linked measure groups [Analysis Services]
- referencing measure groups
- Linked Measure Group Wizard
- measure groups [Analysis Services], linked
- linked dimensions [Analysis Services]
ms.assetid: 7f838452-8669-4194-8e15-7afdc7f15251
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: f7695f971504744d42056d0067217e102ef3d990
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62700287"
---
# <a name="linked-measure-groups"></a>链接度量值组
  链接度量值组基于同一数据库内不同多维数据集中的另一度量值组，或基于一个不同的 Analysis Services 数据库。 如果要在多个多维数据集中重用一组度量值以及对应的数据值，可能使用链接度量值组。  
  
 Microsoft 建议原始和链接度量值组驻留于在同一台服务器上运行的解决方案中。 链接到远程服务器上的度量值组计划为在将来的版本中不推荐使用 (请参阅[SQL Server 2014 中不推荐使用 Analysis Services 功能](../deprecated-analysis-services-features-in-sql-server-2014.md))。  
  
> [!IMPORTANT]  
>  链接度量值组为只读的。 要获得最新更改，您必须基于已修改的源对象删除并重新创建所有链接度量值组。 因此，在以后需要修改度量值组时，应考虑是否可以采用在两个项目间复制和粘贴度量值组这个替代方法。  
  
## <a name="usage-limitations"></a>使用限制  
 如前所述，使用链接度量值的一个重要约束是无法直接自定义链接度量值。 对数据类型、格式、数据绑定和可见性以及度量值组本身中项目的成员身份的修改都是必须在原始度量值组中进行的更改。  
  
 根据需要，在客户端应用程序对其进行访问时，链接度量值组与其他度量值组相同，并且其查询方式与其他度量值组的查询方式相同。  
  
 查询包含链接度量值组的多维数据集时，会在目标多维数据集的第一次计算传递期间建立和解析链接。 受此行为影响，任何存储在链接度量值组中的计算都不会在计算查询之前进行解析； 换言之，必须在目标多维数据集中重新创建计算度量值和计算单元，而不是从源多维数据集中继承。  
  
 下面的列表汇总了使用限制。  
  
-   不能通过另一个链接度量值组创建链接度量值组。  
  
-   无法在链接度量值组中添加或删除度量值。 成员身份仅在原始度量值组中定义。  
  
-   链接度量值组中不支持写回。  
  
-   链接度量值组无法在多个多对多关系中使用（尤其是在这些关系处于不同多维数据集中时）。 这样做可能导致不明确的聚合。 有关详细信息，请参阅 [Incorrect Amounts for Linked Measures in Cubes containing Many-to-Many Relationships](https://social.technet.microsoft.com/wiki/contents/articles/22911.incorrect-amounts-for-linked-measures-in-cubes-containing-many-to-many-relationships-ssas-troubleshooting.aspx)（包含多对多关系的多维数据集中链接度量值的不正确数量）。  
  
 链接度量值组中包含的度量值只能直接与从同一 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 数据库中检索到的链接维度一起组织。 但是，您可以使用计算成员将来自链接度量值组的信息与多维数据集中的其他非链接维度进行关联。 您还可以使用间接关系（例如，引用关系或多对多关系）将非链接维度与链接度量值组进行关联。  
  
## <a name="create-or-modify-a-linked-measure"></a>创建或修改链接度量值  
 使用 [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)] 可创建链接度量值组。  
  
1.  在源多维数据集中立即完成对原始度量值组的所有修改，这样不必在后续多维数据集中重新创建链接度量值组。 可以重命名链接对象，但是无法更改任何其他属性。  
  
2.  在解决方案资源管理器中，双击要向其添加链接度量值组的多维数据集。 此步骤在多维数据集设计器中打开多维数据集。  
  
3.  在多维数据集设计器中的“度量值”窗格或“维度”窗格上，右键单击任一窗格中的任何位置，然后选择“新建链接对象”。 这会启动链接对象向导。  
  
4.  在第一页上，指定数据源。 此步骤建立原始度量值组的位置。 默认值是当前数据库中的当前多维数据集，不过也可以选择其他 Analysis Services 数据库。  
  
5.  在下一页中，选择要链接的度量值组或维度。 维度和多维数据集对象（如度量值组）会分别列出。 只有当前多维数据集中尚不存在的对象才可用。  
  
6.  单击 **“完成”** 创建链接对象。 链接对象出现在“度量值”和“维度”窗格中（通过链接图标指示）。  
  
## <a name="secure-a-linked-measure"></a>保护链接度量值  
 定义了链接之后，在管理对链接度量值组中度量值的访问时，将采用与管理对其他度量值组的访问相同的方式。 链接对象与其非链接对等对象一起出现在角色设计器中。 有关管理度量值组安全性的详细信息，请参阅[授予多维数据集或模型权限 (Analysis Services)](grant-cube-or-model-permissions-analysis-services.md)。  
  
 为了定义或使用链接度量值组，[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 实例的 Windows 服务帐户必须属于在源 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 实例上对源多维数据集和度量值组具有 `ReadDefinition` 和 `Read` 访问权的 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 数据库角色，或必须属于源 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 实例的 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] Administrators 角色。  
  
## <a name="see-also"></a>请参阅  
 [定义链接维度](define-linked-dimensions.md)  
  
  
