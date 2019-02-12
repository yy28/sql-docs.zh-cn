---
title: 任务 5：设置基于字词的关系 |Microsoft Docs
ms.custom: ''
ms.date: 04/27/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
ms.assetid: 6569d512-637d-4f7b-82e1-1e8582278b37
author: leolimsft
ms.author: lle
manager: craigg
ms.openlocfilehash: 322c5a5afcd7c5d82982a86cb9398e66bb248c5d
ms.sourcegitcommit: dfb1e6deaa4919a0f4e654af57252cfb09613dd5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/11/2019
ms.locfileid: "56034448"
---
# <a name="task-5-setting-term-based-relationships"></a>任务 5：设置基于字词的关系
  在本任务中，定义为值的几个基于字词的关系**Supplier Name**域。 基于字词的关系，可对域中值的一部分的字词进行更正。 基于字词的关系使完全相同的多个值（只有其公共部分的拼写除外）可被视为相同的同义词。 例如， **Inc.** 可以更正为**Incorporated**。 DQS 在知识发现、清理或匹配过程中使用这些关系。 请参阅[创建基于字词的关系](https://msdn.microsoft.com/library/hh510404.aspx)的更多详细信息。  
  
1.  选择**Supplier Name**中**域列表**。  
  
2.  切换到**基于字词的关系**右窗格中的选项卡。  
  
3.  单击**添加新关系**按钮在工具栏上，若要添加到表的关系。  
  
4.  类型**Co.** 有关**值**字段并**公司**有关**更正为**字段。  
  
5.  对以下值重复前两个步骤：  
  
    |ReplTest1|更正为|  
    |-----------|----------------|  
    |Corp.|Corporation|  
    |Inc.|Incorporated|  
  
     ![基于字词的关系](../../2014/tutorials/media/et-settingtermbasedrelations.jpg "基于字词的关系")  
  
## <a name="next-step"></a>下一步  
 [任务 6:设置同义词](../../2014/tutorials/task-6-setting-synonyms.md)  
  
  
