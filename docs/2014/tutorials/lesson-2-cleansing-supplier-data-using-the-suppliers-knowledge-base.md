---
title: 第 2 课： 清理供应商数据使用 Suppliers 知识库 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- data-quality-services
- integration-services
- master-data-services
ms.topic: conceptual
ms.assetid: 215c14de-fc3f-46de-a022-bf69b9ea2a96
author: douglaslms
ms.author: douglasl
manager: craigg
ms.openlocfilehash: d957c5ddb394828ed29f169796bcb2bf19cea6a3
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2018
ms.locfileid: "48162587"
---
# <a name="lesson-2-cleansing-supplier-data-using-the-suppliers-knowledge-base"></a>第 2 课：使用 Suppliers 知识库清理供应商数据
  通过使用在本课程中，清理 Excel 文件中的供应商数据**供应商**第一课中创建的知识库。 DQS 中的数据清理包括**计算机辅助过程**前者分析数据与知识库中知识的相符和一个**交互进程**，可用于查看和修改从在计算机辅助过程的结果。 数据清理功能可以识别数据源中不正确的数据，然后对这些数据进行更正或提出更正建议。 它还通过使用域值、同义词的前导值、域规则、基于字词的关系和参考数据来使客户数据标准化和更加丰富。 您可以通过交互方式批准或拒绝计算机辅助过程建议的更改。 请参阅[数据清理](http://msdn.microsoft.com/library/gg524800.aspx)的更多详细信息。  
  
 计算机辅助过程使用以下阈值，您可以使用 DQS 客户端主页上的“配置”选项来配置这些阈值。  
  
-   **用于建议的最低分数：** 的最低分数或置信度级别由 DQS 用于建议替换值。  
  
-   **用于自动更正的最低分数：** 的最低分数或置信度级别由 DQS 用于自动更正值。  
  
 请参阅[配置清理和匹配活动的阈值值](http://msdn.microsoft.com/library/hh510415.aspx)有关如何配置这些设置的详细信息。  
  
 在本课中，您将执行以下任务来使用 Suppliers 知识库清理输入数据。  
  
1.  创建用于清理的数据质量项目，选择 Suppliers 知识库作为要用于分析和清理 Excel 文件中源数据的知识库，然后选择“清理”活动。  
  
2.  将要清理的 Excel 列映射为知识库中适当的 DQS 域/复合域。  
  
3.  运行计算机辅助的清理活动。 计算机辅助过程会在数据质量客户端中显示数据质量信息，您可以使用该客户端以交互方式清理数据。  
  
4.  查看和管理清理活动的结果。 您可以查看计算机辅助过程找到的正确值、不正确但是已更正的值、不正确并提供更改建议的值或无效值。 您可以交互方式批准或拒绝更改，通过使用“更正为”字段更正或覆盖计算机辅助过程给出的建议值。  
  
5.  将清理过程的结果导出到 Excel 文件。  
  
6.  将清理项目的值导入域，以使用新的规则、值和更正等增加知识库中的知识。  
  
## <a name="next-step"></a>下一步  
 [任务 1：创建数据质量项目](../../2014/tutorials/task-1-creating-a-data-quality-project.md)  
  
  
