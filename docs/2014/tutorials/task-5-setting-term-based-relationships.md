---
title: 任务5：设置基于字词的关系 |Microsoft Docs
ms.custom: ''
ms.date: 04/27/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
ms.assetid: 6569d512-637d-4f7b-82e1-1e8582278b37
author: lrtoyou1223
ms.author: lle
manager: craigg
ms.openlocfilehash: 0e9a6a1a96d208077e70c0cf1835cff6e34650dd
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "65489110"
---
# <a name="task-5-setting-term-based-relationships"></a>任务 5：设置基于字词的关系
  在此任务中，将为**供应商名称**域的值定义一些基于字词的关系。 通过基于字词的关系，您可以对属于域中某个值的字词进行更正。 基于字词的关系使完全相同的多个值（只有其公共部分的拼写除外）可被视为相同的同义词。 例如， **inc.** 可以更正为 "**合并**"。 DQS 在知识发现、清理或匹配过程中使用这些关系。 有关更多详细信息，请参阅[创建基于字词的关系](https://msdn.microsoft.com/library/hh510404.aspx)。  
  
1.  选择 "**域列表**" 中的 "**供应商名称**"。  
  
2.  切换到右窗格中的 "**基于字词的关系**" 选项卡。  
  
3.  单击工具栏上的 "**添加新关系**" 按钮，以向表中添加关系。  
  
4.  键入 **"Co** " 作为 "**正确**的" 字段的 "**值**" 字段和 "**公司**"。  
  
5.  对以下值重复前两个步骤：  
  
    |值|更正为|  
    |-----------|----------------|  
    |Corp.|Corporation|  
    |Inc.|Incorporated|  
  
     ![基于字词的关系](../../2014/tutorials/media/et-settingtermbasedrelations.jpg "基于字词的关系")  
  
## <a name="next-step"></a>下一步  
 [任务 6：设置同义词](../../2014/tutorials/task-6-setting-synonyms.md)  
  
  
