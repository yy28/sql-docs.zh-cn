---
title: "启用 DirectQuery 模式下在 SSDT |Microsoft 文档"
ms.custom: 
ms.date: 07/06/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: tabular-models
ms.reviewer: 
ms.suite: sql
ms.technology:
- analysis-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 71fc7ebd-2e86-4a76-994b-66d3a57bcc9b
caps.latest.revision: 16
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 9f3a5cfe3f2b39f35d2b2e70dd44ec11adeebcd0
ms.contentlocale: zh-cn
ms.lasthandoff: 09/01/2017

---
# <a name="enable-directquery-mode-in-ssdt"></a>在 SSDT 中启用 DirectQuery 模式

[!INCLUDE[ssas-appliesto-sqlas-all-aas](../../includes/ssas-appliesto-sqlas-all-aas.md)]

本主题介绍如何在 [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]中为表格模型项目启用 DirectQuery 模式。  
  
为你在 SSDT 中设计的表格模型启用 DirectQuery 模式时：
-   禁用与 DirectQuery 模式不兼容的功能。  
-   验证现有模型。 针对与 DirectQuery 模式不兼容的功能显示警告。  
-   如果已在启用 DirectQuery 模式之前导入数据，则工作模式的缓存已清空。  
  
### <a name="enable-directquery"></a>启用 DirectQuery  
  
在 SSDT 中，在 **Model.bim** 文件的“属性”窗格中，将属性“DirectQuery Mode”更改为“On”。  

![在 SSDT 中启用 DirectQuery 模式](../../analysis-services/tabular-models/media/enable-directquery-mode-in-ssdt.png)
  
如果模型已连接到数据源和现有数据，则系统将提示你输入用于连接到关系数据库的数据库凭据。 将从内存中缓存删除模型中已存在的任何数据。  
  
如果在启用 DirectQuery 模式前已部分或全部完成模型，则可能会受到有关功能不兼容的错误。 在 Visual Studio 中，打开  “错误列表”，并且解决将阻止模型切换到 DirectQuery 模式的任何问题。  


### <a name="whats-next"></a>下一步是什么？ 
现在可以通过“表导入向导”来导入数据，为模型获取元数据。 获得的不是数据行，而是要用作模型基础的表、列和关系。 

可以为每个表创建示例分区，并添加示例数据，以便在生成模型时验证模型行为。 你添加的任何示例数据将会用在 **Analyze for Excel** 或其他可以连接到工作区数据库的客户端工具中。 有关详细信息，请参阅 [在设计模式下将示例数据添加到 DirectQuery 模型中](../../analysis-services/tabular-models/add-sample-data-to-a-directquery-model-in-design-mode.md) 。  
  
> [!TIP]  
    >  即使在空模型的 DirectQuery 模式下，也始终都能查看每个表的小型内置行集。 在 [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)] 中，请单击“表” > “表属性”来查看 50 行的数据集。  
  
  
## <a name="see-also"></a>另请参阅  
[在 SSMS 中启用 DirectQuery 模式](../../analysis-services/tabular-models/enable-directquery-mode-in-ssms.md)

[在设计模式下将示例数据添加到 DirectQuery 模型中](../../analysis-services/tabular-models/add-sample-data-to-a-directquery-model-in-design-mode.md)
  

