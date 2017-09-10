---
title: "使用维度向导创建维度 |Microsoft 文档"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- analysis-services/multidimensional-tabular
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- dimensions [Analysis Services], creating
ms.assetid: d84f66ae-7551-49bf-99d0-88368ca2dd0e
caps.latest.revision: 17
author: Minewiskan
ms.author: owend
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: ff4a16fdc7f18eae35de5023116a11179fb11c5b
ms.contentlocale: zh-cn
ms.lasthandoff: 09/01/2017

---
# <a name="create-a-dimension-using-the-dimension-wizard"></a>使用维度向导创建维度
  可以使用 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]中的维度向导创建新维度。  
  
### <a name="to-create-a-new-dimension"></a>创建新维度  
  
1.  在“解决方案资源管理器”中，右键单击“维度”，然后单击“新建维度”。  
  
2.  在维度向导的 **“选择创建方法”** 页上，选择 **“使用现有表”**，然后单击 **“下一步”**。  
  
    > [!NOTE]  
    >  有时可能必须在不使用现有表的情况下创建维度。 有关详细信息，请参阅 [通过在数据源中生成非时间表来创建维度](../../analysis-services/multidimensional-models/create-a-dimension-by-generating-a-non-time-table-in-the-data-source.md) 和 [通过生成时间表来创建时间维度](../../analysis-services/multidimensional-models/create-a-time-dimension-by-generating-a-time-table.md)。  
  
3.  在 **“指定源信息”** 页上，执行以下操作：  
  
    1.  在 **“数据源视图”** 列表中，选择数据源视图。  
  
    2.  在 **“主表”** 列表中，选择主维度表。  
  
    3.  在 **“键列”** 列表中，查看向导基于主维度表中定义的主键而自动选择的键列。 若要更改此默认设置，请指定将维度表链接到事实数据表的键列。  
  
    4.  在“名称列”下拉列表中，查看向导已自动选择的名称列。  
  
         当列包含说明性信息时，可以使用此默认名称。 但是，您可能希望指定包含对最终用户更有意义的值的名称。 例如，如果“产品”维度中的产品类别属性使用 **ProductCategoryKey** 列作为键列，则可以指定 **ProductCategoryName** 列作为名称列。  
  
         如果 **“键列”** 列表包含多个键列，则必须指定为键属性提供成员值的名称列。 为此，可在数据源视图中创建命名计算，然后使用该命名计算作为名称列。  
  
    5.  单击“下一步” 。  
  
4.  在 **“选择相关表”** 页上，选择要在维度中包含的相关表，然后单击 **“下一步”**。  
  
    > [!NOTE]  
    >  如果指定的主维度表与其他维度表有关系，则将显示“选择相关表”页。  
  
5.  在 **“选择维度属性”** 页上，选择要在维度中包含的属性，然后单击 **“下一步”**。  
  
     还可以更改属性名称，启用或禁用浏览以及指定属性类型。  
  
    > [!NOTE]  
    >  若要激活“启用浏览”和“属性类型”字段，必须选择要包含在维度中的属性。  
  
6.  在“定义帐户智能”页的“内置帐户类型”列中，选择帐户类型，然后单击“下一步”。  
  
     该帐户类型必须对应于 **“源表帐户类型”** 列中列出的源表帐户类型。  
  
    > [!NOTE]  
    >  如果在向导的“选择维度属性”页中定义了“帐户类型”维度属性，则将显示“定义帐户智能”页。  
  
7.  在 **“完成向导”** 页中，输入新维度的名称，并查看维度结构。 若要进行更改，请单击 **“上一步”**；否则，单击 **“完成”**。  
  
    > [!NOTE]  
    >  完成维度向导后，可以使用维度设计器来添加、删除和配置维度中的属性和层次结构。  
  
## <a name="see-also"></a>另请参阅  
 [使用现有表创建维度](../../analysis-services/multidimensional-models/create-a-dimension-by-using-an-existing-table.md)  
  
  
