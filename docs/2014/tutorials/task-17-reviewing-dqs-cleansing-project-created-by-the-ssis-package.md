---
title: 任务 17： 查看 DQS 清理项目创建的由 SSIS 包 |Microsoft 文档
ms.custom: ''
ms.date: 12/29/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- data-quality-services
- integration-services
- master-data-services
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: fc6cc258-72f5-4593-8edb-9f5bc66de9db
caps.latest.revision: 6
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.openlocfilehash: 4226fd9a8e8eb8aa2851eed8eb318b8535010c8a
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36127204"
---
# <a name="task-17-reviewing-dqs-cleansing-project-created-by-the-ssis-package"></a>任务 17：查看由 SSIS 包创建的 DQS 清理项目
  在该任务中，您将打开由 SSIS 包在 DQS 客户端中创建的 DQS 项目，检查清理过程的结果，并可选执行交互式清理和导出结果。  
  
1.  启动**数据质量客户端**。  
  
2.  单击**活动监视**中**管理**窗格。  
  
3.  基于对列表进行排序**活动开始时间**若要查看的最新记录。  
  
4.  请注意你看到以下格式的项目的名称： **CleanseAndCurate.Cleanse Supplier Data.GUID**。  
  
     ![DQS 清理项目创建的 SSIS 包](../../2014/tutorials/media/et-reviewingdqscpcreatedbythessispackage.jpg "DQS 清理项目创建的 SSIS 包")  
  
5.  请注意，中的值**是活动**字段是**Active**。  
  
6.  单击**探查器**在底部窗格中，若要查看的 SSIS 包执行的清理活动的探查器统计信息的选项卡。  
  
7.  单击**关闭**关闭**管理**屏幕。  
  
8.  在主页面中的**DQS 客户端**，单击**打开数据质量项目**中**数据质量项目**窗格。  
  
9. 在项目列表中，选择由 SSIS DQS 清理组件创建的项目。 项目的名称应采用格式： **（以红色） CleanseAndCurate.Cleanse Supplier Data.GUID**。 你可能需要基于对列表进行排序**创建日期**列并查找最新记录。  
  
10. 单击“下一步” 。  
  
11. **管理和查看结果**页应为你从交互式清理未在本教程前面部分中所熟悉。  
  
12. 查看清理结果。 在下一页中，您还可以执行交互式清理，并将结果导出到 Excel 文件或数据库中。  
  
13. 单击“下一步” 。 在此**导出**页上，您可以将结果导出到 excel 文件，CSV 文件，或到 SQL 数据库。  
  
14. 单击**完成**完成活动。  
  
15. 在主页面中的**DQS 客户端**，单击**活动监视**中**管理**窗格。  
  
16. 请注意，值**IsActive**字段的项目是**已结束**现在。  
  
## <a name="next-step"></a>下一步  
 [结语](../../2014/tutorials/conclusion.md)  
  
  