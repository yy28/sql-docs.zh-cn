---
title: 任务 4： 将结果导出从匹配活动到 Excel 文件 |Microsoft 文档
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- data-quality-services
- integration-services
- master-data-services
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 644454c4-3c5a-469a-90ec-e51dc7fb99fc
caps.latest.revision: 6
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.openlocfilehash: 440e8c0db00d5087334746f4094c61de52bf1bc5
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36016013"
---
# <a name="task-4-exporting-the-results-from-matching-activity-to-an-excel-file"></a>任务 4：将匹配活动的结果导出到 Excel 文件
  在本任务中，您将匹配活动的结果导出到 Excel 文件。  
  
1.  在**导出**页上，选择**Excel 文件**为**目标类型**。  
  
2.  选择**存活结果**选项。 在存活过程中，DQS 确定基于每个群集的存活记录**存活规则**所选。  
  
3.  单击**浏览**和导航到要用于存储输出文件的文件夹。  
  
4.  类型**Cleansed 和匹配 Suppliers.xls**的名称，然后单击**打开**。  
  
5.  确认**透视记录**为选择**存活规则**。 当您选择此选项时，为分类的输出选择每个分类的透视记录。 存留规则的其他选项有：  
  
    1.  **最完整记录：** 存活记录是一个具有最大填充字段数。  
  
    2.  **最长记录：** 存活记录是与源字段中的词的最大数目。  
  
    3.  **最完整且最长的记录：** 存活记录都是一个具有最大填充字段数并且在每个字段中具有的词的最大数目。  
  
     ![将结果导出从匹配页](../../2014/tutorials/media/et-exportingtheresultsfrommatoanexcelfile.jpg "从匹配页中导出结果")  
  
6.  单击**导出**将结果导出到 Excel 文件。  
  
7.  单击**关闭**关闭**匹配导出**对话框。  
  
8.  单击**完成**完成匹配活动。  
  
9. 打开**Cleansed 和匹配 Suppliers.xlsx**文件并确认你未看到任何重复项 (供应商 Id)。  
  
 现在，您的供应商数据已经过清理和匹配，删除了重复项。  
  
## <a name="next-step"></a>下一步  
 [第 4 课：在 MDS 中存储供应商数据](../../2014/tutorials/lesson-4-storing-supplier-data-in-mds.md)  
  
  