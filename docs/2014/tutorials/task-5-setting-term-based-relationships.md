---
title: 任务 5： 设置术语基于关系 |Microsoft 文档
ms.custom: ''
ms.date: 04/27/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- data-quality-services
- integration-services
- master-data-services
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 6569d512-637d-4f7b-82e1-1e8582278b37
caps.latest.revision: 8
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.openlocfilehash: b8450d3e77de578810bb57c35aafad6f90c8f19c
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36013649"
---
# <a name="task-5-setting-term-based-relationships"></a>任务 5：设置基于字词的关系
  在此任务中，你可以定义有关值的几个基于字词的关系**供应商名称**域。 基于字词的关系使您能够对一个术语，它的一部分的域中值的更正。 基于字词的关系使完全相同的多个值（只有其公共部分的拼写除外）可被视为相同的同义词。 例如， **Inc.** 可以更正为**Incorporated**。 DQS 在知识发现、清理或匹配过程中使用这些关系。 请参阅[基于创建字词的关系](http://msdn.microsoft.com/library/hh510404.aspx)有关详细信息。  
  
1.  选择**供应商名称**中**域列表**。  
  
2.  切换到**基于字词的关系**右窗格中的选项卡。  
  
3.  单击**添加新关系**工具栏将关系添加到表上的按钮。  
  
4.  类型**Co.** 为**值**字段和**公司**为**更正为**字段。  
  
5.  对以下值重复前两个步骤：  
  
    |ReplTest1|更正为|  
    |-----------|----------------|  
    |Corp.|Corporation|  
    |Inc.|Incorporated|  
  
     ![基于字词的关系](../../2014/tutorials/media/et-settingtermbasedrelations.jpg "基于字词的关系")  
  
## <a name="next-step"></a>下一步  
 [任务 6：设置同义词](../../2014/tutorials/task-6-setting-synonyms.md)  
  
  