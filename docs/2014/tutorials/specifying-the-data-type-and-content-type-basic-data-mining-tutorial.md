---
title: 指定数据类型和内容类型（数据挖掘基础教程） |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: 72484d27-3ef1-4f16-813c-2f43231fc2da
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 583a6fda2dbb4698405a3d69f33955531b3c1c10
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "62720055"
---
# <a name="specifying-the-data-type-and-content-type-basic-data-mining-tutorial"></a>指定数据类型和内容类型（数据挖掘基础教程）
  您已选择了用于生成结构和为模型定型的列，现在可以对向导设置的默认数据类型和内容类型进行任何必要的更改。  
  
#### <a name="review-and-modify-content-type-and-data-type-for-each-column"></a>检查和修改每列的内容类型和数据类型  
  
1.  在 "**指定列的内容和数据类型"** 页上，单击 "**检测**" 运行确定每个列的默认数据和内容类型的算法。  
  
2.  查看 "**内容类型**" 和 "**数据类型**" 列中的条目，并根据需要对其进行更改，以确保设置与下表中列出的设置相同。  
  
     通常，向导会检测数值，并分配相应的数值数据类型；但有些情况下，您可能想要将数值作为文本处理。 例如， **GeographyKey**应作为文本处理，因为它不适合对此标识符执行数学运算。  
  
    |列|内容类型|数据类型|  
    |------------|------------------|---------------|  
    |**地址 Line1**|**离散**|**文本**|  
    |**地址第二行**|**离散**|**文本**|  
    |**年**|**持续**|**Long**|  
    |**Bike Buyer**|**离散**|**Long**|  
    |**上下班路程**|**离散**|**文本**|  
    |**CustomerKey**|**Key**|**Long**|  
    |**DateLastPurchase**|**持续**|**Date**|  
    |**电子邮件地址**|**离散**|**文本**|  
    |**English Education**|**离散**|**文本**|  
    |**English Occupation**|**离散**|**文本**|  
    |**FirstName**|**离散**|**文本**|  
    |**性别**|**离散**|**文本**|  
    |**Geography Key**|**离散**|**文本**|  
    |**House Owner Flag**|**离散**|**文本**|  
    |**姓氏**|**离散**|**文本**|  
    |**婚姻状况**|**离散**|**文本**|  
    |**Number Cars Owned**|**离散**|**Long**|  
    |**Number Children At Home**|**离散**|**Long**|  
    |**区域**|**离散**|**文本**|  
    |**Total Children**|**离散**|**Long**|  
    |**Yearly Income**|**持续**|**仔细**|  
  
3.  单击“下一步”。   
  
## <a name="next-task-in-lesson"></a>课程中的下一个任务  
 [为结构指定测试数据集 &#40;数据挖掘基础教程&#41;](../../2014/tutorials/specifying-a-testing-data-set-for-the-structure-basic-data-mining-tutorial.md)  
  
## <a name="previous-task-in-lesson"></a>课程中的前一个任务  
 [创建目标邮件挖掘模型结构 &#40;基本数据挖掘教程&#41;](../../2014/tutorials/creating-a-targeted-mailing-mining-model-structure-basic-data-mining-tutorial.md)  
  
## <a name="see-also"></a>另请参阅  
 [内容类型 &#40;数据挖掘&#41;](../../2014/analysis-services/data-mining/content-types-data-mining.md)   
 [数据挖掘 &#40;的数据类型&#41;](../../2014/analysis-services/data-mining/data-types-data-mining.md)  
  
  
