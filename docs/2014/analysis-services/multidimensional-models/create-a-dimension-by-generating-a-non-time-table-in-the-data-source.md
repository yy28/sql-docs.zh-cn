---
title: 通过在数据源中生成非时间表来创建维度 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- data sources [Analysis Services], dimensions without data source
- dimensions [Analysis Services], standard
- dimensions [Analysis Services], creating without data source
- standard dimensions [Analysis Services]
ms.assetid: a37f7a46-7451-4582-ba19-2595196d97bc
caps.latest.revision: 40
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 45ba4a55fae371792ecffdc79cde7e8b9b51ed23
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2018
ms.locfileid: "37210097"
---
# <a name="create-a-dimension-by-generating-a-non-time-table-in-the-data-source"></a>通过在数据源中生成非时间表来创建维度
  在 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]中，可以借助 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 中的维度向导在不使用现有数据源的情况下创建维度。 在维度向导的“选择创建方法”页上选择“在数据源中生成非时间表”选项可执行此操作。 若要在基础数据源中创建新维度，必须具有在基础数据源中创建对象的权限。 在不使用预定义数据源视图的情况下定义维度时，可以从头开始定义维度，也可以使用维度模板来定义维度。  
  
 维度向导提供了示例维度模板，您可以使用这些模板生成常用的维度类型。 可以从下列维度类型中选择：  
  
-   帐户  
  
-   Customer  
  
-   date  
  
-   部门  
  
-   目标货币  
  
-   Employee  
  
-   Geography  
  
-   Internet 销售订单详细信息  
  
-   Organization  
  
-   Product  
  
-   Promotion  
  
-   分销商销售订单详细信息  
  
-   Reseller  
  
-   销售渠道  
  
-   销售原因  
  
-   销售汇总订单详细信息  
  
-   销售区域  
  
-   应用场景  
  
-   源货币  
  
 每个标准模板都支持可选择包括在维度中的属性。 还可以为经常与数据一起使用的维度添加自己的模板文件。 维度模板位于以下文件夹中：  
  
 `C:\Program Files\Microsoft SQL Server\100\Tools\Templates\olap\1033\Dimension Templates`  
  
 完成维度向导后，可以使用维度设计器来添加、删除和配置维度中的属性和层次结构。  
  
 不使用数据源创建非时间维度时，维度向导将引导您完成指定维度类型、标识键属性和渐变维度的步骤。  
  
## <a name="specify-dimension-type"></a>指定维度类型  
 在维度向导的 **“指定维度类型”** 页上，可以指定维度类型。 如果基于模板生成维度，则维度类型已定义。 在此页上，还可以为指定的维度类型选择标准属性（如果有的话）。  
  
 如果选择对应于维度类型的模板，则以该维度类型的选项填充此页。 如果不选择模板，或没有相应的维度类型，则默认维度类型是 **“常规”**。 如果尚未选择维度类型，请为要创建的维度选择最合适的类型。 如果没有为 **“维度类型”** 列出合适的类型，请使用 **“常规”**。  
  
 选择维度类型时，向导将在 **“维度属性”** 下列出适用于此维度的属性类型。 若要选择属性类型，请选中属性类型旁边的 **“包含”** 复选框，并在 **“维度属性”** 下面键入属性的名称。 默认名称与 **“属性类型”** 相同。  
  
## <a name="identify-key-attribute-and-changing-dimensions"></a>标识键属性和变化的维度  
 在 **“指定维度键和类型”** 页上，选择要作为维度键属性的属性。 键属性通常对应于主维度表中的主键列，它通常要为维度的叶成员建立索引。  
  
 如果选择了模板，并且在模板中定义了键属性，则该属性将成为默认键属性。 如果选择了模板，但没有在该模板中定义键属性，则默认属性是列表中的第一个属性。 该列表包含在 **“指定维度类型”** 页中选择的所有属性。 可以选择在 **“指定维度类型”** 页中选择的任何一个属性作为键属性。 如果不选择任何属性，向导将自动创建键属性，并以串联的维度名称和“ID”进行命名。  
  
 最后，请指定此维度是否是变化的维度。 在变化的维度中，成员将会随时间的变化移至层次结构中的不同位置。 向导将生成其他列，并创建与这些列相对应的属性。 这些列将允许用户以变化中的因素的方式查询维度。 随后用架构生成向导所创建的任何包将基于维度的渐变维度特征来管理代理键。  
  
 选中 **“这是变化的维度”** 复选框时，维度向导将定义下表中列出的属性：  
  
|Attribute|类型|  
|---------------|----------|  
|SCD OriginalID|SCDOriginalID|  
|SCD End Date|SCDEndDate|  
|SCD Start Date|SCDStartDate|  
|SCD 状态|SCDStatus|  
  
 如果使用已定义这些渐变维度属性的模板，则默认情况下已选中 **“这是变化的维度”** 复选框。 如果清除了该复选框，将从维度中删除渐变维度属性。  
  
 可以使用维度设计器配置渐变维度的属性。  
  
## <a name="completing-the-dimension-wizard"></a>完成维度向导  
 在 **“完成向导”** 页中，键入新维度的名称并查看维度结构。 选中 **“立即生成架构”** 复选框，以在单击 **“完成”** 之后启动架构生成向导。 在大多数情况下，如果计划创建其他对象，则不应选中该复选框。 如果不选中此复选框，则可以随后使用维度设计器生成架构。  
  
## <a name="see-also"></a>请参阅  
 [通过生成时间表来创建时间维度](create-a-time-dimension-by-generating-a-time-table.md)   
 [通过生成时间表来创建时间维度](create-a-time-dimension-by-generating-a-time-table.md)  
  
  
