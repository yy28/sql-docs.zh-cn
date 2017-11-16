---
title: "查看或更改建模标志 （数据挖掘） |Microsoft 文档"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: data-mining
ms.reviewer: 
ms.suite: sql
ms.technology:
- analysis-services
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: d1169735-fb18-417b-b8d6-9a161e444020
caps.latest.revision: 6
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: cbffc4a5312dc83976915653141247d27dc8eae4
ms.contentlocale: zh-cn
ms.lasthandoff: 09/01/2017

---
# <a name="view-or-change-modeling-flags-data-mining"></a>查看或更改建模标志（数据挖掘）
  建模标志是在挖掘结构列或挖掘模型列上设置的属性，用于控制分析期间算法处理数据的方式。  
  
 在数据挖掘设计器中，通过查看结构或模型的属性，可以查看和修改与挖掘结构或挖掘列关联的建模标志。 还可以通过使用 DMX、AMO 或 XMLA 设置建模标志。  
  
 此过程说明如何在设计器中更改建模标志。  
  
### <a name="view-or-change-the-modeling-flag-for-a-structure-column-or-model-column"></a>查看或更改结构列或模型列的建模标志  
  
1.  在 SQL Server Design Studio 中，打开解决方案资源管理器，然后双击挖掘结构。  
  
2.  若要设置 NOT NULL 建模标志，请单击 **“挖掘结构”** 选项卡。若要设置 REGRESSOR 或 MODEL_EXISTENCE_ONLY 标志，请单击“挖掘模型”选项卡。  
  
3.  右键单击要查看或更改的列，然后选择“属性”。  
  
4.  若要添加新的建模标志，请单击 **“建模标志”** 属性旁边的文本框，然后选择要使用的建模标志的复选框。  
  
     建模标志只有在它们适合列数据类型时才显示。  
  
    > [!NOTE]  
    >  更改某个建模标志后，您必须重新处理该模型。  
  
### <a name="get-the-modeling-flags-used-in-the-model"></a>获取模型中使用的建模标志  
  
-   在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]中，打开 DMX 查询窗口，然后键入类似以下内容的查询：  
  
    ```  
    SELECT COLUMN_NAME, CONTENT_TYPE, MODELING_FLAG  
    FROM $system.DMSCHEMA_MINING_COLUMNS  
    WHERE MODEL_NAME = 'Forecasting'  
  
    ```  
  
## <a name="see-also"></a>另请参阅  
 [挖掘模型任务和操作指南](../../analysis-services/data-mining/mining-model-tasks-and-how-tos.md)   
 [建模标志（数据挖掘）](../../analysis-services/data-mining/modeling-flags-data-mining.md)  
  
  

