---
title: 第 2 课： 清理使用供应商知识库的供应商数据 |Microsoft 文档
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- data-quality-services
- integration-services
- master-data-services
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 215c14de-fc3f-46de-a022-bf69b9ea2a96
caps.latest.revision: 7
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.openlocfilehash: 1b4c227ff846649e29b7efc0ad50e4b13416c48c
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36016277"
---
# <a name="lesson-2-cleansing-supplier-data-using-the-suppliers-knowledge-base"></a>第 2 课：使用 Suppliers 知识库清理供应商数据
  你可以在本课程中，来清理通过使用 Excel 文件中的供应商数据**供应商**具有在第一课中创建的知识库。 在 DQS 中清理数据包括**计算机辅助进程**来分析数据符合知识库中的知识，和**交互进程**，可用于查看和修改从计算机辅助进程的结果。 数据清理功能可以识别数据源中不正确的数据，然后对这些数据进行更正或提出更正建议。 它还通过使用域值、同义词的前导值、域规则、基于字词的关系和参考数据来使客户数据标准化和更加丰富。 您可以通过交互方式批准或拒绝计算机辅助过程建议的更改。 请参阅[数据清理](http://msdn.microsoft.com/library/gg524800.aspx)有关详细信息。  
  
 计算机辅助过程使用以下阈值，您可以使用 DQS 客户端主页上的“配置”选项来配置这些阈值。  
  
-   **建议的最低分数：** 的最低分数或置信度级别用于 DQS 建议的值替换。  
  
-   **用于自动更正的最低分数：** 的最低分数或置信度级别由 DQS 用于自动更正的值。  
  
 请参阅[Configure Threshold Values for Cleansing and Matching](http://msdn.microsoft.com/library/hh510415.aspx)有关如何配置这些设置的详细信息。  
  
 在本课中，您将执行以下任务来使用 Suppliers 知识库清理输入数据。  
  
1.  创建用于清理的数据质量项目，选择 Suppliers 知识库作为要用于分析和清理 Excel 文件中源数据的知识库，然后选择“清理”活动。  
  
2.  将要清理的 Excel 列映射为知识库中适当的 DQS 域/复合域。  
  
3.  运行计算机辅助的清理活动。 计算机辅助过程会在数据质量客户端中显示数据质量信息，您可以使用该客户端以交互方式清理数据。  
  
4.  查看和管理清理活动的结果。 您可以查看计算机辅助过程找到的正确值、不正确但是已更正的值、不正确并提供更改建议的值或无效值。 您可以交互方式批准或拒绝更改，通过使用“更正为”字段更正或覆盖计算机辅助过程给出的建议值。  
  
5.  将清理过程的结果导出到 Excel 文件。  
  
6.  将清理项目的值导入域，以使用新的规则、值和更正等增加知识库中的知识。  
  
## <a name="next-step"></a>下一步  
 [任务 1：创建数据质量项目](../../2014/tutorials/task-1-creating-a-data-quality-project.md)  
  
  