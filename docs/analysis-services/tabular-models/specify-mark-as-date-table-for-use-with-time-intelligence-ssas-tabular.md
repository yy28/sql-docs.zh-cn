---
title: 指定标记为日期表 |Microsoft 文档
ms.date: 05/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: tabular-models
ms.topic: article
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 4c717a5a260fc5f222f3a41cc437de1ccc945e03
ms.sourcegitcommit: 1aedef909f91dc88dc741748f36eabce3a04b2b1
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/08/2018
---
# <a name="specify-mark-as-date-table-for-use-with-time-intelligence"></a>指定标记为日期表用于时间智能
[!INCLUDE[ssas-appliesto-sqlas-aas](../../includes/ssas-appliesto-sqlas-aas.md)]
  为了在 DAX 公式中使用时间智能函数，必须指定日期表和日期数据类型的唯一标识符 (datetime) 列。 将日期表中的某列指定为唯一标识符后，您可以在日期表中各列与任何事实数据表之间创建关系。  
  
 使用时间智能函数时，以下规则适用：  
  
-   使用 DAX 时间智能函数时，永远不会指定从事实数据表的 datetime 列。 在您的模型中，始终使用至少一个数据类型为 Date 的 datetime 列和唯一值来创建单独的日期表。  
  
-   请确保您的日期表具有一个连续的日期范围。  
  
-   日期表中的 datetime 列应该以天为粒度（不应包含不足一天）。  
  
-   必须使用 **“标记日期表”** 对话框指定一个日期表和一个唯一标识符列。  
  
-   在事实数据表与日期表中数据类型为 Date 的列之间创建关系。  
  
#### <a name="to-specify-a-date-table-and-unique-identifier"></a>指定日期表和唯一标识符  
  
1.  在模型设计器中，单击日期表。  
  
2.  单击 **“表”** 菜单，然后依次单击 **“日期”**和 **Mark as “日期” “表”**。  
  
3.  在 **“标记日期表”** 对话框的 **“日期”** 列表框中，选择要用作唯一标识符的列。 此列必须包含唯一值，并且数据类型应为 Date。 例如：  
  
    |日期|  
    |----------|  
    |7/1/2010 12:00:00 AM|  
    |7/2/2010 12:00:00 AM|  
    |7/3/2010 12:00:00 AM|  
    |7/4/2010 12:00:00 AM|  
    |7/5/2010 12:00:00 AM|  
  
4.  根据需要在事实数据表和日期表之间创建任何关系。  
  
## <a name="see-also"></a>另请参阅  
 [计算](../../analysis-services/tabular-models/calculations-ssas-tabular.md)   
 [时间智能函数 (DAX)](http://msdn.microsoft.com/en-us/91df278d-4b28-40c1-a572-cdb91f081517)  
  
  
