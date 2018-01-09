---
title: "在数据源视图 (Analysis Services) 中定义逻辑主键 |Microsoft 文档"
ms.custom: 
ms.date: 03/01/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: data-mining
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- removing logical primary keys
- logical primary keys [SQL Server]
- deleting logical primary keys
- data source views [Analysis Services], logical primary keys
ms.assetid: 172bc267-c637-4caa-bf55-0ba198d30b1e
caps.latest.revision: "36"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: ab3e26fdddc257e2ddf8edd450c412bbabb7c557
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/08/2018
---
# <a name="define-logical-primary-keys-in-a-data-source-view-analysis-services"></a>在数据源视图中定义逻辑主键 (Analysis Services)
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]数据源视图向导和数据源视图设计器自动定义的表添加到数据源视图基于基础数据库表的主键。  
  
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
 [在数据源视图中定义命名计算 (Analysis Services)](../../analysis-services/multidimensional-models/define-named-calculations-in-a-data-source-view-analysis-services.md)  
  
  
