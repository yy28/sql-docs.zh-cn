---
title: 指定数据类型和内容类型 （数据挖掘基础教程） |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
ms.assetid: 72484d27-3ef1-4f16-813c-2f43231fc2da
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: b97cec782c7f95de42ee64d7db0ce56ffa916c3e
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2018
ms.locfileid: "48176599"
---
# <a name="specifying-the-data-type-and-content-type-basic-data-mining-tutorial"></a>指定数据类型和内容类型（数据挖掘基础教程）
  您已选择了用于生成结构和为模型定型的列，现在可以对向导设置的默认数据类型和内容类型进行任何必要的更改。  
  
#### <a name="review-and-modify-content-type-and-data-type-for-each-column"></a>检查和修改每列的内容类型和数据类型  
  
1.  上**指定列内容和数据类型**页上，单击**检测**运行确定默认数据和每个列的内容类型的算法。  
  
2.  查看中的条目**内容类型**并**数据类型**列和更改; 如有必要，以确保设置将与下表中列出的内容相同。  
  
     通常，向导会检测数值，并分配相应的数值数据类型；但有些情况下，您可能想要将数值作为文本处理。 例如， **GeographyKey**应处理为文本，因为不适当，若要对此标识符执行数学运算。  
  
    |“列”|内容类型|数据类型|  
    |------------|------------------|---------------|  
    |**地址行 1**|**离散**|**Text**|  
    |**地址行 2**|**离散**|**Text**|  
    |**年龄**|**连续**|**Long**|  
    |**自行车购买者**|**离散**|**Long**|  
    |**上下班路程**|**离散**|**Text**|  
    |**CustomerKey**|**Key**|**Long**|  
    |**DateLastPurchase**|**连续**|**Date**|  
    |**Email Address**|**离散**|**Text**|  
    |**英语教育**|**离散**|**Text**|  
    |**英语职业**|**离散**|**Text**|  
    |**FirstName**|**离散**|**Text**|  
    |**性别**|**离散**|**Text**|  
    |**地域关键字**|**离散**|**Text**|  
    |**House Owner Flag**|**离散**|**Text**|  
    |**Last Name**|**离散**|**Text**|  
    |**婚姻状况**|**离散**|**Text**|  
    |**Number Cars Owned**|**离散**|**Long**|  
    |**Number Children At Home**|**离散**|**Long**|  
    |**地区**|**离散**|**Text**|  
    |**Total Children**|**离散**|**Long**|  
    |**Yearly Income**|**连续**|**双精度**|  
  
3.  单击“下一步” 。  
  
## <a name="next-task-in-lesson"></a>课程中的下一个任务  
 [为结构指定测试数据集&#40;数据挖掘基础教程&#41;](../../2014/tutorials/specifying-a-testing-data-set-for-the-structure-basic-data-mining-tutorial.md)  
  
## <a name="previous-task-in-lesson"></a>课程中的前一个任务  
 [创建目标的邮件挖掘模型结构&#40;数据挖掘基础教程&#41;](../../2014/tutorials/creating-a-targeted-mailing-mining-model-structure-basic-data-mining-tutorial.md)  
  
## <a name="see-also"></a>请参阅  
 [内容类型&#40;数据挖掘&#41;](../../2014/analysis-services/data-mining/content-types-data-mining.md)   
 [数据类型&#40;数据挖掘&#41;](../../2014/analysis-services/data-mining/data-types-data-mining.md)  
  
  
