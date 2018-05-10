---
title: 在数据源视图 (Analysis Services) 中定义逻辑主键 |Microsoft 文档
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: multidimensional-models
ms.topic: article
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: df3eaaed83e4ec4c6aab8433879fb48456946d68
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="define-logical-primary-keys-in-a-data-source-view-analysis-services"></a>在数据源视图中定义逻辑主键 (Analysis Services)
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  数据源视图向导和数据源视图设计器自动根据基础数据库表为添加到数据源视图的表定义主键。  
  
 有时，您可能需要在数据源视图中手动定义主键。 例如，出于性能或设计方面的原因，数据源中的表可能没有显式定义的主键列。 命名查询和视图也可能遗漏表的主键列。 如果表、视图或命名查询未定义物理主键，则可以在数据源视图设计器中为表、视图或命名查询手动定义一个逻辑主键。  
  
## <a name="set-a-logical-primary-key"></a>设置逻辑主键  
 在 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 中，需要使用主键来唯一标识表中的记录，标识维度表中的键列，以及支持表、视图和命名查询之间的关系。 使用这些关系，可以构造用于从基础数据源中检索数据和元数据的查询，还可以利用高级商业智能功能。  
  
 任何列都可用于逻辑主键（包括命名计算）。 创建逻辑主键时，将在数据源视图中创建一个唯一约束并将其标记为主键约束。 在所选表中指定的任何其他现有逻辑主键都将被删除。  
  
1.  在 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]中，打开项目或连接到数据库，此项目或数据库包含要在其中设置逻辑主键的数据源视图。  
  
2.  在解决方案资源管理器中，展开“数据源视图”文件夹，然后双击数据源视图。  
  
     若要查找表或视图，可以通过单击“数据源视图”菜单或者右键单击“表”或“关系图”窗格的空白区域以使用“查找表”选项。  
  
3.  在“表”或“关系图”窗格中，右键单击要用于定义逻辑主键的一列或多列，再单击“设置逻辑主键”。  
  
     设置逻辑主键的选项仅可用于没有主键的表。  
  
     请注意，在设置该键后，键图标现在标识主键列。  
  
## <a name="see-also"></a>另请参阅  
 [多维模型中的数据源视图](../../analysis-services/multidimensional-models/data-source-views-in-multidimensional-models.md)   
 [在数据源视图 & #40; 中定义命名的计算Analysis Services & #41;](../../analysis-services/multidimensional-models/define-named-calculations-in-a-data-source-view-analysis-services.md)  
  
  
