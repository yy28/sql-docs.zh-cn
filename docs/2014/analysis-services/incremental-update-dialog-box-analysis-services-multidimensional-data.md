---
title: 增量更新对话框 (Analysis Services-多维数据) |Microsoft 文档
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- sql12.asvs.process.incrementalupdate.f1
ms.assetid: d5a5ae27-44e7-4179-b9e2-efbf21d6c5f5
caps.latest.revision: 19
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: 51fb9898eb2d43fd56cbefb6f08120669dcd6f0c
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36123511"
---
# <a name="incremental-update-dialog-box-analysis-services---multidimensional-data"></a>“增量更新”对话框（Analysis Services - 多维数据）
  可以使用 **和** 中的 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] “增量更新” [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] 对话框，定义在增量更新度量值组和分区时使用的设置。 通过在 **“处理”** 对话框的 **“对象列表”** 网格的 **“设置”** 列中单击 **“配置”** ，可以显示 **“增量更新”** 对话框。  
  
## <a name="options"></a>“常规”  
  
|术语|定义|  
|----------|----------------|  
|**度量值组**|选择要增量更新的度量值组。<br /><br /> 注意：只有在增量更新多维数据集时，才会启用此选项。 如果是增量更新度量值组或分区，则将禁用此选项。|  
|分区|选择要更新的分区。<br /><br /> 注意：只有在增量更新多维数据集时，才会启用此选项。 如果是增量更新度量值组或分区，则将禁用此选项。|  
|**表**|单击此项可以更新表中的对象。|  
|**数据源或视图**|选择源表所在的数据源或数据源视图。<br /><br /> 注意：只有在选择了“表”  时，才会启用此选项。|  
|**表架构和名称**|选择用于检索数据以增量更新多维数据集、度量值组或分区的源表。<br /><br /> 注意：只有在选择了“表”  时，才会启用此选项。|  
|**“数据集属性”**|单击此项可以更新查询中的对象。|  
|**数据源**|选择要查询的表所在的数据源。<br /><br /> 注意：只有在选择了“查询”  时，才会启用此选项。|  
|**查询文本**|键入用于检索数据以增量更新多维数据集、度量值组或分区的查询文本。<br /><br /> 注意：只有在选择了“查询”  时，才会启用此选项。|  
  
## <a name="see-also"></a>请参阅  
 [Analysis Services 设计器和对话框&#40;多维数据&#41;](analysis-services-designers-and-dialog-boxes-multidimensional-data.md)   
 [处理对话框&#40;Analysis Services-多维数据&#41;](process-dialog-box-analysis-services-multidimensional-data.md)  
  
  