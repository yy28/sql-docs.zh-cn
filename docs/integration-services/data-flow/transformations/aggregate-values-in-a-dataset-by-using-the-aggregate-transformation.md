---
title: "使用聚合转换来聚合数据集中的值 | Microsoft Docs"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: data-flow
ms.reviewer: 
ms.suite: sql
ms.technology: integration-services
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- Aggregate transformation [Integration Services]
- aggregate values [Integration Services]
- datasets [Integration Services], aggregate values
ms.assetid: 01b81c0f-d5e0-483b-81b2-73800a6945ac
caps.latest.revision: "48"
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: f07d092a7b0a583281070fb79063d1432ff81421
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/20/2017
---
# <a name="aggregate-values-in-a-dataset-by-using-the-aggregate-transformation"></a>使用聚合转换来聚合数据集中的值
  若要添加并配置聚合转换，则包必须已包含至少一个数据流任务和一个源。  
  
### <a name="to-aggregate-values-in-a-dataset"></a>聚合数据集中的值  
  
1.  在 [!INCLUDE[ssBIDevStudioFull](../../../includes/ssbidevstudiofull-md.md)]中，打开包含所需包的 [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] 项目。  
  
2.  在解决方案资源管理器中，双击该包将其打开。  
  
3.  单击 **“数据流”** 选项卡，然后从 **“工具箱”**中将聚合转换拖动到设计图面。  
  
4.  将连接线从源或前一转换拖到聚合转换，从而将聚合转换连接到数据流。  
  
5.  双击此转换。  
  
6.  在 **“聚合转换编辑器”** 对话框中单击 **“聚合”** 选项卡。  
  
7.  在 **“可用输入列”** 列表中，选中要对其值进行聚合运算的列旁边的复选框。 所选的列出现在表中。  
  
    > [!NOTE]  
    >  可以多次选择同一列，这样便可对此列应用多次转换。 若要唯一标识聚合，请在列输出别名的默认名称后面追加一个数字。  
  
8.  或者，修改 **“输出别名”** 列中的值。  
  
9. 若要更改默认聚合操作 **“分组依据”**，请选择 **“操作”** 列表中的其他操作。  
  
10. 若要更改默认比较，请选择 **“比较标志”** 列中所列出的单个比较标志。 默认情况下，比较将忽略大小写、假名类型、不占位字符和字符宽度。  
  
11. 对于 **“非重复计数”** 聚合，如果需要，可在 **“非重复键计数”** 列中指定非重复值的精确计数，或者在 **“非重复键数范围”** 列中选择近似的数字。  
  
    > [!NOTE]  
    >  由于转换可以为它的工作预先分配合适的内存数量，因此可通过提供不同值的个数（准确或近似）来优化性能。  
  
12. 或者，单击 **“高级”** 并更新聚合转换输出的名称。 如果聚合包含 **Group By** 操作，则可以在 **“键范围”** 列中选择分组键值的近似计数，或者在 **“键”** 列中指定分组键值的准确数目。  
  
    > [!NOTE]  
    >  由于转换可以为它的工作预先分配合适的内存数量，因此可通过提供不同值的个数（准确或近似）来优化性能。  
  
    > [!NOTE]  
    >  **“键范围”** 和 **“键”** 选项互斥。 如果在两个列中都输入值，将使用 **“键范围”** 或 **“键”** 二者中的更大值。  
  
13. 或者，单击 **“高级”** 选项卡并设置应用于优化聚合转换所执行的所有操作的属性。  
  
14. 单击 **“确定”**。  
  
15. 若要保存更新后的包，请单击 **“文件”** 菜单上的 **“保存选定项”** 。  
  
## <a name="see-also"></a>另请参阅  
 [聚合转换](../../../integration-services/data-flow/transformations/aggregate-transformation.md)   
 [Integration Services 转换](../../../integration-services/data-flow/transformations/integration-services-transformations.md)   
 [Integration Services 路径](../../../integration-services/data-flow/integration-services-paths.md)   
 [数据流任务](../../../integration-services/control-flow/data-flow-task.md)  
  
  
