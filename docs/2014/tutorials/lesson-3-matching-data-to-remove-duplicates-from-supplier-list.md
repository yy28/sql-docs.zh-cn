---
title: 第 3 课： 删除的数据相匹配的复制从供应商列表 |Microsoft 文档
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
ms.assetid: 059170b6-d62e-4b28-9451-99a0cc7e1f5f
caps.latest.revision: 6
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.openlocfilehash: c7d31df6b1d803eb606e68a934b72386f9d7950e
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36129803"
---
# <a name="lesson-3-matching-data-to-remove-duplicates-from-supplier-list"></a>第 3 课：匹配数据以便从供应商列表中删除重复项
  您可以通过在知识库中创建匹配策略，为执行匹配活动准备知识库。 一个知识库中只能有一个匹配策略。 一个匹配策略包含一个或多个匹配规则。 规则识别匹配过程中涉及的域，并指定每个域值在匹配判断中的权重。 您可以在规则中指定域值必须是精确匹配还是相似匹配以及相似度。 还指定域匹配是否为匹配过程的先决条件。 您可以针对示例数据单独测试每个规则以及测试整个策略。 测试过程中显示其匹配分数大于记录**最低记录分数**群集 （组） 中的 DQS 配置中指定的阈值。 您可以继续更改策略中的规则，直到满意为止。  
  
 定义策略后，您创建一个数据质量项目来运行匹配活动。 匹配项目将匹配策略中的匹配规则应用到要进行评估的数据源。 这一过程评估任何两行是匹配项的可能性。 当 DQS 执行匹配分析时，它会创建 DQS 认为是匹配的分类。 DQS 随机将其中的一条记录确定为透视记录。 您可以验证和拒绝任何对该分类而言不是适当匹配的记录。 请参阅[Create a Matching Policy](http://msdn.microsoft.com/library/hh270290.aspx)更多详细信息的主题。  
  
 在本课中，您将执行一个匹配活动来删除供应商列表中的重复项。 首先，您创建包含一个规则的匹配策略以识别供应商列表中的重复项并将该策略发布到知识库。 接着，您创建并运行一个用于匹配的数据质量项目。 最后，您将匹配活动的结果导出到 Excel 文件，您以后在将数据上载到 Master Data Services (MDS) 时将使用该文件。  
  
## <a name="next-step"></a>下一步  
 [任务 1：定义匹配策略](../../2014/tutorials/task-1-defining-a-matching-policy.md)  
  
  