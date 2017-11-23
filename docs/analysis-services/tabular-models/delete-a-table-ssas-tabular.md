---
title: "删除表 (SSAS 表格) |Microsoft 文档"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: tabular-models
ms.reviewer: 
ms.suite: sql
ms.technology:
- analysis-services
- analysis-services/multidimensional-tabular
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: be4ed45f-fde3-466c-9869-49bd3ddb505e
caps.latest.revision: "9"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: be456ceeef0d8d965c9e922bffbcec0507cb3777
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/17/2017
---
# <a name="delete-a-table-ssas-tabular"></a>删除表（SSAS 表格）
  在模型设计器中，您可以删除不再需要的模型工作区数据库中的表。 删除表并不影响原始源数据，只会影响你已导入并且正在使用的数据。 您无法撤消对表的删除。  
  
### <a name="to-delete-a-table"></a>删除表  
  
-   对于想要删除的表，右键单击模型设计器底部的选项卡，然后单击“删除”。  
  
## <a name="considerations-when-deleting-tables"></a>删除表时的注意事项  
  
-   在您删除一个表时，该表位于其上的整个选项卡都将被删除。  
  
-   如果任何度量值与该表相关联，则也将删除该度量值的定义。  
  
-   如果您使用该表创建了任何计算列，则也删除该表中的列；其他表中使用已删除表中的列的任何计算列将显示一个错误。  
  
## <a name="see-also"></a>另请参阅  
 [表和列（SSAS 表格）](../../analysis-services/tabular-models/tables-and-columns-ssas-tabular.md)  
  
  
